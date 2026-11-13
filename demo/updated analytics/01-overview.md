# Analytics → Overview

| | |
|---|---|
| **Route** | `/analytics/overview` |
| **Page title** | Overview |
| **Subtitle** | Comprehensive analytics dashboard |
| **Breadcrumb** | DareAISearch › {Brand} › Analytics › Overview |
| **Sidebar location** | ANALYTICS group → Overview (first item) |
| **Shared shell** | Top bar, sidebar, breadcrumb and the Miss Daring assistant are documented in [00-global-layout.md](00-global-layout.md) |

> Documented from the live app. All numbers, page paths and platform names in this document are **placeholders such as `{n}`**, because every value depends on the selected brand and date range. Text in quotes is the exact on-screen text.

---

## 1. Purpose

A single-screen summary of website performance that combines:
- **AI Search traffic**: sessions referred by AI platforms (ChatGPT, Perplexity, Gemini and similar).
- **Organic traffic**: sessions from traditional search engines (Google, Bing, Yahoo and others), joined with Google Search Console metrics.
- **Week-wise ranking tables** for AI prompts and keywords.
- **Attribution tables** that show how AI-referred users were first discovered.

---

## 2. Page sections (top to bottom)

| # | Section | Contents |
|---|---|---|
| 1 | Page header | Breadcrumb, title, subtitle, Compare toggle, date preset, date range picker (+ second picker in compare mode) |
| 2 | KPI card "ANALYTICS (ORGANIC + AI SEARCH)" | 5 metric tiles |
| 3 | AI insight line (BETA) | One sentence on the top AI platform's share |
| 4 | Data-status banner | "No data collected yet" with two status chips |
| 5 | Analytics (AI Search) | Line chart, bar chart, session-source table, landing-page table, BETA summary line |
| 6 | Analytics (Organic Traffic) | Line chart, bar chart, session-source table, landing-page table with GSC columns, footnote, BETA summary line |
| 7 | Prompt Ranking Performance Week Wise | Engine toggle, date selector, weekly table |
| 8 | Keyword Ranking Performance Week Wise | Weekly tier table |
| 9 | AI Search Decision Table | Source attribution table |
| 10 | AI Search Discovery Table | First-user-source attribution table |

---

## 3. Header controls

| Control | Type | Behaviour |
|---|---|---|
| **Compare** | Toggle switch (off by default) with compare icon | Turns on comparison mode (see section 4) |
| **Date preset** | Dropdown (teal, filled). Default **Last 30 Days** | Options: **Last 7 Days** · **Last 15 Days** · **Last 30 Days** · **All Time**. Each sets the range ending today: 7 days = today−6 → today, 15 days = today−14 → today, 30 days = today−29 → today, All Time = Jan 1, 2023 → today |
| **Date range picker** | Button with calendar icon, label `{Mon D, YYYY} - {Mon D, YYYY}`, chevron | Opens a **two-month calendar popover** (current month and next month, weeks Su–Sa). Choosing a custom range sets the dates. Changing preset or dates reloads every data block |
| **Compare date picker** | Second picker, shown only when Compare is on, separated by the word **vs** | Default is the previous period of equal length (e.g. 30 days immediately before the current range) |
| **Period legend** | Two dots with date labels, shown under the title in compare mode | Teal dot = current period, dark-teal dot = previous period |

### Loading state
When data reloads (first load, preset change, compare on), the KPI card shows grey rounded **skeleton placeholders** (4 tiles, each with a number bar and a caption bar) and the chart areas show grey blocks.

---

## 4. Compare mode (Compare toggle on)

| Area | What changes |
|---|---|
| Header | Second date picker with "vs" appears, plus a two-item period legend |
| KPI tiles | Under each value: `vs {previous value} {↑ or ↓}{n}%` (for example `vs {n} ↓{n}%`). When both values are 0 the text is just `vs 0` |
| All tables with metrics (session source, landing page, Decision, Discovery) | Every metric column header gains the subtitle **(Current vs Previous)**. Each cell shows the current value and, below it, `vs {previous} {↑/↓}{n}%`. If the row did not exist in the previous period the cell shows `vs -`. The `↑`/`↓` percentage is the relative change between periods |
| Decision and Discovery tables | A **(Comparison Mode)** label appears beside the table title |
| Line charts | The date axis follows the selected ranges; tooltip lists the series name (**Current Period**) with its value |
| Unchanged | AI insight line, summary lines, Prompt Ranking table and Keyword Ranking table are not compared |

---

## 5. Section details

### 5.1 KPI card: "ANALYTICS (ORGANIC + AI SEARCH)"
Section label in uppercase small text. Four tiles, each with an icon, a large number and a caption with an **ⓘ** icon (hover shows a tooltip).

| Tile | Icon | Value | ⓘ tooltip text |
|---|---|---|---|
| **Active users** | People | `{n}` | "Total unique users who engaged with your website during the selected date range, including traffic from both traditional and AI search platforms." |
| **New users** | Person-plus | `{n}` | "Users visiting your website for the first time within the selected date range." |
| **Sessions** | Pulse line | `{n}` | "Total number of sessions initiated by users during this period, including repeat visits." |
| **Key events** | Target | `{n}` (0 when no conversion event is configured or fired in GA4) | "Important conversion actions tracked on your website, such as form submissions or purchases." |

### 5.2 AI insight line
- Sparkle icon, text, and a **BETA** pill.
- Text pattern: **"{platform} accounts for {pct}% of AI Search traffic during this period."**
- Logic: top AI platform's sessions ÷ total AI-referred sessions.

### 5.3 Data-status banner
Information banner with a clock icon.

| Part | Text |
|---|---|
| Title (bold) | No data collected yet |
| Chip 1 | Website analytics: {Collected / Not collected} |
| Chip 2 | Keyword ranking: {Collected / Not collected} |

### 5.4 Analytics (AI Search)
Title with a teal accent bar and ⓘ.
**ⓘ tooltip:** "Traffic and engagement metrics from AI-powered search platforms like ChatGPT, Perplexity, and Claude directing users to your website."

**Charts (side by side)**
| Chart | Type | Axes / data | ⓘ tooltip | Hover |
|---|---|---|---|---|
| **Active Users by time** | Smooth line chart with point markers | X: dates (`MM/DD`, every 3rd day labelled). Y: active users per day (integer ticks). Series: AI-referred traffic | "Trend of user engagement from AI search platforms over the selected date range." | Tooltip: `{MM/DD}` and `Current Period : {n}` |
| **Total Sessions by AI Search Platforms** | Horizontal bar chart with value label at bar end | Y: platform domain (e.g. `{platform}.com`). X: sessions (0 to rounded max). Bars in teal shades | "Breakdown of website sessions originating from AI-powered search platforms such as ChatGPT, Perplexity, and Claude." | Tooltip: `{domain} | sessions : {n}` |

**Table: Session source** (teal header, rows separated by lines, bold teal footer)
| Column | Description |
|---|---|
| Session source | AI platform domain |
| Active users | Active users from that source |
| New users | New users from that source |
| Sessions | Sessions from that source |
| Bounce rate | Share of non-engaged sessions, shown as `{n.n}%` |
| Key events | Key events from that source |

Footer row **Total**: sums of the columns above; bounce rate is the total-level figure shown with two decimals (`{n.nn}%`). This table is not scrollable and has no search box.

**Table: Landing Page Wise Performance - AI Search Traffic** (title has ⓘ)
ⓘ tooltip: "Individual landing pages receiving traffic from AI search platforms. When admin views Decode Age, matching pages are enriched with Google Search Console metrics (Clicks, Impressions, CTR, Position) for the same date range."

| Element | Details |
|---|---|
| Search box | Right of the title. Magnifier icon, placeholder **"Search landing pages..."**, an **✕** clear button appears when text is entered |
| Columns | **#** (row number `1.`, `2.` …) · **Landing page** (URL path) · **Active users** · **New users** · **Sessions** · **Key events** |
| **NEW** tag | Small teal pill before the path: the page received AI traffic in this period but not in the previous period |
| `(not set)` | Landing page value when GA4 has no page for the session |
| Scrolling | Body scrolls vertically inside a box of max height 400 px; header row and **Grand total** row stay pinned |
| Footer | **Grand total** row (sums) |
| Search behaviour | Filters rows by text contained in the landing-page path. A row **"Search total ({n} results)"** with the sums for matching rows appears above the Grand total. With no match it shows "Search total (0 results)" with all zeros. Clearing the box restores all rows |
| Key events cell | Rendered as a teal value (link style) |

**Summary line (BETA):** "AI Search drives {pct}% of total sessions, with {n} active users across {n} platforms." with a BETA pill.

### 5.5 Analytics (Organic Traffic)
**ⓘ tooltip:** "Website traffic from traditional organic search engines like Google, Bing, and Yahoo during the selected period."

**Charts**
| Chart | Type | Axes / data | ⓘ tooltip |
|---|---|---|---|
| **Sessions over time** | Smooth line chart | X: dates (`MM/DD`, every 2nd day). Y: sessions per day | "Daily session volume from organic search traffic over the selected date range." |
| **Sessions by source** | Horizontal bar chart with value labels | Y: search-engine domain (`google`, `bing`, `{engine}.search.yahoo.com` …). X: sessions | "Distribution of organic sessions across different traffic sources and channels." |

**Table: Session source** — same columns, footer and behaviour as 5.4 (Session source · Active users · New users · Sessions · Bounce rate · Key events · **Total** row), with organic sources as rows.

**Table: Landing Page Wise Performance - Organic Search Traffic**
| Element | Details |
|---|---|
| Title row | Title + ⓘ + green pill **"GSC matched {matched}/{total}"** + second ⓘ + search box |
| Title ⓘ tooltip | Same text as the AI landing-page table: "Individual landing pages receiving organic search traffic. When admin views Decode Age, matching pages are enriched with Google Search Console metrics (Clicks, Impressions, CTR, Position) for the same date range." |
| "GSC matched" pill ⓘ tooltip | "Google Search Console data has a ~2-day reporting lag. The GSC columns reflect data up to 2 days before the selected end date; GA4 columns reflect the full selected range." |
| Search box | Same component and behaviour as 5.4 |
| Columns (GA4) | **#** · **Landing page** · **Active users** · **New users** · **Sessions** · **Key events** |
| Columns (Search Console) | **Clicks** (with small **GSC** badge in the header) · **Impressions** (thousands separators, e.g. `1,234`) · **CTR** (`{n.nn}%`) · **Position** (average, one decimal) |
| **NEW** tag | Page received organic traffic in this period but not in the previous one |
| Missing GSC data | Cells show **—** when the page is not found in Search Console |
| Scrolling | Max height 400 px, vertical scroll, header and Grand total pinned |
| Footer | **Grand total** (sums for counts; CTR is the overall ratio; Position shows **—**) |
| Footnote | "— = page not found in Search Console for this period." |

**Summary line (BETA):** "{source} accounts for {pct}% of organic sessions with a {n.n}% bounce rate."

### 5.6 Prompt Ranking Performance Week Wise
| Element | Type | Details |
|---|---|---|
| Title | Heading with ⓘ. Pattern: **"Prompt Ranking Performance Week Wise ({Engine})"** | Engine name updates with the toggle |
| ⓘ tooltip | | "Daily tracking of your brand's ranking position across key AI prompts, showing visibility trends over time." |
| **Date selector** | Multi-select dropdown button, label **"{n} of {total} dates"** (default all selected) | Menu: **Select All** · **Deselect All** · one checkbox row per weekly snapshot date (`DD-Mon-YYYY`, newest first). The table shows only checked dates. At least one date always stays selected (Deselect All leaves 1) |
| **Engine toggle** | Two tab buttons: **ChatGPT** (default, active = teal) · **Gemini** | Switches the engine whose data is shown; the heading and table values change |

**Table**
| Column | Description |
|---|---|
| **Particulars** | Row label |
| One column per selected date | `DD-Mon-YYYY`, weekly (7-day step), newest first, centred values |

**Rows:** **1. Ranked Prompts**: the number of prompts in which the brand was ranked for that week and engine.
The table is wider than the card, so it **scrolls horizontally**; the first column is not pinned. There is no search box.

### 5.7 Keyword Ranking Performance Week Wise
Title has ⓘ. **ⓘ tooltip:** "Weekly snapshot of your keyword positions across search engines, grouped by ranking tiers (Top 5, 10, 20, 50, 100)."

| Column | Description |
|---|---|
| **Keyword Ranking** | Ranking tier label |
| One column per weekly snapshot | Date label in long format, e.g. `{DD Month YYYY}`, newest first. Only the snapshots available for the brand are shown (a short list, no date selector) |

| Row | Meaning |
|---|---|
| 1. Top 5 | Number of tracked keywords ranking in positions 1–5 |
| 2. Top 10 | …positions 1–10 |
| 3. Top 20 | …positions 1–20 |
| 4. Top 50 | …positions 1–50 |
| 5. Top 100 | …positions 1–100 |

Tiers are cumulative, so values never decrease from Top 5 down to Top 100. Header row is teal, tier labels are bold and left-aligned.

### 5.8 AI Search Decision Table
Title has ⓘ. **ⓘ tooltip:** "Attribution analysis showing which AI platforms are driving sessions and converting users, helping identify high-value decision-making channels."

| Column | Description |
|---|---|
| Session Source | AI platform that the session came from |
| First User Source | Platform that first acquired the user (same as the session source in this table) |
| Sessions | Sessions |
| Total Users | Total users |
| New Users | New users |

Rows: one per AI platform. Footer **Total** row (First User Source shows **-**). In compare mode: see section 4.

### 5.9 AI Search Discovery Table
Title has ⓘ. **ⓘ tooltip:** "Shows how users initially discovered your brand via AI search platforms, attributing traffic by first user source to measure AI-driven brand awareness."

Columns are the same as the Decision table (**Session Source · First User Source · Sessions · Total Users · New Users**).

Difference: it also includes rows where the **session source is a different channel** (for example `google`) but the **first user source** was an AI platform, i.e. users who discovered the brand through AI and returned later through another channel. Its Total therefore equals or exceeds the Decision table total. Footer **Total** row (First User Source shows **-**). In compare mode: see section 4.

---

## 6. UI element inventory

### Buttons, dropdowns and toggles
| Element | Location | Type |
|---|---|---|
| Compare | Header | Toggle switch |
| Date preset | Header | Dropdown (Last 7 / 15 / 30 Days, All Time) |
| Date range | Header | Calendar popover (two months) |
| Compare date range | Header (compare mode) | Calendar popover |
| Search landing pages | AI and Organic landing tables | Text search with clear button |
| "{n} of {total} dates" | Prompt Ranking block | Multi-select dropdown with Select All / Deselect All |
| ChatGPT / Gemini | Prompt Ranking block | Two-way toggle (tabs) |
| ⓘ icons (16 on this page) | Section titles, chart titles, KPI captions, GSC pill | Hover tooltips (texts listed above) |

### Not present on this page
Tabs (other than the engine toggle), column sorting (table headers are not clickable), pagination, export or download buttons, row click-through.

### Badges and labels
| Label | Where | Meaning |
|---|---|---|
| **BETA** | AI insight line, both summary lines | Feature in beta |
| **NEW** | Landing-page rows | First appearance in the selected period vs the previous period |
| **GSC** (small badge) | "Clicks" column header | Value comes from Google Search Console |
| **GSC matched {a}/{b}** | Organic landing table title | `a` of `b` landing pages found in Search Console |
| **Total / Grand total / Search total** | Table footers | Aggregates |
| **(Current vs Previous)** | Column headers in compare mode | Cell shows both periods |
| **(Comparison Mode)** | Decision and Discovery titles in compare mode | |

### Status and empty states
| Message | Where |
|---|---|
| "No data collected yet", "Website analytics: …", "Keyword ranking: …" | Information banner |
| "Search total (0 results)" with zero values | Landing tables when the search matches nothing |
| "— = page not found in Search Console for this period." | Organic landing table footnote |
| `vs -` | Compare mode, no previous-period value |
| Skeleton placeholders | While data loads |

### Themes
Dark (default) and light, via the top-bar switch; all charts, tables and banners restyle.

---

## 7. Data sources and API calls

| Data block | Call | Input |
|---|---|---|
| KPI card, AI Search charts and tables, Organic charts and tables, Decision and Discovery tables | `POST FN fetch-ga4-analytics` | `startDate`, `endDate` (called again for the compare range) |
| Organic landing-page Clicks, Impressions, CTR, Position and "GSC matched" | `POST FN fetch-search-console-data` | `brand`, `startDate`, `endDate`, `rowLimit` |
| Prompt Ranking Performance Week Wise | `POST FN fetch-prompt-weekly-summary` | engine and brand context |
| Keyword Ranking Performance Week Wise | `POST FN fetch-keywords-ranking` | brand context |
| Shell (roles, subscription, notifications) | See [00-global-layout.md](00-global-layout.md) section 5 | |

All calls return HTTP 200 on a normal load and run in parallel on page open and on every date change.

---

## 8. Behaviour rules

- **AI source classification:** GA4 sessions whose source is an AI platform domain (for example chatgpt.com, perplexity.ai, gemini.google.com) belong to the AI Search blocks; sessions from search engines belong to the Organic blocks.
- **Percent share:** insight % = top platform sessions ÷ total AI sessions; AI summary % = AI sessions ÷ total sessions; organic insight % = top organic source sessions ÷ total organic sessions.
- **GA4 vs GSC join:** organic landing pages from GA4 are matched to Search Console pages by path; unmatched pages show **—**. GSC data lags about 2 days, so GSC columns end 2 days before the selected end date while GA4 columns cover the full range.
- **NEW flag:** computed against the previous period of equal length.
- **Key events = 0:** no conversion events configured or fired in GA4.
- **Google not connected:** GA4 and GSC blocks would have no data (inferred from the Google connection requirement).
- **Role-dependent data:** both landing-page tooltips state that Search Console enrichment applies when an admin views the page; the user's SEO Team membership is checked on load through `rpc/is_seo_team_member`.
- **Date reload:** any change to preset, date range, compare toggle or compare range reloads all GA4 and GSC blocks. The engine toggle and the date selector affect only the Prompt Ranking block.
