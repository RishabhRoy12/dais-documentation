# Search Console Flow

> Written for the **Search Console** page (`/analytics/console-insights`, `doc analytics/02-search-console.md`). Sidebar: ANALYTICS group, 2nd item. The page's internal name is "Console Insights" (route and usage label); the sidebar and title say "Search Console".

**Notation:** **GSC** = Google Search Console. The **GSC property** = the Search Console property of the brand's website (shown on the page as "Property: {GSC property}", for example `sc-domain:{domain}`). A **branded query** = a search query that contains the brand name, its variations, misspellings or products. A **non-branded query** = any other query.

**Goal:** the page shows how the brand's website performs in Google search: clicks, impressions, CTR and average position for a chosen date range, with four breakdowns (queries, pages, devices, countries). All of this data comes from **GSC**. The only part that is not from GSC is the **branded / non-branded split**, which the System adds to the queries. This page is about Google search only, so it does not depend on which AI models are enabled for the brand.

## Where the data comes from

| Data on the page | Source | Call (per the page docs) |
|------------------|--------|--------------------------|
| KPI cards (Total Clicks, Total Impressions, Avg CTR, Avg Position) | **GSC** | `POST fetch-search-console-data` (called again for the compare range when Compare is on) |
| Clicks & Impressions Over Time (chart) | **GSC** | `POST fetch-search-console-data` |
| Top Queries, Top Pages, Devices, Countries | **GSC** | `POST fetch-search-console-data` |
| Branded / Non-branded split and counts | **System** (AI-assisted), applied to all queries that came from GSC | `POST classify-branded-queries` |
| The "Property: {GSC property}" label | The brand's connected GSC property | – |
| Brand lookup | Brands list (by brand name) | `GET brands` |
| Usage tracking | System | `POST user_page_sessions` (`/analytics/console-insights`, "Console Insights") |

## Purpose and Access

The page shows:

1. **Control bar:** Start and End dates, **Compare** toggle (with Compare Start and Compare End), **Refresh**, and the "Property: {GSC property}" label (not clickable). In compare mode a **period legend** appears under it.
2. **Four KPI cards:** TOTAL CLICKS, TOTAL IMPRESSIONS, AVG CTR, AVG POSITION (no ⓘ tooltips).
3. **Clicks & Impressions Over Time:** a dual-axis line chart. Clicks on the left axis, impressions on the right axis.
4. **Breakdown card** with four tabs: **Top Queries** (default), **Top Pages**, **Devices**, **Countries**, plus a search box on every tab. On Top Queries the client can filter **All / Branded / Non-branded**.

The client can only view the page. The client can pick the start and end date, turn **Compare** on, press **Refresh**, switch tabs, search inside a table and filter the queries. The client cannot add or change any data.

Not on this page: a date preset dropdown, pagination, export or download, column sorting, row click-through, KPI tooltips.

## In short

1. The brand gives us access to its GSC property (once, fixed for the brand). Without that access the Search Console sidebar item is locked.
2. The page fetches the performance data live from GSC for the chosen date range (nothing is copied or stored).
3. The System marks each returned query as branded or non-branded.
4. The default range is 28 days, ending 2 days before today (GSC is about 2 days behind).
5. The client can change the dates, compare with the previous period, or press Refresh to read the data again.

## System rules

- All numbers come from **GSC**: the KPI cards, the chart and the four tables.
- The brand connects its **GSC property** by giving us access to the property (once). The property is fixed for the brand and is shown on the page as "Property: {GSC property}".
- **Locked item rule:** the Search Console sidebar item is **locked** for a brand when we do not have access to its GSC property.
- **Live data:** GSC data is fetched live every time (for the chosen dates, and again on Refresh). It is not copied or stored.
- **Reporting lag:** GSC data is about 2 days behind. So the default end date is **today minus 2 days**, and the default start date is 28 days before the end date. Dates after today are greyed out and cannot be picked (each picker is a single-month calendar).
- **KPI maths:** Avg CTR = clicks ÷ impressions over the range. Avg Position is the average position reported by GSC (lower is better).
- **Branded / non-branded** is decided by the System (AI-assisted) and can occasionally be wrong (the page says so in an ⓘ "About branded queries" tooltip next to the filter). It applies only to the **Top Queries** tab: Branded ({n}) + Non-branded ({n}) = All, counted in queries.
- Changing the start date, the end date, the compare dates, or pressing **Refresh**, reads the data from GSC again (no page reload), and the branded split is re-run for the queries that come back.
- **Compare** (off by default) shows the previous period (equal length, immediately before it by default; Compare Start and Compare End can be changed) as "vs {value}" only. There is no percentage change on this page. In compare mode:
  - A period legend shows both date ranges.
  - The KPI cards show "vs {previous value}".
  - The chart title gets "(Current vs Previous)" and two extra orange dotted lines, Clicks (prev) and Impressions (prev).
  - Every metric column in all four tables gets the subtitle "(Current vs Previous)", and each cell shows the current value with "vs {previous value}" below it.
- **Tabs and search:** switching a tab changes only the table, its search box and the filter row. The KPI cards and the chart do not change. The search box filters rows live by the text in the first column. The branded filter exists only on Top Queries, and search text is per tab.
- **Table contents:** Top Queries lists all queries returned by GSC for the range. Top Pages has one row per page (full URL). Devices has 3 rows: DESKTOP, MOBILE, TABLET. Countries has one row per country, shown as a lowercase 3-letter code (for example `ind`, `gbr`, `usa`).
- Rows are ordered by clicks, highest first, as returned by the data call. Columns cannot be sorted. Rows are not clickable. The table body scrolls inside the card with the header kept visible.
- **Empty search:** if the search finds nothing, the table shows "No query match", "No page match", "No device match" or "No country match" with the typed text, depending on the tab.
- **Errors:** if the data call fails, the page shows an error toast ("Edge Function returned a non-2xx status code") and keeps the previous numbers and chart on screen.- The data is **brand scoped**: it follows the brand chosen in the top bar.
- The client cannot add or change any data.

## Data and Storage

| Data | Source | Stored where | Notes |
|------|--------|--------------|-------|
| Brand ↔ GSC property | Brand gives us access to the property | Brand setup | Set once, fixed for the brand. No access = Search Console item locked |
| Clicks, impressions, CTR, position (totals, per day, per query, page, device, country) | GSC | Not stored (fetched live) | Fetched live for the chosen date range (and again for the compare range), about 2 days behind |
| Branded / non-branded label per query | System (AI-assisted) | Not stored (per the page docs, worked out for the queries returned) | Re-run on every read |
| Page visit | System | Usage tracking (`user_page_sessions`) | Recorded when the page is opened |

Page details: `doc analytics/02-search-console.md`.

## Other pages that use the same data

The **Overview** page uses the same Search Console data for its organic landing-page table (Clicks, Impressions, CTR, Position and the "GSC matched" pill). See [01_overview_flow.md](../../flows/analytics flows/01_overview_flow.md).

## Runbook: Client

1. Open **Analytics → Search Console**.
2. Check the date range (28 days ending 2 days ago by default). Change the start or end date if needed, or turn **Compare** on (and adjust Compare Start and Compare End if needed).
3. Read the four KPI cards and the Clicks & Impressions chart.
4. Open the tabs: **Top Queries** (use All / Branded / Non-branded), **Top Pages**, **Devices**, **Countries**. Use the search box to find a row.
5. Press **Refresh** to read the latest data again.

## Troubleshooting

| Situation | What to check |
|-----------|---------------|
| No data or zeros | We may not have access to the brand's GSC property (the item would be locked), or the date range has no data. |
| Last two days are missing or low | Expected. GSC is about 2 days behind. |
| Error toast and numbers did not change | The data call failed. Check the dates, then press Refresh. |
| A query is in the wrong group (branded / non-branded) | The split is AI-assisted and can be wrong. |
| Branded and non-branded counts look off | They count queries, and All = Branded + Non-branded. |
| Search shows "No ... match" | Nothing in the first column contains the typed text. Clear the search box. |
| Someone wants to upload or export GSC data | Not needed and not available on this page. |
