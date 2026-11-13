# Analytics → Citation Overview
Route: `/analytics/citations`

## Purpose
Shows **which web sources AI engines cite** when answering the tracked prompts, and whether the brand's own domain is among them.

## Controls
Brand multi-select ("10 of 10 brands") · range "Last 7 days" · engine toggle ChatGPT / Gemini.

## Layout

```mermaid
flowchart TB
  S["AI summary (BETA)<br/>'0% citation rate across 22 prompts; 100% absence rate'"]
  RA["RECOMMENDED ACTIONS: RISK / VISIBILITY"]
  A["Brand's Citations in AI Indexed Sources (ChatGPT)<br/>Prompts × weekly dates, ✓ / ✗ per cell"]
  B["Brand Domain Citations<br/>cited domains per brand (e.g. herbalchakra.in, dabur.com, cdsco.gov.in)"]
  S --> RA --> A --> B
```

## Architecture and data flow

```mermaid
flowchart LR
  P["Citation Overview page"]
  P -->|"GET brands (or)"| BR[("brands")]
  P --> F1["fetch-citation-data"]
  P -->|"{startDate, endDate}"| F2["fetch-sources-data"]
  P -->|"GET order, offset, limit"| CG[("citation_graph_data")]
  P --> F3["generate-page-insights"]
  F1 --> ANS[("AI answers per prompt per week<br/>cited / not cited")]
  F2 --> SRC[("cited source URLs and domains")]
  CG --> SRC
```

## Sequence

```mermaid
sequenceDiagram
  actor U as User
  participant P as Page
  participant DB as Supabase
  participant F as Edge functions
  U->>P: open
  P->>DB: brands (current + peers)
  P->>F: fetch-citation-data
  F-->>P: prompt × week citation matrix
  P->>F: fetch-sources-data (all-time)
  P->>F: fetch-sources-data {startDate, endDate}
  F-->>P: cited domains and counts
  P->>DB: citation_graph_data (paged: offset, limit)
  P->>F: generate-page-insights
  F-->>P: summary + cards
  P-->>U: matrix (✓/✗), domain lists, cards
  U->>P: toggle engine / brand set
  P->>F: re-query
```

## Definitions
- **Citation rate** = prompts where the brand's domain appears among cited sources ÷ tracked prompts.
- **Absence rate** = 1 − citation rate (here 100%).
- **WoW citation growth** = change in citations vs the prior week (0 here).
- **Brand Domain Citations** list shows peers' domains too (dabur.com, himalaya...), so it is also a source-gap tool: domains AI trusts that the brand is not on.

## Relationship to Execution
Gaps found here feed the off-page execution pages (Profile Citation, Directories, Guest Post, Reddit/Quora, etc.). See [../05-execution-workflow.md](../05-execution-workflow.md).

## Note
A second route `/analytics/citation-overview` and `/analytics/citation-leaderboard` exist in the router but are not in the sidebar.
