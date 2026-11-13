# Analytics → Overview
Route: `/analytics/overview` · Subtitle: "Comprehensive analytics dashboard"

## Purpose
One-screen summary that combines **AI-search traffic** (sessions referred by ChatGPT, Perplexity and Gemini), **organic traffic** (Google), and **week-wise rank tables** for prompts and keywords.

## Controls
Compare toggle · date-range preset (*Last 30 Days*) · date picker (Oct 14 – Nov 12, 2026) · date selector "26 of 26 dates" · engine toggle (ChatGPT / Gemini) on the prompt-ranking block.

## Page layout

```mermaid
flowchart TB
  H["Header: breadcrumb, Compare, preset, date picker"]
  K["KPI strip (Organic + AI Search)<br/>Active users 379 · New users 346 · Sessions 543 · Key events 0"]
  INS["Auto-insight (BETA): chatgpt.com = 83% of AI Search traffic"]
  BAN["Data-status banner: 'No data collected yet'"]
  A["Analytics (AI Search)<br/>Active Users by time (line) · Sessions by AI platform (bar)<br/>Session-source table · Landing Page Wise table"]
  O["Analytics (Organic Traffic)<br/>GA4 organic + GSC clicks/impressions per landing page"]
  P["Prompt Ranking Performance Week Wise (ChatGPT / Gemini)"]
  KW["Keyword Ranking Performance Week Wise"]
  D["AI Search Decision Table"]
  DS["AI Search Discovery Table"]
  H --> K --> INS --> BAN --> A --> O --> P --> KW --> D --> DS
```

## Architecture and data flow

```mermaid
sequenceDiagram
  actor U as User
  participant P as Overview page
  participant G as fetch-ga4-analytics
  participant S as fetch-search-console-data
  participant K as fetch-keywords-ranking
  participant W as fetch-prompt-weekly-summary
  participant GA as Google Analytics 4
  participant GS as Search Console
  participant DB as Supabase tables
  U->>P: open page / change dates
  par parallel loads
    P->>G: {startDate, endDate}
    G->>GA: sessions by source, landing page
    P->>S: {brand, startDate, endDate, rowLimit}
    S->>GS: clicks, impressions per page
    P->>K: keyword ranks
    K->>DB: ranking snapshots
    P->>W: weekly prompt summary
    W->>DB: weekly_prompt_ranking
  end
  G-->>P: AI-referrer rows (chatgpt.com, perplexity.ai, gemini.google.com)
  S-->>P: landing-page clicks / impressions
  K-->>P: week-wise keyword grid
  W-->>P: week-wise prompt grid
  P->>P: classify AI sources, compute % share, NEW-page flags
  P-->>U: render KPIs, charts, tables
```

## Key logic (observed)
- **AI-source classification:** GA4 sessions whose source is an AI domain (chatgpt.com, perplexity.ai, gemini.google.com) feed the AI Search block. The "83%" insight is 44 ÷ 53 AI sessions.
- **Landing Page Wise table:** columns Landing page · Active users · New users · Sessions · Key events. Rows carry a **NEW** tag when a page first received AI traffic in the period.
- **Session source table** adds Bounce rate. Totals: 40 active users, 53 sessions, 20.75% bounce.
- **Organic table** joins GA4 sessions with GSC clicks and impressions by landing page.

## Edge cases
| Case | Behaviour |
|---|---|
| Banner says "Website analytics: Not collected / Keyword ranking: Not collected" while GA4 data renders | Contradiction (see [09](../09-observations-and-gaps.md)); the banner likely reads a different status flag than the data calls |
| Google not connected | GA4 and GSC blocks would be empty (inferred from `google_connections`) |
| Key events = 0 | No conversion events configured or fired in GA4 |
