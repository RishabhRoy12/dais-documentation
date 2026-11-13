# Analytics → Competitors Intelligence
Route: `/analytics/competitors` · Subtitle: "Brand mention tracking and competitive analysis"

## Purpose
Shows how the brand compares with competitors in three ways: **AI share of voice**, **AI-cited sources**, and **traditional SEO strength** (traffic share, authority, keywords, backlinks).

## Controls
Brand multi-select ("10 of 224 brands") · range "Last 7 days" · engine toggle Gemini / ChatGPT · brand filter on keyword table ("10 of 10 brands").

## Layout

```mermaid
flowchart TB
  S["AI summary line (BETA)<br/>'1% traffic share, authority 6, trailing Zoicpharmaceuticals 55% ...'"]
  RA["RECOMMENDED ACTIONS (BETA)<br/>cards: COMPETITION / VISIBILITY / GROWTH × HIGH / MEDIUM"]
  SOV["Share of Voice (Gemini or ChatGPT)"]
  SRC["Brand's Mention in AI Indexed Sources (ChatGPT)"]
  AU["Authority Score table<br/>Domain · Organic Traffic · Organic Keywords · Backlinks · Ref. Domains · Authority Score"]
  TS["Domain by Traffic share"]
  KW["Branded vs Non-branded Keywords by Domain"]
  S --> RA --> SOV --> SRC --> AU --> TS --> KW
```

## Architecture and data flow

```mermaid
flowchart LR
  P["Competitors page"]
  P -->|"GET brands (or filter)"| T1[("brands")]
  P -->|"{brandName, dateRangeDays}<br/>{brandName}<br/>{brandName, startDate, endDate}"| F1["fetch-competitor-mentions"]
  P -->|"{p_brand_name, p_days, p_offset, p_limit}"| R1["rpc get_share_of_voice_window"]
  P --> F2["fetch-semrush-competitor-data"]
  P --> F3["fetch-traffic-share-data"]
  P --> F4["fetch-keywords-by-domain"]
  P -->|"{page, brand, source, signals}"| F5["generate-page-insights"]
  F1 --> LLM[("AI answer runs<br/>ChatGPT / Gemini")]
  R1 --> LLM
  F2 --> SEM["Semrush"]
  F3 --> SEM
  F4 --> SEM
  F5 --> AI["LLM → recommendations + summary"]
  SEM -. "snapshot dated July 2026" .-> P
```

## Sequence on load

```mermaid
sequenceDiagram
  actor U as User
  participant P as Page
  U->>P: open (Gemini, 7 days default)
  P->>P: load brand list (224 brands, 10 selected)
  par
    P->>P: fetch-competitor-mentions (window A)
    P->>P: fetch-competitor-mentions (all-time)
    P->>P: fetch-competitor-mentions (explicit range)
    P->>P: get_share_of_voice_window
    P->>P: fetch-semrush-competitor-data
    P->>P: fetch-traffic-share-data
    P->>P: fetch-keywords-by-domain
  end
  P->>P: generate-page-insights with signals from the above
  P-->>U: charts, tables, RECOMMENDED ACTIONS
  U->>P: toggle engine or brand set
  P->>P: re-run mention and share-of-voice calls
```

## Observations
- **Two data clocks:** AI mention data is live (last 7 days) while Semrush authority/traffic is a snapshot ("Last updated: July 2026").
- **Recommendation cards** are tagged by category (COMPETITION, VISIBILITY, GROWTH) and priority (HIGH, MEDIUM) and include a concrete next step (e.g. audit top organic queries of the 55%-traffic competitor).
- `fetch-competitor-mentions` is called three times with different parameter sets, an optimisation opportunity.
- The competitor set looks cross-industry (pharma, biotech), so competitor selection is probably brand-configured rather than auto-detected by industry (inferred).
