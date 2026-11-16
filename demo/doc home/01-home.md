# Home

| | |
|---|---|
| **Route** | `/brand-pulse` |
| **Page title** | Home |
| **Subtitle** | "Your weekly AI search command center for {Brand}." |
| **Breadcrumb** | DareAISearch › {Brand} › Home |
| **Sidebar location** | First item, above the ANALYTICS group. It is shown as a rounded teal pill while the page is open. Clicking it from any page returns here |
| **Landing page** | The page the app opens after sign-in |
| **Shared shell** | Top bar, sidebar, breadcrumb and the Miss Daring assistant are documented in [../doc analytics/00-global-layout.md](../doc%20analytics/00-global-layout.md) |

> Documented from the live app, **Sub-Admin** view, on three brands. Names, numbers and dates are placeholders such as `{n}` and `{Brand}`. Text in quotes is exact on-screen text. The page is read-only: every click leads to an Analytics page and nothing was changed.

---

## 1. Purpose

A one-page **weekly summary** for the selected brand. It compares the latest week with the week before and says what moved (prompt rankings, keyword rankings, citations, competitor mentions and traffic), what to push next and where to jump for detail. All of it is generated from the same data as the Analytics pages.

---

## 2. Page sections (top to bottom)

| # | Section | Contents |
|---|---|---|
| 1 | Page header | Title and subtitle |
| 2 | THIS WEEK'S SIGNAL | Highlighted card with one summary sentence and four comparison lines |
| 3 | KPI cards | Four clickable cards in a row |
| 4 | Key Movements | Four clickable cards with a priority tag |
| 5 | Trending This Week | Three lists side by side |
| 6 | Where to Focus Next | Two lists side by side: Opportunities and Spots to Win Back |
| 7 | Recommended Actions | Numbered clickable rows |
| 8 | Jump Into Detail | Row of seven shortcut buttons |

There is no date picker, filter, Refresh button, data-freshness banner or ⓘ tooltip on this page.

---

## 3. Section details

### 3.1 THIS WEEK'S SIGNAL
A wide dark-teal card with a sparkle icon and the small spaced label **THIS WEEK'S SIGNAL**.

| Element | Details |
|---|---|
| Headline | One large sentence built from the week's changes. Seen: "{Brand} has {n} more prompt ranking, {n} prompts trending up, and {n} keywords close to Top 3, {n} citations to earn back ready to act on." and, on a brand with no prompt data, "{Brand} has {n} keywords moved up, and {n} keywords close to Top 3, {n} keywords to recover ready to act on." The parts change with the brand's data, and the wording is not always grammatical ("1 more prompt ranking") |
| Comparison lines | Four small lines saying which two periods were compared: **Traffic:** `{YYYY-MM-DD} – {YYYY-MM-DD} vs {YYYY-MM-DD} – {YYYY-MM-DD}` (last full week vs the week before) · **Prompts:** `{DD-Mon-YYYY} vs {DD-Mon-YYYY}` · **Keywords:** `{DD Month YYYY} vs {DD Month YYYY}` · **Citations:** `{D(th) Month YYYY} vs {D(th) Month YYYY}` |

The date styles differ on the four lines, and on one brand the Keywords line lost its spaces ("16November 2026 vs 10November 2026"). On a brand with no recent keyword scan the keyword dates were months old ("01 August 2026 vs 25 July 2026"), so the keyword part of the page can lag behind the rest.

### 3.2 KPI cards
Four equal cards. Each has a round icon at the left, a small arrow at the top right, an uppercase label, a large number and a change line.

| Card | Icon | Change line | Opens |
|---|---|---|---|
| **RANKED PROMPTS** | List | `{+/-n} ({+/-n.n}%)` and "{DD-Mon-YYYY} vs {DD-Mon-YYYY}" | Prompt Ranking |
| **AI SEARCH TRAFFIC** | Globe | `{+/-n} ({+/-n.n}%)` and "vs prior week" | Overview |
| **KEYWORDS IN TOP 10** | Target | `{+/-n}` and "{DD Month YYYY} vs {DD Month YYYY}" | Keyword Ranking |
| **ORGANIC TRAFFIC** | Trend arrow | `{+/-n} ({+/-n.n}%)` and "vs prior week" | Overview |

The change line starts with a small arrow: green pointing up for a rise, red pointing down for a fall, a grey dash for no change (shown as "0").

### 3.3 Key Movements
Heading with a chart icon and the line **"The four biggest changes this week. Click any card to dive in."**

| Card | Number | Opens | Link text |
|---|---|---|---|
| **Prompts Gained** | Count and change `{+n}` | Prompt Ranking | "Investigate in Prompt Ranking →" |
| **Keywords Improved** | Count and change | Keyword Ranking | "Investigate in Keyword Ranking →" |
| **Prompts to Bring Back** | Count and change `{-n}` | Prompt Ranking | "Investigate in Prompt Ranking →" |
| **Keywords to Recover** | Count and change `{-n}` | Keyword Ranking | "Investigate in Keyword Ranking →" |

Each card has a priority tag at its top right: **HIGH** (red), **MED** (amber) or **LOW** (grey). The tag changes with the brand: Prompts Gained was HIGH on all three brands, while Keywords to Recover was LOW on two and MED on one. How the priority is chosen was not shown.

### 3.4 Trending This Week
Heading "Trending This Week" and the line "Quiet shifts that are easy to miss in the regular reports." Three cards side by side; each row is a prompt on the left and a rank on the right, and each row opens **Prompt Ranking**.

| Card | Row content | Empty-state text |
|---|---|---|
| **Fastest Rising Prompts** | Prompt text and `#{old} → #{new}` in teal (6 rows seen) | "No rising prompts this week." |
| **Newly Appearing** | Prompt text and `#{rank}` in teal (4 rows seen) | "No new prompts entered ranking this week." |
| **Prompts to Bring Back** | Prompt text and `was #{rank}` in red (3 rows seen) | "Every prompt held its rank this week — a strong base to build on." |

### 3.5 Where to Focus Next
Heading "Where to Focus Next" and the line "Wins worth pushing further, and spots worth winning back." Two cards: a green-tinted **Opportunities** and a red-tinted **Spots to Win Back**.

| Card | Rows (what was seen) | Opens |
|---|---|---|
| **Opportunities** | Keyword on the left. On the right either a teal pill **"Rank #{n} • close to Top 3"** (up to 6 rows) or an improvement `{old} → {new}` in teal (3 rows, listed after the pills) | Keyword Ranking |
| **Spots to Win Back** | Keyword with a slip `{old} → {new}` in red (up to 4 rows), then competitor rows "{Competitor} gaining mentions" with `+{n}` in red (up to 3 rows) | Competitors for competitor rows (tested); the keyword rows are expected to open Keyword Ranking but were not clicked |

In the same way, only some Trending rows were clicked (a rising prompt and a prompts-to-bring-back row, both Prompt Ranking); the Newly Appearing rows were not tested.

The row limits are what the three sample brands showed (a brand with 33 improved keywords listed only 3), so the lists are cut to the top few.

### 3.6 Recommended Actions
Heading "Recommended Actions" and the line "Prioritized next steps based on this week's signals." Full-width rows, each with a round number, one sentence and an arrow at the right. The number of rows depends on the brand (5, 4 and 3 were seen), and every row opens a page:

| Sentence pattern | Opens |
|---|---|
| "Keep pushing the {n} prompts that are trending up." | Prompt Ranking |
| "{n} prompts dropped out — easy targets to win back next." | Prompt Ranking |
| "{n} keywords sit just outside the Top 3 — small effort, quick wins." | Keyword Ranking |
| "{n} keywords are moving up — keep the content fresh to hold the gain." | Keyword Ranking |
| "{n} keywords slipped a little — a quick refresh can bring them back." | Keyword Ranking |
| "A few competitors gained mentions — worth a look to see what's working." | Competitors |
| "Citations dipped slightly — a good week to reach out to top sources again." | Citation Overview |

A row appears only when its condition is met that week.

### 3.7 Jump Into Detail
Heading "Jump Into Detail". Seven rounded buttons with an icon each, left to right: **Overview** · **Prompt Ranking** · **Keyword Ranking** · **Citations** · **Competitors** · **Activity** · **YouTube**. They open Overview, Prompt Ranking, Keyword Ranking, Citation Overview, Competitors Intelligence, Activity Tracker and YouTube Analytics. The YouTube button is shown on every brand tested, including one whose sidebar has no YouTube Analytics item.

---

## 4. UI element inventory

### Buttons, dropdowns and toggles
| Control | Where | Opens |
|---|---|---|
| RANKED PROMPTS / AI SEARCH TRAFFIC / KEYWORDS IN TOP 10 / ORGANIC TRAFFIC | KPI cards | Prompt Ranking / Overview / Keyword Ranking / Overview |
| Four Key Movements cards | Key Movements | Prompt Ranking or Keyword Ranking (see 3.3) |
| Prompt and keyword rows | Trending, Opportunities, Spots to Win Back | Prompt Ranking, Keyword Ranking or Competitors |
| Numbered rows | Recommended Actions | See 3.6 |
| Seven shortcut buttons | Jump Into Detail | See 3.7 |

### Badges and labels
| Label | Where | Meaning |
|---|---|---|
| HIGH / MED / LOW | Key Movements cards | Priority of the movement |
| Rank #{n} • close to Top 3 | Opportunities | Keyword ranking just below the Top 3 |
| {old} → {new} | Trending, Opportunities, Spots | Rank before and after; teal means better, red means worse |
| +{n} | Spots to Win Back | Extra mentions a competitor gained |

### Not present on this page
Date picker or compare switch, brand-level filters, search box, sort controls, export, ⓘ tooltips, BETA badges.

### Status and empty states
Each of the three Trending cards has its own empty-state sentence (section 3.4). No whole-page empty state was seen.

---

## 5. Data sources and API calls

| Data block | Call |
|---|---|
| Ranked prompts and prompt movement | `POST fetch-prompt-visibility` |
| Keywords in Top 10, close to Top 3 | `POST fetch-keywords-ranking` |
| Keywords improved | `POST fetch-improved-keywords` |
| Keywords to recover | `POST fetch-dropped-keywords` |
| Citations | `POST fetch-citation-data` |
| Competitor mentions | `POST fetch-competitor-mentions` |
| AI search and organic traffic | `POST fetch-ga4-analytics` |
| Search score trend | `POST fetch-searchscore-trend` |
| Usage tracking | `POST user_sessions`, `POST user_page_sessions` |
| Sub-admin brands list | `GET sub_admin_brands` |

The same calls feed the Analytics pages, so the numbers here should match those pages. Shell calls (roles, subscription, notifications) are listed in the global layout document, section 5.

---

## 6. Behaviour rules

- **Brand scoped:** the page follows the brand chosen in the top bar; the sentence, cards and lists all change with it.
- **Week over week:** traffic compares the last full week with the one before; prompts, keywords and citations compare the last two scan dates, which is why the dates on the four comparison lines differ.
- **Sections adapt to the data:** the headline and the Recommended Actions list drop the parts that have nothing to report, and lists show their empty-state sentence instead of rows.
- **Everything is a shortcut:** no element changes data; every click is a link into an Analytics page.
- **Brand differences:** Dorset showed a locked Search Console item in the sidebar but still a complete Home page; Herbal Chakra's keyword data stopped at an August scan.
- **Pro User view:** not checked on this page; this document describes the Sub-Admin view.
