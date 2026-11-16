# Analytics → Product Leaderboard

| | |
|---|---|
| **Route** | `/analytics/product-leaderboard` |
| **Page title (on screen)** | ChatGPT Shopping Leaderboard |
| **Name in sidebar and breadcrumb** | Product Leaderboard |
| **Subtitle** | None |
| **Breadcrumb** | DareAISearch › {Brand} › Analytics › Product Leaderboard |
| **Sidebar location** | ANALYTICS group → Product Leaderboard (shown only for brands that have the page enabled; see [00-global-layout.md](00-global-layout.md) section 6) |
| **Shared shell** | Top bar, sidebar, breadcrumb and the Miss Daring assistant are documented in [00-global-layout.md](00-global-layout.md) |

> Documented from the live app, using a brand that has leaderboard data (populated state) and a brand that has none (empty state). This page is documented on its own; how its data connects to other pages is left for a later pass. All numbers, product names and dates are **placeholders such as `{n}`**, because they depend on the brand. Text in quotes is exact on-screen text.

---

## 1. Purpose

Shows where the brand and its products appear in **ChatGPT Shopping** results: a week-by-week rank grid for the brand and every product that has ever been ranked, with summary numbers for the latest scan.

This page has **no ⓘ tooltips, no filters, no search box, no AI insight line and no Recommended Actions**.

---

## 2. Page sections (top to bottom)

| # | Section | Contents |
|---|---|---|
| 1 | Page title | "ChatGPT Shopping Leaderboard" (no subtitle) |
| 2 | Summary card | Five metrics |
| 3 | Rank grid | Product × weekly-date table |
| – | Empty state | Replaces sections 2–3 when the brand has no data |

---

## 3. Section details

### 3.1 Summary card
One rounded card with five metrics side by side, each a small uppercase label above a large number.

| Metric | Value |
|---|---|
| **TOTAL PRODUCTS** | Number of rows in the grid (brand row + products ever ranked) |
| **RANKED (LATEST)** | Number of rows that have a rank in the **latest** scan date |
| **TOP 3** | How many of those have rank 1–3 in the latest scan |
| **TOP 5** | How many have rank 1–5 in the latest scan (shown in teal) |
| **AVG RANK** | Average of the ranks present in the latest scan, one decimal |

### 3.2 Rank grid
| Column | Description |
|---|---|
| **Product Name** | Name of the brand (first row) or product, bold, wraps over lines when long |
| **{D Mon YYYY}** (one column per scan date) | Weekly scan dates, newest first (42 dates in the sampled brand), shown in two or three short lines (`7 Nov` / `2026`). All dates are always shown |

**Cell values**
| Display | Meaning |
|---|---|
| 🥇 **1**, 🥈 **2**, 🥉 **3** in a round highlighted chip | Rank 1, 2 or 3 in ChatGPT Shopping on that date (gold, silver, bronze medal beside the number) |
| **4**, **5** in a round dark chip | Rank 4 or 5 |
| Small grey number | Rank 6–10 |
| **-** (dimmed) | Not ranked on that date |

**Rows and behaviour**
- The first row is the **brand** itself; the following rows are products, those ranked in the latest scan first (best rank first), then products ranked only in earlier scans, then products that never ranked recently (all dashes).
- Header row is teal and stays at the top of its box when scrolling. The box scrolls **horizontally** (the grid is wider than the page); the page scrolls vertically over all 78 rows (no inner vertical scroll box).
- The Product Name column is not pinned while scrolling horizontally.
- Column headers are not sortable and not clickable; rows and cells are not clickable; no hover tooltip.

### 3.3 Empty state
Shown when the brand has no leaderboard data:

| Element | Details |
|---|---|
| Icon | Trophy icon in teal inside a dark teal circle |
| Heading | **No Leaderboard Data Yet** |
| Message | "Product leaderboard data will appear here once ranking data is available." |

---

## 4. UI element inventory

### Buttons, dropdowns and toggles
None on this page (apart from the shell controls).

### Not present on this page
Filters, date picker, search box, sorting, pagination, export or download, ⓘ tooltips, charts, AI insight line, Recommended Actions.

### Badges and labels
| Label | Where | Meaning |
|---|---|---|
| 🥇 🥈 🥉 | Rank cells | Medal for ranks 1–3 |
| **-** | Rank cells | Not ranked |
| TOTAL PRODUCTS / RANKED (LATEST) / TOP 3 / TOP 5 / AVG RANK | Summary card | Summary metrics |

### Status and empty states
| Message | Where |
|---|---|
| "No Leaderboard Data Yet" + "Product leaderboard data will appear here once ranking data is available." | Whole page, when no data exists |

---

## 5. Data sources and API calls

| Data block | Call | Input |
|---|---|---|
| Summary card and grid | `POST fetch-product-leaderboard` | `{}` for the signed-in brand, or `{ "brandOverride": "{Brand}" }` when a brand is selected in the switcher |
| Usage tracking | `POST user_page_sessions` | `page_path: "/analytics/product-leaderboard"`, `user_id` |

Shell calls (roles, subscription, notifications) are listed in [00-global-layout.md](00-global-layout.md) section 5. The page makes a single data call.

---

## 6. Behaviour rules

- **Brand scoped:** data is for the brand selected in the top bar; the page is available only to brands that have it enabled.
- **Summary maths** are all for the latest scan date (the first grid column): sample check: ranks 1, 5 and 9 give RANKED 3, TOP 3 = 1, TOP 5 = 2, AVG RANK = 5.0.
- **Dates** are the scan dates from the ranking data (weekly, with occasional extra dates).
- **Empty until ranked:** the empty state appears when the data call returns nothing.
