# Analytics → Search Console

| | |
|---|---|
| **Route** | `/analytics/console-insights` |
| **Page title** | Search Console |
| **Subtitle** | "Google Search Console performance — {Brand}" |
| **Breadcrumb** | DareAISearch › {Brand} › Analytics › Search Console |
| **Sidebar location** | ANALYTICS group → Search Console (2nd item) |
| **Shared shell** | Top bar, sidebar, breadcrumb and the Miss Daring assistant are documented in [00-global-layout.md](00-global-layout.md) |

> Documented from the live app. This page is documented on its own; how its data connects to other pages is left for a later pass. All numbers, queries, pages and dates are **placeholders such as `{n}`**, because they depend on the brand. Text in quotes is exact on-screen text.

---

## 1. Purpose

Shows the brand website's **Google Search Console (GSC)** performance for a chosen date range: total clicks, impressions, average CTR and average position, a clicks/impressions trend chart, and four breakdown tables (Top Queries, Top Pages, Devices, Countries). Queries can be split into **branded** and **non-branded**.

---

## 2. Page sections (top to bottom)

| # | Section | Contents |
|---|---|---|
| 1 | Page header | Breadcrumb, title, subtitle |
| 2 | Control bar | Start date, End date, Compare toggle (+ two compare dates), Refresh button, GSC property label |
| 3 | Period legend | Only in compare mode |
| 4 | Four KPI cards | Total Clicks, Total Impressions, Avg CTR, Avg Position |
| 5 | Clicks & Impressions Over Time | Dual-axis line chart |
| 6 | Breakdown card | Four tabs, search box, branded filter (Top Queries only), table |

---

## 3. Control bar

| Control | Type | Behaviour |
|---|---|---|
| **Start** | Button: calendar icon + "Start:" + date (`{Mon D, YYYY}`) | Opens a **single-month calendar** with previous/next month arrows and a month title (e.g. "November 2026"), weeks Su–Sa. Today's date is highlighted; **dates after today are greyed and disabled**. Picking a date reloads all data |
| **End** | Same as Start with "End:" | Same calendar. **Default end date is 2 days before today** (GSC reporting lag). Default start is 28 days before the end date (a 28-day window) |
| **Compare** | Toggle switch (off by default) with compare icon | See section 4 |
| **Refresh** | Outlined button, bold text | Re-runs the GSC fetch and the branded-query classification for the current dates (no page reload) |
| **Property label** | Small text, right-aligned: "Property: {GSC property}" (e.g. `sc-domain:{domain}`) | Shows which Search Console property the data comes from. Not clickable |

### Loading state
While data loads, KPI cards and chart show skeleton placeholders.

---

## 4. Compare mode (Compare toggle on)

| Area | What changes |
|---|---|
| Control bar | Two more date buttons appear: **Compare Start:** and **Compare End:**. Default = the period of equal length immediately before the current one |
| Period legend | Under the control bar: teal dot + "{current range}" and dark-teal dot + "{previous range}" (format `{Mon D, YYYY} – {Mon D, YYYY}`) |
| KPI cards | A small line under each value: `vs {previous value}` (no percentage change is shown on this page) |
| Chart | Title gets the label **(Current vs Previous)**. Two extra **orange dotted** lines are drawn: **Clicks (prev)** and **Impressions (prev)**. The legend lists all four series |
| Tables | Every metric column header gets the subtitle **(Current vs Previous)**. Each metric cell shows the current value and, below it, `vs {previous value}`. Applies to all four tabs |

---

## 5. Section details

### 5.1 KPI cards
Four equal cards in one row, each with an uppercase label (top-left), a small teal icon (top-right) and a large bold value. The cards have **no ⓘ tooltip**.

| Card | Icon | Value format | Meaning |
|---|---|---|---|
| **TOTAL CLICKS** | Mouse-pointer click | `{n}` | Sum of GSC clicks in the range |
| **TOTAL IMPRESSIONS** | Eye | `{n,nnn}` (thousands separator) | Sum of GSC impressions |
| **AVG CTR** | Percent sign | `{n.nn}%` | Clicks ÷ impressions over the range |
| **AVG POSITION** | Trend-up arrow | `{n.n}` | Average search position (lower is better) |

### 5.2 Clicks & Impressions Over Time
| Property | Details |
|---|---|
| Type | Smooth **dual-axis line chart** |
| Series | **Clicks** (teal line, left axis) and **Impressions** (grey line, right axis) |
| X axis | Dates in `YYYY-MM-DD`, every second day labelled |
| Y axes | Left: clicks (integer ticks). Right: impressions (integer ticks) |
| Legend | Below the chart: "Clicks", "Impressions" (+ "Clicks (prev)", "Impressions (prev)" in compare mode) |
| Hover | Tooltip: `{YYYY-MM-DD}` then `Clicks : {n}` and `Impressions : {n}` |

### 5.3 Breakdown card

**Tabs** (segmented control): **Top Queries** (default) · **Top Pages** · **Devices** · **Countries**. Switching a tab changes the table, the search box placeholder and the filter row; the KPI cards and chart do not change.

**Common table behaviour**
- Header row is dark with muted text; metric columns are right-aligned.
- Body scrolls vertically inside a box of max height 480 px; header stays visible.
- Rows are ordered by clicks, highest first (as returned by the data call). **Column headers are not sortable**.
- Rows are not clickable.
- Numbers use thousands separators; CTR as `{n.nn}%`; Position with one decimal.

| Tab | Columns | Rows | Search box placeholder | Extra controls |
|---|---|---|---|---|
| **Top Queries** | **Query** · **Clicks** · **Impressions** · **CTR** · **Position** | All search queries returned by GSC for the range (`{n}`) | "Search query…" | Branded filter (below) |
| **Top Pages** | **Page** (full URL) · **Clicks** · **Impressions** · **CTR** · **Position** | One row per page | "Search page…" | None |
| **Devices** | **Device** · **Clicks** · **Impressions** · **CTR** · **Position** | 3 rows: `DESKTOP`, `MOBILE`, `TABLET` (uppercase) | "Search device…" | None |
| **Countries** | **Country** · **Clicks** · **Impressions** · **CTR** · **Position** | One row per country, shown as a lowercase 3-letter code (e.g. `ind`, `gbr`, `usa`) | "Search country…" | None |

**Search box** (all tabs)
| Element | Details |
|---|---|
| Control | Left of the filter row. Magnifier icon + placeholder text per tab |
| Behaviour | Filters rows live by text contained in the first column |
| No match | Message **No query match "{text}"** on Top Queries, **No page match "{text}"** on Top Pages, **No device match "{text}"** on Devices and **No country match "{text}"** on Countries |

**Branded filter** (Top Queries tab only)
| Element | Details |
|---|---|
| Control | Segmented radio group, right side: **All** (default, active = teal) · **Branded ({n})** · **Non-branded ({n})**. Counts show the number of queries in each group; All = Branded + Non-branded |
| Behaviour | Filters the Queries table to branded queries (those containing the brand name, variants, misspellings or products), non-branded queries, or all |
| **ⓘ "About branded queries"** | Icon button next to the filter. Hover tooltip: "Branded = queries that include your brand name, variations, misspellings or products. Classification is AI-assisted, like Google Search Console, and may occasionally be wrong." |

---

## 6. UI element inventory

### Buttons, dropdowns and toggles
| Element | Location | Type |
|---|---|---|
| Start / End | Control bar | Single-month calendar popovers |
| Compare Start / Compare End | Control bar (compare on) | Same calendar popovers |
| Compare | Control bar | Toggle switch |
| Refresh | Control bar | Button |
| Top Queries / Top Pages / Devices / Countries | Breakdown card | Tabs |
| All / Branded / Non-branded | Top Queries tab | Radio segmented control |
| ⓘ About branded queries | Top Queries tab | Tooltip icon (the only ⓘ on the page) |
| Search box | Breakdown card | Text input (placeholder changes per tab) |

### Not present on this page
Date preset dropdown, pagination, export or download, column sorting, row click-through, KPI tooltips.

### Badges and labels
| Label | Where | Meaning |
|---|---|---|
| "Property: {GSC property}" | Control bar, right | Data source property |
| "(Current vs Previous)" | Chart title and column headers in compare mode | Both periods shown |
| "Clicks (prev)" / "Impressions (prev)" | Chart legend in compare mode | Previous-period series |
| "vs {value}" | KPI cards and table cells in compare mode | Previous-period value |

### Status and empty states
| Message | Where |
|---|---|
| No query / page / device / country match "{text}" | Table when the search finds nothing (one message per tab) |
| Red-bordered toast **"Edge Function returned a non-2xx status code"** (bottom-right, with an exclamation icon) | Shown when the data call fails, e.g. after choosing a date range the service rejects. The previous numbers stay on screen |
| Skeleton placeholders | During loading |

---

## 7. Data sources and API calls

| Data block | Call | Input |
|---|---|---|
| KPI cards, chart, all four tables | `POST fetch-search-console-data` | `{ "brand": "{Brand}", "startDate": "{YYYY-MM-DD}", "endDate": "{YYYY-MM-DD}" }` (called again for the compare range) |
| Brand lookup | `GET brands` (select `id`, filter `name ilike {Brand}`, limit 1) | Brand name |
| Branded / non-branded split and counts | `POST classify-branded-queries` | `{ "brand": "{Brand}", "queries": [ "{query 1}", "{query 2}", … ] }` (all queries from the fetch above) |
| Usage tracking | `POST user_page_sessions` | `page_path: "/analytics/console-insights"`, `page_label: "Console Insights"`, `user_id` |

Shell calls (roles, subscription, notifications) are listed in [00-global-layout.md](00-global-layout.md) section 5. The page's internal name is "Console Insights" (route and usage label), while the sidebar and title say "Search Console".

---

## 8. Behaviour rules

- **Brand scoped:** data is for the brand selected in the top bar; the GSC property is the one connected for that brand.
- **Reporting lag:** GSC data is ~2 days behind, so the default end date is today minus 2 days.
- **Date change:** changing Start, End, Compare dates, or pressing Refresh re-calls the GSC fetch; the branded classification is re-run for the returned queries.
- **KPI maths:** CTR = clicks ÷ impressions; position is the average position reported by GSC.
- **Tabs and filters:** the branded filter exists only on Top Queries; search text is per tab.
- **Compare mode:** shows previous-period values only as `vs {value}`; there is no percentage-change arrow on this page.
- **Classification accuracy:** branded/non-branded is AI-assisted and may occasionally be wrong (stated in the tooltip).
- **Date validation:** there is no client-side check between Start and End. Choosing a Start date after the End date (or an End date before the Start) is accepted by the pickers, the data call is made, the error toast above appears and the KPI numbers and chart keep their previous values.
