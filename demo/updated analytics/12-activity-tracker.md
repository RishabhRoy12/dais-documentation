# Analytics → Activity Tracker

| | |
|---|---|
| **Route** | `/analytics/activity` |
| **Page title** | Activity Tracker |
| **Subtitle** | None |
| **Breadcrumb** | DareAISearch › {Brand} › Analytics › Activity Tracker |
| **Sidebar location** | ANALYTICS group → Activity Tracker (12th item) |
| **Shared shell** | Top bar, sidebar, breadcrumb and the Miss Daring assistant are documented in [00-global-layout.md](00-global-layout.md) |

> Documented from the live app. This page is documented on its own; how its data connects to other pages is left for a later pass. All dates, brand names and counts are **placeholders such as `{n}`**, because they depend on the brand. Text in quotes is exact on-screen text.

---

## 1. Purpose

A read-only **activity feed** of the work the DareAISearch platform and team have done for the brand: monitoring, reporting, publishing, audits and recommendations, listed newest first with the date of each item.

This page has **no filters, no AI insight line, no Recommended Actions and no ⓘ tooltips**.

---

## 2. Page sections (top to bottom)

| # | Section | Contents |
|---|---|---|
| 1 | Page title | "Activity Tracker" (no subtitle) |
| 2 | Data-freshness banner | "Data as of {YYYY-MM-DD}" |
| 3 | Recent Activity card | Heading, subheading, scrolling list of activity items |

---

## 3. Section details

### 3.1 Data-freshness banner
A full-width, thin rounded bar with a clock icon and bold text: **"Data as of {YYYY-MM-DD}"**. It states the date of the most recent activity record loaded (not today's date).

### 3.2 Recent Activity
| Element | Details |
|---|---|
| Heading | Clock icon + **Recent Activity** (bold) |
| Subheading | "Latest updates and events" (grey) |
| List | Vertical list of rounded activity rows inside a box of max height **500 px** with its own vertical scroll (all items are loaded at once; 60 in the sampled brand) |

**Activity row**
| Part | Details |
|---|---|
| Status icon | Teal circle with a check mark (left). Every row shows this completed icon |
| Text | One sentence, always starting with **"DareAISearch {Team/Engine name}"** followed by what was done, e.g. "DareAISearch {Engine} {completed/published/optimized/...} {work description}." |
| Date | Right-aligned, ordinal short format **"{D(th) Mon, YYYY}"**, e.g. `{4th Aug, 2026}` |

- Rows are ordered **newest first** by date; several rows can share a date.
- The same sentence can appear on more than one date (recurring tasks such as weekly ranking tracking).
- Rows are plain text: not clickable, no hover tooltip, no links or buttons.

**Engine / team names seen in the sentences**
| Name in text | Type of work described |
|---|---|
| Insights | Weekly and monthly performance reports and snapshots, GA4 / Search Console analysis, off-page tracking sheets |
| Publisher | On-page and off-page work: META tags, H1 headings, image alt text, internal linking, tracking-sheet upkeep |
| Monitor | Tracking of AI prompt rankings and keyword ranking movements |
| Audit Engine | Technical and on-page website audits, fixes and data validation |
| Content Engine | Blog publishing validation and content recommendations |
| Recommendation Engine | On-page and local-profile optimisation recommendations |
| Platform QA | Validation and resolution of Search Console error signals |
| Schema | Structured-data and content-enhancement recommendations |
| Intelligence | Google Business Profile and YouTube opportunity analysis, keyword-cluster and prompt strategy |

---

## 4. UI element inventory

### Buttons, dropdowns and toggles
None on this page.

### Not present on this page
Date filters, search box, category filters, tabs, pagination or "load more", export or download, links, ⓘ tooltips, AI insight line, Recommended Actions.

### Badges and labels
| Label | Where | Meaning |
|---|---|---|
| "Data as of {YYYY-MM-DD}" | Banner | Date of the latest loaded activity |
| Teal check circle | Each row | Activity completed |
| "{D(th) Mon, YYYY}" | Right of each row | Date of the activity |
| "Latest updates and events" | Card subheading | Description of the list |

### Status and empty states
No empty-state text was captured, because the sampled brand has activity records.

---

## 5. Data sources and API calls

| Data block | Call | Input |
|---|---|---|
| Banner date and activity list | `POST fetch-activity-data` | `{}` (brand taken from the session) |
| Usage tracking | `POST user_page_sessions` | `page_path: "/analytics/activity"`, `user_id` |

Shell calls (roles, subscription, notifications) are listed in [00-global-layout.md](00-global-layout.md) section 5. The page makes a single data call.

---

## 6. Behaviour rules

- **Brand scoped:** the feed is for the brand selected in the top bar.
- **Order and range:** newest first; the list covers a rolling window of recent months (the sampled brand showed about two months, from `{D Mon YYYY}` to `{D Mon YYYY}`).
- **Freshness:** the banner date comes from the data, so it can be earlier than today if no newer activity has been recorded.
- **Read-only:** the page has no interaction other than scrolling the list.
