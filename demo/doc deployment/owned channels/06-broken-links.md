# Broken Links

> Path in the platform: **Deployment → Owned Channels → Broken Links** (`/execution/broken-links`)
> The page title on screen is **Broken Links**. It sits under **Owned Channels**, not under a page named "Broken Links on Online Communities".
> In this document, **{brand name}** stands for the brand selected in the platform and **{brand website}** for that brand's own website.
> **This page is not in every brand's sidebar.** It appeared only for one brand (together with **Robot.txt** and **Sitemap**, which are not covered here). The first brands explored did not show it.
> Explored with a Sub-Admin account. Only observed behaviour is documented. Nothing was created, edited, deleted or submitted. No link was opened.
> The screenshots are unchanged and show the real brand name and real links.

## 1. Overview

The **Broken Links** page is a read-only monthly list of **broken links found for {brand name}**, together with the action planned for each one and its progress. A broken link is a link that leads to a missing or removed page. Broken links give visitors and search engines a bad experience, so they are usually either redirected to a working page or removed.

For each broken link, the page shows:

- The page where the broken link was found.
- The broken link itself.
- The action to take (for example redirect it, or remove it).
- Where to redirect it, when a redirect is planned.
- Comments from the platform team and from the client.
- The status of the fix and when it was last updated.

It helps the team and the client see which broken links were found each month and whether they have been fixed on the website.

## 2. Page Layout

From top to bottom:

| # | Section | What it shows |
|---|---------|---------------|
| 1 | **Breadcrumb** | `DareAISearch > {brand name} > Broken Links`. |
| 2 | **Page header** | Title "Broken Links". There is no subtitle. |
| 3 | **Month selector** (left) | Drop-down showing the selected month. |
| 4 | **Count label** (next to the selector) | e.g. "13 entries in September 2026 for {brand name}". |
| 5 | **Table** | One row per broken link, with 10 columns. It is wide, so it scrolls sideways. |
| 6 | **Empty state** | If the month has no entries: "No entries for *Month Year*." |

The page has no summary cards, search box, status filter or action buttons (no Add, Edit, Delete or Upload). Other items on screen belong to the platform shell: sidebar, brand switcher, theme toggle, notifications bell, user menu and the **Ask Miss Daring** floating button (not explored).

## 3. Features and Functionality

### 3.1 Month selector

- Lists 15 months, from **January 2027** back to **November 2025**.
- The page opens on the **current month** (November 2026), which was empty. Use the selector to move to a month with data.
- Months with entries: **September 2026** (13 entries) and **October 2026** (2 entries). All other months were empty.
- Choosing a month reloads the table and the count label. It is a view filter only.

### 3.2 Links in the table

- **Page URL**, **Broken Link** and **URL for Redirection** are clickable links with a small "open in new tab" icon.
- Long addresses wrap over several lines inside their column.
- I did not open any link.

### 3.3 What is not available

- There is no search, filter, sorting or paging.
- The Status badge is plain text and cannot be changed here.
- The **Reference Screenshot**, **DIAS Comments** and **Client Comments** cells are plain text. They showed "—" on every row, and no button to add a screenshot or a comment was visible.
- Clicking a row does nothing.

## 4. Data Fields and Columns

| Column | What it shows | Observed |
|--------|---------------|----------|
| **#** | Row number. | 1, 2, 3 … |
| **Page URL** | The page of {brand website} where the broken link was found. | Home page, or the blog listing page |
| **Broken Link** | The address that no longer works. | Pages on {brand website}, or product pages on other websites |
| **Reference Screenshot** | A screenshot that shows the problem. | "—" (empty) on all rows |
| **Action To be Taken** | The fix planned for the broken link. | **301 redirection** or **Removal** |
| **URL for Redirection** | The working page the broken link should redirect to. | Filled for 301 redirection rows; "—" for Removal rows |
| **DIAS Comments** | Comments from the platform team. | "—" (empty) on all rows |
| **Client Comments** | Comments from the client. | "—" (empty) on all rows |
| **Status** | The progress of the fix, shown as a badge. | **Live on Website** or **Pending** |
| **Last Updated** | Date and time the row was last updated. | e.g. "2 Nov 2026, 1:54 pm" (the same time on all 15 rows) |

### Action types

| Action | Meaning (inferred from the name and data) |
|--------|-------------------------------------------|
| **301 redirection** | The broken address should send visitors permanently to a working page (shown in **URL for Redirection**). Seen on all 13 September rows. |
| **Removal** | The link to the broken address should be removed from the page. No redirect page is given. Seen on both October rows, where the broken links are product pages on other websites. |

How the data is organised:

- Data is grouped by **month** and by **brand**.
- September 2026: 13 rows. All are **301 redirection** and **Live on Website**. 10 rows were found on the home page and 3 on the blog listing page. The redirect address shown on the first rows is the brand's home page; I did not compare every row.
- October 2026: 2 rows. Both are **Removal** and **Pending**, and both were found on the home page.
- There is no screenshot, DIAS comment or client comment on any row.

## 5. Available Statuses

| Status | Look | Meaning (inferred) | Seen in data? |
|--------|------|--------------------|---------------|
| **Live on Website** | Dark badge | The fix (the redirect) is done and active on the website. | Yes, on all 13 September rows |
| **Pending** | Dark badge | The fix has not been done yet. | Yes, on both October rows |

The meanings come from the names; the page gives no explanation. Other statuses (for example Approved or Disapproved, as on other pages) may exist but did not appear.

## 6. User Workflow

1. Sign in and select the brand in the top bar. Check that **Broken Links** appears under **Deployment → Owned Channels** for that brand.
2. Open **Deployment → Owned Channels → Broken Links**.
3. The current month may be empty. Use the **month selector** to choose a month with entries.
4. Read the count label to see how many broken links were found.
5. For each row, read the **Page URL** (where it was found) and the **Broken Link** (what is broken).
6. Read **Action To be Taken** and, for redirects, the **URL for Redirection**.
7. Scroll sideways to see the comments, the **Status** and **Last Updated**.
8. Click a link to open the page in a new tab and check it, if needed.

## 7. Important Notes and Dependencies

- The page is **view-only**. No control on it adds or changes data.
- The page is **brand-specific**: it is available in the sidebar for some brands only.
- Data is **per brand and per month**. Changing the brand in the top bar changes the list.
- The page opens on the current month, which may be empty.
- The fix itself (adding a redirect or removing a link) happens on the brand's website, not on this page. This page only tracks it.
- The two comment columns and the screenshot column were empty, so how they look when filled is not documented.
- All 15 rows show the same "Last Updated" time, so the time may reflect when the data was loaded rather than when each fix was made. This is an observation only.
- **Not tested**: opening the links, other months in other brands and the **Ask Miss Daring** button.

## 8. Screenshots

| Screenshot | Description |
|------------|-------------|
| ![Empty month](../screenshots/broken-links/01-default-view.png) | Default view: empty current month (November 2026). |
| ![Month selector](../screenshots/broken-links/02-month-selector.png) | Month selector list (15 months). |
| ![September left](../screenshots/broken-links/03-september-2026-left.png) | September 2026, left side: row number, Page URL, Broken Link, Reference Screenshot, Action and URL for Redirection. |
| ![September right](../screenshots/broken-links/04-september-2026-right.png) | September 2026 scrolled right: comments, Status and Last Updated. |
| ![October](../screenshots/broken-links/05-october-2026.png) | October 2026: two **Removal** rows with **Pending** status. |
