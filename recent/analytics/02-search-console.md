# Analytics → Search Console
Route: `/analytics/console-insights`

## Purpose
Google Search Console performance for the brand's property (`sc-domain:herbalchakra.in`), with automatic **branded vs non-branded** query classification.

## Controls
Start / End date pickers (Oct 14 – Nov 10, 2026) · Compare toggle · **Refresh** · tabs **Top Queries / Top Pages / Devices / Countries** · query filter **All / Branded (16) / Non-branded (234)**.

## Layout

```mermaid
flowchart TB
  H["Header + property label + Refresh"]
  K["4 KPI tiles<br/>Total Clicks 335 · Impressions 6,215 · Avg CTR 5.39% · Avg Position 19.8"]
  C["Clicks & Impressions Over Time (dual-axis line)"]
  T{"Tabs"}
  Q["Top Queries<br/>Query · Clicks · Impressions · CTR · Position<br/>filter: All / Branded / Non-branded"]
  PG["Top Pages"]
  DV["Devices"]
  CT["Countries"]
  H --> K --> C --> T
  T --> Q & PG & DV & CT
```

## Architecture and data flow

```mermaid
sequenceDiagram
  actor U as User
  participant P as Search Console page
  participant R as REST brands
  participant S as fetch-search-console-data
  participant GSC as Google Search Console API
  participant C as classify-branded-queries
  U->>P: open / Refresh / change dates
  P->>R: GET brands (name, limit) → resolve brand + GSC property
  P->>S: {brand, startDate, endDate}
  S->>GSC: searchanalytics.query (dimensions: date, query, page, device, country)
  GSC-->>S: rows
  S-->>P: totals + per-dimension rows
  P->>C: {brand, queries[]}
  C-->>P: branded / non-branded label per query
  P-->>U: KPIs, chart, tabbed tables, filter counts (16 branded / 234 non-branded)
```

## Notes
- Authentication to GSC uses the user's Google connection (`google_connections`, `google-oauth-url`). Without it the page cannot load.
- Branded classification is server-side and likely uses the brand name and its variants (e.g. "herbal chakra", "pvt ltd"). Method not visible, so treat as inferred.
- Branded queries dominate clicks (top row "herbal chakra": 113 clicks at position 2.4), while non-branded queries ("shilajit manufacturer", "healthy snacks manufacturers in india") have impressions but low CTR, which is the growth gap.
- Date range ends Nov 10, two days before today, which is consistent with GSC's reporting lag.
