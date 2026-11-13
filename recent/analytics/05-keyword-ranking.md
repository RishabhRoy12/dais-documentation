# Analytics → Keyword Ranking
Route: `/analytics/keyword-ranking`

## Purpose
Traditional Google rank tracking for a fixed keyword list (20 for the test brand), shown as tier counts and a week-by-week grid.

## Controls
Date selector (latest "1 August 2026", "9 of 9 dates") · sortable date columns (▲ marks the active sort).

## Layout

```mermaid
flowchart TB
  T["Tier tiles as of selected date<br/>Top 5 = 0 · Top 10 = 2 · Top 20 = 3 · Top 50 = 4 · Top 100 = 4"]
  S["AI summary (BETA): 'zero movement 25 Jul → 01 Aug; 4 of 20 in Top 100'"]
  RA["RECOMMENDED ACTIONS: VISIBILITY / GROWTH cards"]
  G["Keyword Performance Week Wise<br/>Sr. No · Keywords · one column per week"]
  T --> S --> RA --> G
```

## Architecture and data flow

```mermaid
sequenceDiagram
  actor U as User
  participant P as Keyword Ranking page
  participant DB as Supabase
  participant K as fetch-keywords-ranking
  participant I as generate-page-insights
  U->>P: open
  P->>DB: rpc get_keyword_selection_access(_brand_name)
  P->>K: fetch rankings for brand
  K->>DB: weekly ranking snapshots
  K-->>P: keywords × dates (position per week)
  P->>P: bucket into Top 5/10/20/50/100 for selected date
  P->>P: compute week-over-week delta
  P->>I: {page, brand, source, signals (tiers, deltas)}
  I-->>P: summary + action cards
  P-->>U: tiles, cards, grid
```

## Logic
- **Tier tiles are cumulative** (Top 10 includes Top 5). Here 0 → 2 → 3 → 4 → 4.
- **Movement** compares the selected date with the previous weekly snapshot, so "zero keyword movement" means identical positions.
- **Unranked** = tracked but outside the top 100 (16 of 20 here).
- Snapshots are **weekly on Saturdays** and the newest in this account is 1 August 2026, about 3 months older than today. Either the tracker stopped or the snapshots are produced manually. Confirm with the team.
- Access to *selecting* keywords is permission-checked (`get_keyword_selection_access`), so staff or the client can edit the keyword list only if allowed.

## Related
Brand Pulse reuses the same function for "Fastest Rising" and "Dropped" views (`fetch-improved-keywords`, `fetch-dropped-keywords`).
