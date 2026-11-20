# Classified

> Path in the platform: **Execution → Third Party Channels → Classified** (`/execution/classified`)
> In this document, **{brand name}** stands for the brand selected in the platform.
> Explored with a Sub-Admin account. Only observed behaviour is documented. Nothing was created, edited, deleted or submitted. No listing link was opened.
> The screenshots are unchanged and show the real brand name and real listing links.

## 1. Overview

The **Classified** page is a read-only monthly list of **classified-ad listings posted for {brand name}** on third-party classified-ad websites. Each listing is a "citation": an online mention of the brand (for example, an ad for the brand's products) that can link back to its website and help search engines and AI search engines recognise the brand.

For each listing, the page shows:

- The link to the listing.
- Its status (for example **Live**).
- A comment button.

It helps the team see which classified listings were posted each month and whether they are live.

## 2. Page Layout

From top to bottom:

| # | Section | What it shows |
|---|---------|---------------|
| 1 | **Breadcrumb** | `DareAISearch > {brand name} > Classified`. |
| 2 | **Page header** | Title "Classified". There is no subtitle. |
| 3 | **Month selector** (left) | Drop-down showing the selected month. |
| 4 | **Count label** (next to the selector) | e.g. "50 links". |
| 5 | **Table** | One row per listing, with 3 columns: Links, Status, Comment. |

The page has no summary cards, search box, status filter or action buttons (no Add, Edit, Delete or Upload). Other items on screen belong to the platform shell: sidebar, brand switcher, theme toggle, notifications bell, user menu and the **Ask Miss Daring** floating button (not explored).

## 3. Features and Functionality

### 3.1 Month selector

- The list is short. It had only **three months**: **July 2026**, **June 2026** and **May 2026**.
- The page opens on **July 2026**, the latest month with data. It does not open on the current calendar month.
- Choosing a month reloads the table and the count label. It is a view filter only.

### 3.2 Links

- Each row's link opens the listing in a new tab. It has a small "open in new tab" icon in front of it.
- Long links are shortened with "…" in the table.
- I did not open any link.

### 3.3 Comment button

- The **Comment** column shows a small speech-bubble icon followed by "—".
- Clicking it opens a small box that reads **No comments yet.** (observed on the first row).
- The box has **no text area and no Send button**, so comments cannot be written from this page. This is the same as on the Social Citation page, and different from the Profile Citation page.
- I did not check whether other rows have existing comments.

### 3.4 Long list

All rows for the month are shown on one page. There is no paging, no "load more" button and no search. Scroll down the page to see the full list (50 rows in each month).

### 3.5 What is not available

There is no search, no filter and no sorting. The status badge is plain text and cannot be changed here. Clicking a row does nothing.

## 4. Data Fields and Columns

| Column | What it shows |
|--------|---------------|
| **Links** | The address of the classified listing. Opens in a new tab. |
| **Status** | A green badge showing the status of the listing (observed: **Live**). |
| **Comment** | A comment button (icon and "—") that opens the comments box. |

How the data is organised:

- Data is grouped by **month** and by **brand**.
- Each of the three months shows **50 links**, and the list is **identical in all three months** (the same 50 listings appear in July, June and May 2026). The page does not explain why.
- The listings are spread over **17 different classified-ad websites**. Most sites have 3 or 4 listings each, and three sites have 1 listing each.
- The link addresses suggest each listing is an ad for one of the brand's products (for example, running or sports shoes). This is an observation only; the page does not state it.

## 5. Available Statuses

| Status | Look | Meaning (from its name) | Seen in data? |
|--------|------|-------------------------|---------------|
| **Live** | Green badge | The listing is published and available online. | Yes, on all 50 rows in each month |

Other statuses (for example Pending, as on the Profile Citation page) may exist, but none appeared here. The meaning of Live comes from its name; the page gives no explanation.

## 6. User Workflow

1. Sign in and select the brand in the top bar.
2. In the sidebar, open **Execution → Third Party Channels → Classified**.
3. Read the count label to see how many listings are shown for the month.
4. Use the **month selector** to move between the three available months.
5. Scroll down to see all rows and check the **Status** of each.
6. Click a **link** to open the listing in a new tab and check it.
7. Click the comment button on a row to see its comments (if any).

## 7. Important Notes and Dependencies

- The page is **view-only**. No control on it adds or changes data.
- Data is **per brand and per month**. Changing the brand in the top bar changes the list. The brand switcher lists more than one brand; only one was explored.
- The month list contains only months that have data (three months were available). The page opens on the latest of them.
- Listings are on **third-party classified-ad websites**, which the platform does not control. A link may stop working if a listing expires or is removed.
- The same 50 listings appear in every month seen, so counts across months should not be added together as new listings.
- No existing comments were seen, so how comments are displayed once added is not documented. Comments seem to be added elsewhere.
- **Not tested**: opening the links, other brands and the **Ask Miss Daring** button.

## 8. Screenshots

| Screenshot | Description |
|------------|-------------|
| ![Default view](screenshots/classified/01-default-view.png) | Default view: month selector, count label and table (July 2026). |
| ![Month selector](screenshots/classified/02-month-selector.png) | Month selector list (three months). |
| ![Comment box](screenshots/classified/03-comment-popup.png) | Comment box showing "No comments yet." with no text area or Send button. |
| ![Bottom of list](screenshots/classified/04-bottom-of-list.png) | Bottom of the list, showing that all rows are on one page. |
