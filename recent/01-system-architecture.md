# 01 · System Architecture

How the DareAISearch platform (`app.dareaisearch.com`) is put together, as observed from the live app and its JS bundle.

## Facts observed

| Layer | What it is | Evidence |
|---|---|---|
| Frontend | React SPA built with Vite, React Router, Radix UI components, installed as a PWA (service worker, `apple-mobile-web-app-*` tags). Originally generated with **Lovable** (`meta author`). | `index.html`, `/assets/index-*.js`, `registerSW.js` |
| Backend | **Supabase**: Auth, PostgREST (`/rest/v1`), RPC functions, and Edge Functions (`/functions/v1`). | all XHR go to one `*.supabase.co` project |
| Auth | Supabase email/password plus "Continue with Google". Google is also connected separately for GA4 and Search Console data. | `/auth/v1/token`, `google-oauth-url`, `google_connections` |
| Analytics sources | GA4, Google Search Console, Semrush, AI-engine prompt tracking (ChatGPT, Gemini), Reddit, YouTube. | edge functions listed in doc 07 |
| Telemetry | Microsoft Clarity, a first-party `/__l5e/trackevents` endpoint, and in-house `user_sessions` / `user_page_sessions` tables. | network log |
| Client cache | `localStorage`: `cachedUserProfile`, `preAuthBrandName`, `preAuthName`, `preAuthWebsiteUrl`, `sidebar-opened-before`. | bundle |

## Component diagram

```mermaid
flowchart TB
  subgraph Client["Browser (PWA)"]
    SPA["React SPA<br/>Vite + React Router + Radix UI"]
    SW["Service Worker"]
    LS[("localStorage<br/>cachedUserProfile, preAuth*")]
    SPA --- SW
    SPA --- LS
  end

  subgraph SB["Supabase project"]
    AUTH["Auth<br/>/auth/v1"]
    REST["PostgREST<br/>/rest/v1 (tables + RPC)"]
    EF["Edge Functions<br/>/functions/v1"]
    DB[("Postgres + RLS<br/>brands, prompts, records, ...")]
    AUTH --> DB
    REST --> DB
    EF --> DB
  end

  subgraph EXT["External data sources"]
    GA4["Google Analytics 4"]
    GSC["Google Search Console"]
    SEM["Semrush"]
    LLM["AI engines<br/>ChatGPT / Gemini prompt runs"]
    RED["Reddit"]
    YT["YouTube"]
    GOOG["Google OAuth"]
  end

  subgraph TEL["Telemetry"]
    CL["Microsoft Clarity"]
    TE["/__l5e/trackevents"]
  end

  SPA -- "sign-in / session" --> AUTH
  SPA -- "table reads, RPC (RLS)" --> REST
  SPA -- "fetch-* / generate-* / import-* / send-*" --> EF
  SPA -- "page + session events" --> CL
  SPA --> TE
  EF --> GA4
  EF --> GSC
  EF --> SEM
  EF --> LLM
  EF --> RED
  EF --> YT
  AUTH <-- "OAuth" --> GOOG
```

## Request pattern

Two access paths exist, and which one a page uses tells you where its logic lives:

```mermaid
flowchart LR
  P["Page component"] -->|"simple CRUD / lists"| T["supabase.from(table)<br/>or rpc(fn)<br/>(row-level security in DB)"]
  P -->|"aggregation, external APIs, LLM calls"| F["supabase.functions.invoke(fn)<br/>(server-side secrets)"]
  T --> DB[("Postgres")]
  F --> DB
  F --> X["Third-party APIs"]
```

- **Execution pages** (Image Alt, Schema Markup, Reddit, and so on) read straight from `execution_*_records` tables.
- **Analytics pages** call edge functions (`fetch-*`), which aggregate GA4, GSC, Semrush and prompt-run data.
- **AI insight panels** ("RECOMMENDED ACTIONS") call `generate-page-insights` with `{page, brand, source, signals}`.

## Brand scoping (multi-tenant)

Almost every request is scoped by **brand**. Normal users see one brand (here *Herbal Chakra*). Internal staff can override it, which is why edge functions take `brandOverride`. Brand access is enforced by RLS plus helper RPCs such as `current_user_brand_name`, `get_prompt_selection_access` and `get_keyword_selection_access`.

```mermaid
flowchart LR
  U["User"] --> PR["profiles / user_roles"]
  PR --> B["brands"]
  B --> D1["prompts_brandwise"]
  B --> D2["weekly_prompt_ranking"]
  B --> D3["citation_graph_data"]
  B --> D4["execution_*_records"]
  B --> D5["brand_voice_*"]
  SA["sub_admin_brands"] -. "sub_admin sees several brands" .-> B
```
