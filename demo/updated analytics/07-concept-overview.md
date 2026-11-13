# Analytics → Concept Overview

| | |
|---|---|
| **Route** | `/analytics/concepts` |
| **Page title** | Concept Overview |
| **Subtitle** | None |
| **Breadcrumb** | DareAISearch › {Brand} › Analytics › Concept Overview |
| **Sidebar location** | ANALYTICS group → Concept Overview (7th item) |
| **Shared shell** | Top bar, sidebar, breadcrumb and the Miss Daring assistant are documented in [00-global-layout.md](00-global-layout.md) |

> Documented from the live app. This page is documented on its own; how its data connects to other pages is left for a later pass. All numbers, concept names and brand names are **placeholders such as `{n}`**, because they depend on the brand. Text in quotes is exact on-screen text.

---

## 1. Purpose

Shows which **concepts** (topics such as manufacturing, certifications, ingredients) AI models associate with the brand, how often they are mentioned, and with what **sentiment** (positive, neutral, negative). A second table compares how often each concept is mentioned for the brand versus its competitors.

This page has **no AI insight line and no Recommended Actions**.

---

## 2. Page sections (top to bottom)

| # | Section | Contents |
|---|---|---|
| 1 | Page title | "Concept Overview" (no subtitle, no page-level date filter) |
| 2 | Model pill | A single teal pill labelled "ChatGPT" |
| 3 | Concepts Aggregated – ChatGPT | Month dropdown, sentiment key, concept table with bars |
| 4 | Concepts by Brand | Snapshot date label, model dropdown, concept × brand table |

---

## 3. Section details

### 3.1 Model pill
A single rounded teal button labelled **ChatGPT** under the title. It shows which model the first table covers. Clicking it does nothing (no menu, no switching), and there is no other option.

### 3.2 Concepts Aggregated – ChatGPT
Title with an **ⓘ** icon. **ⓘ tooltip:** "Aggregated concept mentions and sentiment analysis, showing how frequently key topics are discussed with positive, neutral, or negative sentiment."

| Element | Type | Details |
|---|---|---|
| **Month dropdown** | Dropdown beside the title, default = latest month (e.g. "July 2026") | Lists the months that have data, newest first (sample: July 2026, June 2026). Choosing a month reloads the table and changes the column header to "Mentions ({Month YYYY})" |
| **Sentiment key** | Top-right, three items: green-check circle **Sentiments Positive**, dark-teal circle **Sentiments Neutral**, red-check circle **Sentiments Negative** | Explains the bar colours |

**Table columns**
| Column | Description |
|---|---|
| **Concept** | Numbered row (`1.`, `2.` …) and the concept name. Names are **hierarchical paths joined by `__`**, from broad to specific, e.g. `{category}`, `{category}__{sub-category}`, `{category}__{sub-category}__{topic}`. Parent concepts and their children appear as separate rows |
| **Mentions ({Month YYYY})** | Total mentions of the concept in the month: number followed by a grey horizontal bar scaled to the largest value in the table |
| **Sentiments Positive** | Number of positive mentions + teal bar |
| **Sentiments Neutral** | Number of neutral mentions + dark-teal bar |
| **Sentiments Negative** | Number of negative mentions + bar (red per the key; an empty track when the value is 0, which was the case for every row in the three brands and several months checked) |

Mentions = Positive + Neutral + Negative.

**Table behaviour**
- Rows are ordered by Mentions, highest first, as returned by the data call.
- Bars sit on a faint full-width track; each bar's length is relative to the highest value in that column.
- The body scrolls vertically inside a box of max height 600 px; all rows are loaded at once.
- Footer text at bottom-right: **"1 - {n} / {n}"** (rows shown / total rows).
- Column headers are not sortable, rows are not clickable, and bars have no hover tooltip. No search box and no export.

### 3.3 Concepts by Brand
Title with an **ⓘ** icon and a small grey date label **"({YYYY-MM-DD})"** (the snapshot date of the data). **ⓘ tooltip:** "Mentions of each concept broken down by competing brand, per AI model. Source: SEMrush."

| Element | Type | Details |
|---|---|---|
| **Model dropdown** | Dropdown on the right, default **ChatGPT** | Options: **ChatGPT** · **Gemini**. Changes only this table (the first table and its title stay on ChatGPT) |

**Table columns**
| Column | Description |
|---|---|
| **Concept** | Top-level concept name (no `__` hierarchy here). Pinned to the left |
| **{Competitor 1} … {Competitor n}** | One column per competitor brand (names as tracked) |
| **{brand}** | The user's own brand as the **last** column, shown in lower case (e.g. `{brand name in lowercase}`) |

**Cell values**
| Value | Meaning |
|---|---|
| Number | Mentions of the concept for that brand in the selected model |
| `0` (dimmed grey) | No mentions |

**Table behaviour**
- Rows are ordered alphabetically by concept name. The set of concepts and the numbers differ between ChatGPT and Gemini (e.g. 12 rows for ChatGPT in the sample, a different list for Gemini).
- The first column is pinned; numeric columns are right-aligned.
- The box has a fixed height; there is no pagination, sorting, search box or export. Rows are not clickable.

---

## 4. UI element inventory

### Buttons, dropdowns and toggles
| Element | Location | Type |
|---|---|---|
| ChatGPT pill | Under the title | Static label styled as a button (no action) |
| Month dropdown ("{Month YYYY}") | Concepts Aggregated header | Dropdown |
| Model dropdown ("ChatGPT") | Concepts by Brand header | Dropdown (ChatGPT, Gemini) |
| ⓘ icons (2) | Both table titles | Hover tooltips (texts above) |

### Not present on this page
AI insight line, Recommended Actions, page-level date picker, Compare toggle, search boxes, column sorting, expandable rows, pagination controls, export or download.

### Badges and labels
| Label | Where | Meaning |
|---|---|---|
| Sentiments Positive / Neutral / Negative | Key and column headers | Sentiment categories (green / dark teal / red) |
| "Mentions ({Month YYYY})" | Column header | Month shown |
| "({YYYY-MM-DD})" | Concepts by Brand title | Snapshot date |
| "1 - {n} / {n}" | Table footer | Row count |

### Status and empty states
No dedicated empty-state text was seen. Zero values are shown as `0` (dimmed in the brand table, empty bar track in the sentiment columns).

---

## 5. Data sources and API calls

| Data block | Call | Input |
|---|---|---|
| Concepts Aggregated (concepts, mentions, sentiments, month list) | `POST fetch-concept-data` | `{}` on first load (latest month); `{ "month": "{YYYY-MM}" }` when the month is changed |
| Concepts by Brand | `POST fetch-concept-by-brand` | `{}`; the model switch is applied to the loaded data |
| Usage tracking | `POST user_page_sessions` | `page_path: "/analytics/concepts"`, `user_id` |

Shell calls (roles, subscription, notifications) are listed in [00-global-layout.md](00-global-layout.md) section 5. The Concepts by Brand table's tooltip names **SEMrush** as its source.

---

## 6. Behaviour rules

- **Brand scoped:** all data is for the brand selected in the top bar.
- **Independent controls:** the Month dropdown affects only Concepts Aggregated; the Model dropdown affects only Concepts by Brand. The first table is always ChatGPT.
- **Month change** triggers a new `fetch-concept-data` call, and the number of rows can change between months (sample: 17 rows in July vs 27 in June).
- **Concept hierarchy** is encoded in the name with `__` separators and is displayed as-is (not indented or collapsible).
- **Brand column:** the user's own brand is always the last column, and competitors are the ones tracked for the brand.
