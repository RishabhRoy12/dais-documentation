# Analytics → Local Listings

| | |
|---|---|
| **Route** | `/analytics/local-listings` |
| **Page title** | Local Listings |
| **Subtitle** | None |
| **Breadcrumb** | DareAISearch › {Brand} › Analytics › Local Listings |
| **Sidebar location** | ANALYTICS group → Local Listings (shown only for brands that have the page enabled; see [00-global-layout.md](00-global-layout.md) section 6) |
| **Shared shell** | Top bar, sidebar, breadcrumb and the Miss Daring assistant are documented in [00-global-layout.md](00-global-layout.md) |

> Documented from the live app, using a brand that has local-listing data (populated state) and a brand that has none (empty state). This page is documented on its own; how its data connects to other pages is left for a later pass. All numbers and months are **placeholders such as `{n}`**, because they depend on the brand. Text in quotes is exact on-screen text.
>
> **Limitation:** the populated brand had **0 posts** (only reviews). The layout used to list individual **posts**, if the page has one, was therefore not visible and is not documented.

---

## 1. Purpose

Summarises the brand's **local listing** activity (reviews, posts, impressions) by month, from the team's **tracking sheet**, with a generated insight sentence.

This page has **no ⓘ tooltips, no tables, no charts, no search box and no Recommended Actions**.

---

## 2. Page sections (top to bottom)

| # | Section | Contents |
|---|---|---|
| 1 | Page title | "Local Listings" (no subtitle) |
| 2 | Summary card | Five metrics and a month dropdown |
| 3 | Insight line (BETA) | One generated sentence |
| – | Empty state | Replaces sections 2–3 when the brand has no listing data |

---

## 3. Section details

### 3.1 Summary card
One rounded card with five metrics side by side (small uppercase label above a large number) and a dropdown on the right.

| Metric | Meaning |
|---|---|
| **TOTAL POSTS** | Number of local listing posts in the selected period |
| **TOTAL REVIEWS** | Number of reviews in the selected period |
| **IMPRESSIONS** | Total impressions of the listing in the selected period |
| **MONTHS TRACKED** | Number of months with data included in the selection (7 for "All Months", 1 for a single month) |
| **AVERAGE REVIEWS** | Average reviews per tracked month, one decimal (`{n.n}`) |

**Month dropdown**
| Property | Details |
|---|---|
| Default | **All Months** |
| Options | **All Months** and then one entry per month with data, shown as the month name only (**January**, **February** … **July**) |
| Effect | Recalculates the five metrics and the insight sentence for that month |

### 3.2 Insight line
- Sparkle icon, one generated sentence, **BETA** pill.
- Pattern: "{n} reviews across {n} month(s) ({n.n} avg) — emerging social proof that strengthens brand trust in AI-generated local recommendations."
- It changes with the month dropdown (for a single month the wording is "… across 1 month …").

### 3.3 Empty state
Shown when the brand has no local-listing data:

| Element | Details |
|---|---|
| Icon | Map-pin icon in teal inside a dark teal circle |
| Heading | **No Listings Yet** |
| Message | "Local listing data will appear here once posts are added to the tracking sheet." |

---

## 4. UI element inventory

### Buttons, dropdowns and toggles
| Element | Location | Type |
|---|---|---|
| Month dropdown ("All Months") | Summary card | Dropdown |

### Not present on this page
Search box, filters other than the month dropdown, tabs, tables, charts, pagination, export or download, ⓘ tooltips, Recommended Actions.

### Badges and labels
| Label | Where | Meaning |
|---|---|---|
| **BETA** | Insight line | Generated/beta feature |
| TOTAL POSTS / TOTAL REVIEWS / IMPRESSIONS / MONTHS TRACKED / AVERAGE REVIEWS | Summary card | Metric labels |

### Status and empty states
| Message | Where |
|---|---|
| "No Listings Yet" + "Local listing data will appear here once posts are added to the tracking sheet." | Whole page, when no data exists |

---

## 5. Data sources and API calls

| Data block | Call | Input |
|---|---|---|
| Summary card, month list, insight sentence | `POST fetch-local-listings` | `{}` for the signed-in brand, or `{ "brandOverride": "{Brand}" }` when a brand is selected in the switcher (the month filter was applied without an extra call) |
| Usage tracking | `POST user_page_sessions` | `page_path: "/analytics/local-listings"`, `user_id` |

Shell calls (roles, subscription, notifications) are listed in [00-global-layout.md](00-global-layout.md) section 5.

---

## 6. Behaviour rules

- **Brand scoped:** data is for the brand selected in the top bar; the page is available only to brands that have it enabled.
- **Empty until tracked:** content appears only after the brand's local-listing data is added to the tracking sheet.
- **Month selection** recalculates all five metrics and the insight sentence; months are listed by name only (the year is not shown).
