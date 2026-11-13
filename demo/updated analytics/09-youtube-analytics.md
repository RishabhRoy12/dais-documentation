# Analytics → YouTube Analytics

| | |
|---|---|
| **Route** | `/analytics/youtube` |
| **Page title** | YouTube Analytics |
| **Subtitle** | None |
| **Breadcrumb** | DareAISearch › {Brand} › Analytics › YouTube Analytics |
| **Sidebar location** | ANALYTICS group → YouTube Analytics (shown only for brands that have the page enabled; see [00-global-layout.md](00-global-layout.md) section 6) |
| **Shared shell** | Top bar, sidebar, breadcrumb and the Miss Daring assistant are documented in [00-global-layout.md](00-global-layout.md) |

> Documented from the live app, using a brand that has videos (populated state) and a brand that has none (empty state). This page is documented on its own; how its data connects to other pages is left for a later pass. All numbers, video titles and dates are **placeholders such as `{n}`**, because they depend on the brand. Text in quotes is exact on-screen text.

---

## 1. Purpose

Shows the YouTube videos tracked for the brand (long videos and Shorts), with an SEO score for each video, for a chosen month. Videos come from the team's **tracking sheet**.

This page has **no ⓘ tooltips** and no tables or charts.

---

## 2. Page sections (top to bottom)

| # | Section | Contents |
|---|---|---|
| 1 | Page title | "YouTube Analytics" (no subtitle) |
| 2 | Summary card | Total Videos, Shorts, month dropdown |
| 3 | Insight lines (BETA) | Two generated sentences |
| 4 | Video grid | Two-column grid of video cards |
| – | Empty state | Replaces sections 2–4 when the brand has no videos |

---

## 3. Section details

### 3.1 Summary card
A full-width rounded card.

| Element | Details |
|---|---|
| **TOTAL VIDEOS** | Small uppercase label with a large number: count of tracked videos for the selected month (long videos + Shorts) |
| **SHORTS** | Label with a large number: how many of them are Shorts |
| **Month dropdown** | Right side, default **All Months**. Options: **All Months** and one entry per month that has videos, newest first, in the short form `{Mon YY}` (e.g. `{Oct 26}`, `{Sep 26}` … `{Jan 26}`). Choosing a month reloads the data and updates the two numbers |

### 3.2 Insight lines
Two lines under the summary card, each with a sparkle icon, a generated sentence and a **BETA** pill:
1. A format-mix sentence, pattern "{n}% of content leverages Video format, aligning with YouTube's push toward short-form discovery."
2. A topical sentence about the themes of the content, pattern "Content spans {theme} — building topical authority across {audience/vertical}."

The sentences are generated text and do **not** change when the month is changed.

### 3.3 Video grid
Cards in **two columns** (one column on narrow screens), newest month first; within a month long videos are listed before Shorts. All cards are on the page (no pagination, no "load more"); the page itself scrolls.

**Video card**
| Part | Details |
|---|---|
| Thumbnail | Large image (YouTube thumbnail), full card width, about 16:9. Clicking it opens the video on YouTube in a **new tab** |
| Title | Bold video title |
| Type badge | Pill **Video** or **Shorts** |
| Month badge | Pill with the month, `{Mon YY}` (e.g. `{Oct 26}`) |
| **ORIGINAL SEO SCORE** | Small uppercase label; below it a number (SEO score of the original video metadata, 0–100) or **—** when no score exists. Shorts show **—** |
| **OPTIMIZED SEO SCORE** | Same format for the optimised metadata (teal **—** when not yet available) |
| **Watch on YouTube** | Grey link with an external-link icon at the bottom; opens the video in a new tab |

**Month filter behaviour (as observed):** choosing a month changes the TOTAL VIDEOS and SHORTS numbers to that month's counts (e.g. "4" and "2"), but in testing the grid below did **not** reduce to those videos: it showed 11 cards from several months. Treat the grid as not filtered by the month dropdown.

### 3.4 Empty state
Shown when the brand has no tracked videos instead of the summary card and grid:

| Element | Details |
|---|---|
| Icon | Video-player icon in teal inside a dark teal circle |
| Heading | **No Videos Yet** |
| Message | "YouTube video data will appear here once videos are added to the tracking sheet." |

---

## 4. UI element inventory

### Buttons, dropdowns and toggles
| Element | Location | Type |
|---|---|---|
| Month dropdown ("All Months") | Summary card | Dropdown |
| Thumbnail | Video card | Link to YouTube (new tab) |
| Watch on YouTube | Video card | Link to YouTube (new tab) |

### Not present on this page
Search box, sorting, tabs, pagination, export or download, ⓘ tooltips, tables, charts, Recommended Actions.

### Badges and labels
| Label | Where | Meaning |
|---|---|---|
| **BETA** | Both insight lines | Generated/beta feature |
| **Video** / **Shorts** | Card badge | Content type |
| `{Mon YY}` | Card badge and dropdown | Month of the video |
| **ORIGINAL SEO SCORE** / **OPTIMIZED SEO SCORE** | Card | SEO score before and after optimisation |
| **—** | Score fields | No score available |

### Status and empty states
| Message | Where |
|---|---|
| "No Videos Yet" + "YouTube video data will appear here once videos are added to the tracking sheet." | Whole page, when no videos exist |

---

## 5. Data sources and API calls

| Data block | Call | Input |
|---|---|---|
| Summary numbers, month list, video cards, insight lines | `POST fetch-youtube-data` | `{}` for the signed-in brand, or `{ "brandOverride": "{Brand}" }` when a brand is selected in the switcher (the month filter is applied on the loaded data; no extra call was made) |
| Usage tracking | `POST user_page_sessions` | `page_path: "/analytics/youtube"`, `user_id` |

Shell calls (roles, subscription, notifications) are listed in [00-global-layout.md](00-global-layout.md) section 5. Thumbnails are loaded from `img.youtube.com`.

---

## 6. Behaviour rules

- **Brand scoped:** data is for the brand selected in the top bar; the page is available only to brands that have it enabled.
- **Empty until tracked:** videos appear only after they are added to the tracking sheet.
- **Insight lines** are generated per load and are independent of the month dropdown.
- **Month dropdown:** updates the two summary numbers; the grid did not follow it in testing (see 3.3).
