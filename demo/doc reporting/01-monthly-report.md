# Reporting → Monthly Report

| | |
|---|---|
| **Route** | `/reporting/monthly` |
| **Page title** | Monthly Report |
| **Subtitle** | None |
| **Breadcrumb** | DareAISearch › {Brand} › Reporting › Monthly Report |
| **Sidebar location** | REPORTING group → Monthly Report (the only item in the group) |
| **Shared shell** | Top bar, sidebar, breadcrumb and the Miss Daring assistant are documented in [../doc analytics/00-global-layout.md](../doc%20analytics/00-global-layout.md) |

> Documented from the live app, **Sub-Admin** view, on three brands. Text in quotes is exact on-screen text. Months, years and counts are placeholders such as `{Month YYYY}` and `{n}`. Only the first slide of one report was looked at, so the content of the report decks beyond their cover slide is **not documented**.

---

## 1. Purpose

A library of the **monthly performance reports** prepared for the brand, one per month. Each report is a slide deck; the page lists them as cards and opens a chosen one in a viewer on the same page. The page has no data of its own: it only lists and opens the finished reports.

---

## 2. Page sections (top to bottom)

| # | Section | Contents |
|---|---|---|
| 1 | Page title | "Monthly Report" (no subtitle) |
| 2 | Toolbar row | Count text on the left, year dropdown on the right |
| 3 | Report grid | One card per month |

There is no data-freshness banner, AI insight line, Recommended Actions or ⓘ tooltip.

---

## 3. Section details

### 3.1 Toolbar row
| Element | Details |
|---|---|
| Count text | **"{n} reports available"** (grey, small). With one report it reads **"1 report available"** |
| Year dropdown | Button with a calendar icon, the chosen year and a chevron, at the right. Options: **All years** · **{YYYY}** for each year that has reports, newest first (sample: 2026, 2025). The default is the **latest year** (not "All years") |

The count and the grid change with the dropdown. In the Asics sample, **2026** showed 7 reports, **2025** showed 3 and **All years** showed 10.

### 3.2 Report grid
Cards are laid out three per row, newest month first, wrapping to the next row.

| Part of a card | Details |
|---|---|
| Accent | Thin teal bar down the left edge |
| Heading | **{Month YYYY}**, bold (for example "July 2026") |
| Sub-heading | **Monthly Report**, teal |
| Button | Wide dark-teal button **View Report →** with an arrow icon |

Cards are listed by month with no gaps filled: a month without a report has no card.

### 3.3 Report viewer (opens on View Report)
A large rounded modal over the page, with the rest of the page dimmed.

| Part | Details |
|---|---|
| Header | **{Month YYYY}** (bold) and under it "Monthly Report" |
| Close | **X** button at the top right; the **Esc** key also closes it |
| Body | The report deck embedded from Google Slides in preview mode (`docs.google.com/presentation/d/{id}/preview`), filling the modal |
| Viewer bar | At the bottom: previous and next arrows, the slide number box, a three-dot menu, and a **Google Slides** link at the right (Google's own viewer controls) |

**Cover slide (slide 1):** DareAISearch logo with "By {agency name}", the word "FOR", the brand's logo, the title **"AI Search Visibility & Performance Report"** and the month in purple, for example "{Month YYYY}". The remaining slides were not opened.

---

## 4. UI element inventory

### Buttons, dropdowns and toggles
| Control | Where | Action |
|---|---|---|
| Year dropdown | Toolbar row | Filter the cards by year or show all years |
| View Report → | Each card | Open that month's deck in the viewer |
| Previous / Next arrows, slide number box | Viewer bar | Move between slides |
| Three-dot menu | Viewer bar | Google Slides viewer options (contents not captured) |
| Google Slides | Viewer bar | Google's link for the deck |
| X (Close) | Viewer header | Close the viewer |

### Not present on this page
Date range picker, search box, month filter, sort control, download or export button of its own, pagination, AI insight line, Recommended Actions, ⓘ tooltips.

### Badges and labels
| Label | Where | Meaning |
|---|---|---|
| "{n} reports available" | Toolbar row | Number of reports for the chosen year |
| "Monthly Report" | Each card, viewer header | Type of document |

### Status and empty states
No empty-state text was captured: every brand tested had at least one report (Asics 10 across two years, Dorset 7, Herbal Chakra 1).

---

## 5. Data sources and API calls

| Data block | Call | Input |
|---|---|---|
| Report list | `GET monthly_report_submissions` | selected brand name, ordered, limited |
| Reports from the report service | `POST fetch-monthly-reports` | none captured |
| Report deck in the viewer | Google Slides preview, loaded in an iframe | The deck's own link |

Shell calls (roles, subscription, notifications) are listed in the global layout document, section 5.

---

## 6. Behaviour rules

- **Brand scoped:** the list is for the brand chosen in the top bar; switching brand reloads the cards (the same account showed 10, 7 and 1 reports on its three brands).
- **Newest first:** cards are ordered by month, newest first, across all years when "All years" is chosen.
- **Read-only:** the page cannot create, edit or delete a report; the only actions are filtering and viewing.
- **Viewing needs access to the deck:** the deck is shown through Google Slides, so what is visible depends on that deck being available to the viewer's session (it opened without a sign-in prompt in the test).
- **Reports are produced by the team:** the Activity Tracker lists recurring entries such as "DareAISearch Insights prepared the {Brand} monthly performance presentation …", which is presumably the work behind these decks (the link between the two was not shown on either page).
