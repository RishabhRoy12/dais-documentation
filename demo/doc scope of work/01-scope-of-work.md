# Deployment → Scope of Work

| | |
|---|---|
| **Route** | `/deliverables/scope-of-work` |
| **Page title** | Scope of Work |
| **Subtitle** | "Monthly task plan and deliverable commitments" |
| **Breadcrumb** | DareAISearch › {Brand} › Scope of Work |
| **Sidebar location** | DEPLOYMENT group → Scope of Work (the last item of the group, below the channel lists) |
| **Shared shell** | Top bar, sidebar, breadcrumb and the Miss Daring assistant are documented in [../doc analytics/00-global-layout.md](../doc%20analytics/00-global-layout.md) |

> Documented from the live app, **Sub-Admin** view, on three brands (one filled in, one partly filled in, one in an error state). Names, dates and counts are placeholders such as `{Person}` and `{n}`. Text in quotes is exact on-screen text. The task names are the same standard monthly plan for every brand; they are quoted because they are the content of the page.

---

## 1. Purpose

Shows the **monthly plan of work** the DareAISearch team has committed to for the brand: a dated task list with the projects each task covers, who is responsible and whether it is done. The four counters at the top summarise the list.

---

## 2. Page sections (top to bottom)

| # | Section | Contents |
|---|---|---|
| 1 | Page header | Title, subtitle and a **Refresh** button at the right |
| 2 | Summary cards | Four cards: Total Tasks, Completed, In Progress, Pending |
| 3 | Task table | Six columns, scrolls inside its own box |

There is no data-freshness banner, filter, search box, AI insight line, Recommended Actions or ⓘ tooltip.

---

## 3. Section details

### 3.1 Refresh
Outlined button with a refresh icon, top right. Fetches the plan again (one call, see section 5).

### 3.2 Summary cards
Four equal cards in one row, each with a small icon, an uppercase label and a large number.

| Card | Icon and colour | Counts |
|---|---|---|
| **TOTAL TASKS** | Clipboard, neutral | Every row of the table |
| **COMPLETED** | Check circle, green border and number | Rows whose **STATUS** is Completed |
| **IN PROGRESS** | Clock, amber border and number | Rows whose **STATUS** is Work in Progress |
| **PENDING** | Alert circle, neutral | Rows whose **STATUS** is Pending |

The cards count the **STATUS** column. When that column is empty the cards show 0 even if other columns contain status words (see 6).

### 3.3 Task table
A bordered table with an uppercase header row. The body scrolls vertically inside a box about **700 px** high, with the header kept in view. All rows load at once (36 and 34 in the samples).

| Column | Content |
|---|---|
| **TASK** | Bold task name, up to two lines (for example "Prepare clients report", "Work on Off Page Backlinks ( 60 Backlinks)", "Meta tags updation on website") |
| **PROJECTS** | Teal outlined chips. **All Projects** for tasks that cover everything, or one chip per project or client, wrapping to a second line when there are many |
| **TIME TAKEN** | A date in the form **{D-Mon-YY}**, for example "2-Nov-26". Despite the header it holds a **due date**, not a duration |
| **WORK DONE FOR** | A chip: **Last Month** · **Same Month** · **Next Month**, saying which month the task's work belongs to |
| **RESPONSIBILITY** | Teal chips with the names of the people responsible; "—" when nobody is set |
| **STATUS** | A pill: **Completed** (green, check icon) · **Work in Progress** · "—" when not started. A **Pending** value is also counted by the cards |

Rows are in date order, earliest first. The same task name repeats on many dates (the backlinks task is listed once per working day).

### 3.4 Standard plan (task names seen)
The plan has 19 distinct tasks (36 rows once repeats are counted); the sample lists them in this order: All clients previous months work check · Prepare clients report · Share the reports with managers, Poc, VP & COO · Identify the focus keywords, Prompts and Pages to work on · Work on Off Page Backlinks (60 Backlinks) · Finalise the On Page Blog topics and share with clients for Approval · On Page Suggestions · Schemas creation and share with clients · Content Audit and finalise the pages and share with content writer · Share the approved blog topics with content writer · Share the On Page Suggestions with content writer · XML Sitemap & Robots Txt and Manual updation any if required · Outreach the Paid Backlinks Sites · Finalise the topics for Outreach paid backlinks site and share with content writer · Reviews additon & replies on GMB and 3rd party review addition · Share the paid content with the outreach sites for publication · Meta tags updation on website · Check all the updates which shared with client · Re check the changes and update with the clients.

---

## 4. UI element inventory

### Buttons, dropdowns and toggles
| Control | Where | Action |
|---|---|---|
| Refresh | Header | Fetch the plan again |
| Try again | Error card | Retry the failed load |

### Not present on this page
Month or date filters, search box, sorting on column headers, row click-through, edit or add task buttons (the page is read-only), export, AI insight line, Recommended Actions, ⓘ tooltips.

### Badges and labels
| Label | Where | Meaning |
|---|---|---|
| All Projects / {Project} | PROJECTS chips | Scope of the task |
| Last Month / Same Month / Next Month | WORK DONE FOR chips | Month the work belongs to |
| Completed / Work in Progress | STATUS pill | Progress of the task |

### Status and empty states
| State | Text |
|---|---|
| Load failed | Red-bordered card: **"Failed to load Scope of Work"**, the reason line (seen: **"Access denied for this brand"**) and a **Try again** button. The header and Refresh button stay |
| No tasks | Not captured |

---

## 5. Data sources and API calls

| Data block | Call | Input |
|---|---|---|
| Summary cards and task table | `GET fetch-scope-of-work` | `brand={Brand}` in the query |

Pressing **Refresh** repeats this single call. Shell calls (roles, subscription, notifications) are listed in the global layout document, section 5.

---

## 6. Behaviour rules

- **Brand scoped:** the plan is for the brand chosen in the top bar. The same account saw 36 tasks on one brand, 34 on another and an error on the third.
- **Access can be refused per brand:** a brand the account may not read shows the red error card ("Access denied for this brand") instead of the table; the summary cards are hidden in that case.
- **Cards follow the STATUS column only.** On the 36-task brand the table's **STATUS** column was empty, so the cards read **0 / 0 / 0**, while three rows carried "pending", "Work in Progress" and "Completed" text in the **WORK DONE FOR** column instead. On the 34-task brand every column was filled and the cards read **14 completed / 1 in progress / 0 pending**.
- **Column labels do not always match the contents:** **TIME TAKEN** shows dates, and on the 36-task brand the status words sat under **WORK DONE FOR**. Treat the data as read from a shared plan sheet whose columns were not filled the same way for every brand.
- **Odd dates:** the last rows of both filled-in brands carry years that look like typing slips (for example "30-Nov-31", "29-Oct-31") and appear after the November 2026 rows.
- **Read-only:** the page has no edit controls; where progress is updated was not shown.
- **Sidebar differences by brand:** a brand without the Search Console plan shows that item locked, and Local Listings appears only for some brands, as described in the global layout document.
