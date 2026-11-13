# 06 · Intelligence & Content-Generation Workflows

The Intelligence menu holds the tools that create content or research. Only calls actually seen are listed. Several of these pages call their generation endpoints only after a user action, which a read-only crawl does not trigger.

## Tools overview

| Tool | Route | What it does (as seen) | Data touched |
|---|---|---|---|
| Brand Voice | `/intelligence/brand-voice` | Tabs: *Brand Voice Document*, *Brand Voice Review*. Lists Approved Blogs used to learn the voice. | `brand_voice_settings`, `brand_voices` (is_active), `brand_voice_source_docs` (is_primary), `brand_voice_blogs`, `fetch-execution-blogs` |
| Prompt Planner (BETA) | `/analytics/prompt-research` | Tabs: Related Topics, Prompts, Brands, Source Domains. Topic table: Topic, Volume, Prompts Count, Relevance Score. | (no calls on load, run on demand) |
| Blog Generator v2 | `/blog-generator-v2` | "Requests" list plus topic generation per brand. | `blog_topic_generation_v2`, `blog_column_layouts`, `team_members`, `get_blog_v2_brand_ref` |
| FAQ Creator | `/faq-generator` | Generates and stores FAQ sets per user. | `faq_results` |
| YouTube Intelligence | `/youtube-intelligence` | Generates YouTube optimisation output per user. | `youtube_intelligence_results` |
| Publisher Intelligence | `/intelligence` | Marketplace of publisher websites, with tabs *Marketplace / My Orders / Analytics* and filters. Used to buy placements. | `publisher_websites_public` |

## Brand-voice-driven content loop

```mermaid
flowchart TD
  SRC["Source docs<br/>brand_voice_source_docs"] --> BV["Brand Voice Document<br/>brand_voices (active version)"]
  AB["Approved blogs<br/>brand_voice_blogs / fetch-execution-blogs"] --> BV
  BV --> REV["Brand Voice Review tab"]
  BV -. "guides tone" .-> BG["Blog Generator v2"]
  PP["Prompt Planner<br/>topics, prompts, source domains"] --> BG
  BG --> EXB["Execution: Blogs<br/>Topic / Blog / Final status"]
  EXB -- "approved + published" --> AB
```

## Prompt Planner flow (inferred from tabs)

```mermaid
flowchart LR
  T["Related Topics<br/>Volume, Prompts Count, Relevance"] --> P["Prompts"]
  P --> B["Brands answered"]
  P --> S["Source Domains cited"]
  P -- "promote to tracked prompts" --> TRK["prompts_brandwise<br/>(Prompt Ranking)"]
```

The final arrow is an inference: access to selecting prompts is gated by `get_prompt_selection_access`.

## FAQ Creator and YouTube Intelligence (shared pattern)

```mermaid
sequenceDiagram
  actor U as User
  participant P as Page
  participant T as results table (RLS by user_id)
  U->>P: open page
  P->>T: HEAD count (user_id)
  P->>T: GET history ordered by created_at
  U->>P: submit input (URL / topic / video)
  P->>P: generation call (not captured, needs user input)
  P->>T: store result row
  P-->>U: show result + history
```

## Publisher Intelligence (marketplace)

```mermaid
flowchart LR
  M["Marketplace<br/>publisher_websites_public + Filters"] --> O["Place order"]
  O --> MY["My Orders"]
  MY --> AN["Analytics"]
```

## AI chat assistant

A floating sparkle button on every page opens a chat backed by the `analytics-chat` function and the `chat_messages` table, so the user can ask questions about their dashboard data.

## Hidden / staff-only intelligence routes (present in router, not in client sidebar)

`/intelligence/dais-crawler` and `/dais-crawler-v2` (site crawl jobs, with `/report/:jobId`), `/intelligence/competitor-research`, `/intelligence/recommendations`, `/intelligence/visibility-overview`, `/hdie` (+ `/backfill`, `/intelligence`), `/prompt-generator`, `/blog-generator` (v1). Purposes are guessed from names only and were not opened.
