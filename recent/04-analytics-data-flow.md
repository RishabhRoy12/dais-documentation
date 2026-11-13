# 04 · Analytics Data Flow

Maps each analytics page to the backend call that feeds it and the source data behind it. Calls were captured from the network log. The upstream source is inferred from the function name and what the page displays.

## Page → function → source

```mermaid
flowchart LR
  subgraph Pages
    BP["Brand Pulse"]
    OV["Overview"]
    SC["Search Console"]
    CP["Competitors"]
    PR["Prompt Ranking"]
    KR["Keyword Ranking"]
    CT["Citation Overview"]
    CN["Concept Overview"]
    RD["Reddit Overview"]
    YT["YouTube Analytics"]
    PL["Product Leaderboard"]
    LL["Local Listings"]
    AT["Activity Tracker"]
    MOM["Strategic Sync-ups"]
  end

  subgraph Functions["Edge functions / RPC / tables"]
    f1["fetch-ga4-analytics"]
    f2["fetch-search-console-data"]
    f3["fetch-keywords-ranking"]
    f4["fetch-prompt-weekly-summary"]
    f5["fetch-prompt-visibility"]
    f6["fetch-competitor-mentions"]
    f7["fetch-semrush-competitor-data<br/>fetch-traffic-share-data<br/>fetch-keywords-by-domain"]
    f8["rpc get_share_of_voice_window"]
    f9["fetch-citation-data<br/>fetch-sources-data<br/>table citation_graph_data"]
    f10["fetch-concept-data<br/>fetch-concept-by-brand"]
    f11["fetch-reddit-overview"]
    f12["fetch-youtube-data"]
    f13["fetch-product-leaderboard"]
    f14["fetch-local-listings"]
    f15["fetch-activity-data"]
    f16["manage-mom"]
    f17["classify-branded-queries"]
    f18["table weekly_prompt_ranking<br/>prompts_brandwise"]
    f19["generate-page-insights"]
    f20["fetch-searchscore-trend<br/>fetch-dropped-keywords<br/>fetch-improved-keywords"]
  end

  subgraph Src["Sources"]
    GA["GA4"]
    GS["Search Console"]
    SM["Semrush"]
    AI["AI engine prompt runs<br/>ChatGPT / Gemini"]
    RE["Reddit"]
    YU["YouTube"]
  end

  BP --> f20 & f3 & f6 & f9 & f5 & f1
  OV --> f3 & f4 & f2 & f1
  SC --> f2 & f17
  CP --> f6 & f7 & f8 & f19
  PR --> f18 & f5 & f19
  KR --> f3 & f19
  CT --> f9 & f19
  CN --> f10
  RD --> f11
  YT --> f12
  PL --> f13
  LL --> f14
  AT --> f15
  MOM --> f16

  f1 --> GA
  f2 --> GS
  f17 --> GS
  f7 --> SM
  f3 --> SM
  f5 --> AI
  f4 --> AI
  f6 --> AI
  f9 --> AI
  f10 --> AI
  f11 --> RE
  f12 --> YU
```

## Overview page in detail

The Overview page loads four functions in parallel and renders them in two blocks.

```mermaid
sequenceDiagram
  participant U as User
  participant P as /analytics/overview
  participant G as fetch-ga4-analytics
  participant S as fetch-search-console-data
  participant K as fetch-keywords-ranking
  participant W as fetch-prompt-weekly-summary
  U->>P: pick date range (default last 30 days, optional Compare)
  par
    P->>G: startDate, endDate
    P->>S: brand, startDate, endDate, rowLimit
    P->>K: keyword rankings
    P->>W: weekly prompt summary
  end
  G-->>P: active users, new users, sessions, key events, sessions by AI platform
  S-->>P: clicks, impressions, landing pages
  K-->>P: keyword week-wise ranks
  W-->>P: ChatGPT prompt ranking week-wise
  P-->>U: KPI strip, AI Search charts, Organic table, AI Search Decision and Discovery tables
```

Observed values for the test brand: 379 active users, 346 new users, 543 sessions over Oct 14 to Nov 12 2026. chatgpt.com drives 44 of the 53 AI-search sessions (about 83%).

## Metric glossary

| Metric | Meaning on the dashboard |
|---|---|
| Visibility % (Gemini / ChatGPT) | Share of tracked prompts in which the brand appears in that engine's answer |
| Share of Voice | Brand mentions relative to competitors across tracked prompts (`get_share_of_voice_window` over `p_days`, `p_offset`, `p_limit`) |
| Citations | Times a brand domain is cited as a source in AI answers |
| Concepts + sentiment | Topics associated with the brand in AI answers, split positive, neutral or negative |
| Authority score | Semrush domain authority (page notes "Last updated: July 2026") |
| AI Search Decision / Discovery tables | Landing pages receiving AI-referred sessions, bucketed by funnel intent (inferred) |

## Insight generation loop

```mermaid
flowchart LR
  D["Page data + signals"] --> G["generate-page-insights<br/>{page, brand, source, signals}"]
  G --> R["RECOMMENDED ACTIONS panel"]
  R --> X["Execution items<br/>(blogs, schema, FAQ, citations)"]
```

Used on Competitors, Prompt Ranking, Keyword Ranking and Citations.

## Brand Pulse (home) flow

```mermaid
flowchart TD
  BP["/brand-pulse"] --> A["fetch-searchscore-trend → search_scores"]
  BP --> B["fetch-keywords-ranking"]
  BP --> C["fetch-improved-keywords"]
  BP --> D["fetch-dropped-keywords"]
  BP --> E["fetch-prompt-visibility"]
  BP --> F["fetch-competitor-mentions"]
  BP --> G["fetch-citation-data"]
  BP --> H["fetch-ga4-analytics"]
  C --> S1["Fastest Rising Prompts"]
  D --> S2["Prompts to Bring Back"]
  E --> S3["Trending This Week / Newly Appearing"]
  A --> S4["Key Movements"]
  F --> S5["Where to Focus Next"]
  G --> S5
  S1 & S2 & S3 & S4 & S5 --> OP["Opportunities"]
```
