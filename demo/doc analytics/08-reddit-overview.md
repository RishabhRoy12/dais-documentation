# Analytics → Reddit Overview

| | |
|---|---|
| **Route** | `/analytics/reddit-overview` |
| **Page title** | Reddit Overview |
| **Subtitle** | "Subreddit impact and trending Reddit threads for your brand" |
| **Breadcrumb** | DareAISearch › {Brand} › Analytics › Reddit Overview |
| **Sidebar location** | ANALYTICS group → Reddit Overview (8th item) |
| **Shared shell** | Top bar, sidebar, breadcrumb and the Miss Daring assistant are documented in [00-global-layout.md](00-global-layout.md) |

> Documented from the live app. This page is documented on its own; how its data connects to other pages is left for a later pass. All numbers, subreddit names, thread titles and dates are **placeholders such as `{n}`**, because they depend on the brand. Text in quotes is exact on-screen text.

---

## 1. Purpose

Shows which **Reddit communities (subreddits)** and **Reddit threads** AI models cite when answering the brand's tracked prompts, for a chosen AI model and scan date. It helps identify where Reddit conversations influence the brand's AI visibility.

This page has **no AI insight line, no Recommended Actions and no ⓘ tooltips**.

---

## 2. Page sections (top to bottom)

| # | Section | Contents |
|---|---|---|
| 1 | Page header | Breadcrumb, title, subtitle, model dropdown, scan-date dropdown |
| 2 | Subreddit Impact | Table of subreddits with bars |
| 3 | Threads | Table of Reddit threads |

---

## 3. Header controls

| Control | Type | Details |
|---|---|---|
| **Model dropdown** | Dropdown, default **ChatGPT** | Options: **ChatGPT** · **Gemini**. Switching reloads both tables for that model and resets the date to the latest available for it |
| **Scan-date dropdown** | Dropdown showing `{YYYY-MM-DD}`, default = latest scan date | Lists the scan dates that have data for the chosen model, newest first (sample: 15 dates for ChatGPT, fewer for Gemini). Choosing a date reloads both tables |

---

## 4. Section details

### 4.1 Subreddit Impact
Card with a chat-bubble icon and the title **"Subreddit Impact"**.

**Table columns**
| Column | Description |
|---|---|
| **Subreddit** | Subreddit name as `r/{name}` (or `r/u_{user}` for user profiles). Teal text, a link to the subreddit |
| **Link** | External-link icon; opens the same subreddit page |
| **Prompts ⇅** | Number of tracked prompts whose answers cite this subreddit. Shown as a **blue bar** with the number at the right end |
| **Visibility ⇅** | Share of the subreddit among all subreddit citations: **teal bar** with `{n.n}%` at the right end |
| **Threads ⇅** | Number of distinct threads from this subreddit. **Amber bar** with the number at the right end |
| **Citations ⇅** | Total citations of this subreddit. Plain number, right-aligned |

- Bar lengths are relative to the largest value in the column.
- Rows are listed in descending order of Prompts.
- All links open in a **new tab** (`target="_blank"`, `rel="noopener noreferrer"`).
- Column headers are buttons with a **⇅** icon. In testing, clicking them did **not** visibly change the row order (the table stays in descending order), so sorting should be treated as not effective.
- The body scrolls vertically inside a box of max height 560 px; the header stays visible.
- No search box, pagination or export. Bars have no hover tooltip.

**Empty state:** the centred message **"No subreddit data available yet."** is shown in place of the table when no data exists for the chosen model and date.

### 4.2 Threads
Card titled **"Threads"**.

**Table columns**
| Column | Description |
|---|---|
| **Thread** | Thread title in bold, or **—** when the title is not available |
| **Link** | External-link icon; opens the thread |
| **Thread URL** (sub-label "Click to open thread") | Orange Reddit **R** badge and the thread URL, truncated with "…". Teal link; opens the thread in a new tab |
| **Subreddit** | `r/{name}` of the thread (plain text) |
| **Prompts ⇅** | Number of tracked prompts whose answers cite the thread: blue bar with the number at the right end |

- Rows are listed in descending order of Prompts.
- The body scrolls vertically inside a box of max height 560 px; the header stays visible. Sort icon behaves as in 4.1.
- No search box, pagination or export.

---

## 5. UI element inventory

### Buttons and dropdowns
| Element | Location | Type |
|---|---|---|
| Model (ChatGPT / Gemini) | Header, right | Dropdown |
| Scan date (`{YYYY-MM-DD}`) | Header, right | Dropdown |
| Column headers with ⇅ | Both tables | Sort buttons (see 4.1) |
| Subreddit names and link icons | Both tables | External links (new tab) |
| Thread URLs and link icons | Threads table | External links (new tab) |

### Not present on this page
AI insight line, Recommended Actions, ⓘ tooltips, page-level date range picker, Compare toggle, search boxes, pagination, export or download.

### Badges and labels
| Label | Where | Meaning |
|---|---|---|
| Blue / teal / amber bars | Prompts / Visibility / Threads columns | Relative size of the value |
| Orange **R** badge | Thread URL cells | Reddit source marker |
| **—** | Thread column | No title available |
| "Click to open thread" | Thread URL header | Helper text |

### Status and empty states
| Message | Where |
|---|---|
| "No subreddit data available yet." | Subreddit Impact, when there is no data for the selected model and date |
| (no message seen) | Threads table: no empty-state text was captured, because every date tested had thread rows |

---

## 6. Data sources and API calls

| Data block | Call | Input |
|---|---|---|
| Both tables and the date list | `POST fetch-reddit-overview` | `{}` on first load (ChatGPT, latest date); `{ "model": "gemini-2.5-flash" }` when Gemini is chosen; `{ "model": "{model}", "date": "{YYYY-MM-DD}" }` when a date is chosen |
| Usage tracking | `POST user_page_sessions` | `page_path: "/analytics/reddit-overview"`, `user_id` |

Shell calls (roles, subscription, notifications) are listed in [00-global-layout.md](00-global-layout.md) section 5.

---

## 7. Behaviour rules

- **Brand scoped:** all data is for the brand selected in the top bar.
- **Model and date drive both tables.** Each combination triggers a new `fetch-reddit-overview` call.
- **Available dates differ per model**, so switching to Gemini can shorten the date list and reset the selected date.
- **Visibility %** is the subreddit's share of all subreddit citations for that scan (values add up to 100% across the subreddits shown).
- **Scan dates with no data** show the empty state in Subreddit Impact while the Threads table can still list rows from that date's data; in the sample, such a date (`{YYYY-MM-DD}`) showed "No subreddit data available yet." above a populated Threads table.
