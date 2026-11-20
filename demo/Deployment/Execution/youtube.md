# YouTube – Execution Runbook

> Path in the platform: **Execution → Controlled Channels → YouTube** (`/execution/youtube`)
>
> This document explains **how the work is carried out**: who does what, in which order, and how status changes. For screen layout, columns, filters and observed data, see the UI document: [UI/youtube.md](../UI/youtube.md). For the workflow as a flowchart, see [Flowcharts/youtube.md](../Flowcharts/youtube.md).
>
> This page is **not** the same as **Analytics → YouTube Analytics** or **Intelligence → YouTube Intelligence**.

---

## 1. Purpose

The YouTube page is used to prepare the **YouTube details for each brand's videos**: title, description, tags, file name, thumbnail name, first comment and playlist. Work is organised **per brand and per month**. Each row is one video.

The internal team adds the details on the platform. The brand reviews them and approves or disapproves each row. When the video is published, the team (or the brand) adds the **Video URL** and the row is marked **Live on Website**.

## 2. End-to-End Flow

1. Internal team selects the **brand** and the **month**.
2. Team adds rows (**Download Sample CSV** then **Upload CSV**, or **Add Manually**).
3. Every new row starts as **Approval Pending**.
4. The team clicks **Notify new rows** to tell the brand the details are ready. There are **no automatic emails** to the brand.
5. **Brand reviews** each row and **approves** it, or **disapproves** it with a comment saying what to change.
6. After a disapproval, the team reads the comment, **edits the row** and saves. The row returns to **Approval Pending**.
7. The team clicks **Notify changes** so the brand reviews the edited rows. Steps 5–7 repeat until approved.
8. After approval, the team publishes the video, adds the **Video URL** and marks the row **Live on Website**. The brand can also mark a row Live.

---

## 3. Roles and Scope

| Role | Brands in scope | What they can do | What they cannot do |
|------|-----------------|------------------|---------------------|
| **Admin** | All brands | Add rows (Upload CSV, Add Manually), edit, delete (with confirmation), change status, add comments, send Notify emails | Cannot approve or disapprove. **Only the brand user can** |
| **SEO Team Lead** | Assigned brands only | Same as Admin, for assigned brands | Cannot approve or disapprove |
| **SEO Team Member** | Assigned brands only | Same as Admin, for assigned brands | Cannot approve or disapprove |
| **Brand user** | Own brand only | View rows, **approve** or **disapprove** (a disapproval needs a comment), mark **Live on Website** | Cannot add, edit or delete rows. Can comment **only when disapproving** (this applies on all pages) |

Notes:

- On this page, **Admin, Team Lead and Team Member have the same access**. The only difference is the brands each can see.
- Brands never see Add, Upload, Edit, Delete or Notify controls.
- A row can hold **several comments**, each shown with **who wrote it**. The comment box is the same for CSV rows and manually added rows.

---

## 4. Status Control – Who Can Change Status, and To What

### 4.1 Status definitions

Standard status names are used on every page.

| Status | Meaning |
|--------|---------|
| **Approval Pending** | Default for every new row. Waiting for the brand's review. Also the state **any edited row** returns to. (The product flow calls this *Pending*.) |
| **Approved** | The brand accepted the details. The team can publish the video. |
| **Disapproved** | The brand did not accept the details and left a comment on what to change. |
| **Live on Website** | The video is published and the Video URL is added. (The product flow calls this *Live*.) |

### 4.2 Who changes status, and how

| Change | Done by | How |
|--------|---------|-----|
| New row → **Approval Pending** | System | Automatic on upload or manual add |
| Approval Pending → **Approved** | Brand user | Approves the row |
| Approval Pending → **Disapproved** | Brand user | Disapproves and adds a comment |
| **Any status → Approval Pending** | System | Automatic whenever the internal team **edits** the row, whether it was Approved, Disapproved, Live or Pending. **Exception:** adding or changing the **Video URL**, or marking the row **Live on Website** does **not** reset the status |
| Approved → **Live on Website** | Internal team or brand user | After the video is published and the Video URL is added |

### 4.3 Rules to remember

- A disapproval needs a comment.
- **Any edit resets the row to Approval Pending**, so the brand reviews it again. The only exceptions are adding or changing the **Video URL** and marking the row **Live on Website**, which keep the current status.
- A row can be marked **Live on Website** only if it is **Approved** and the **Video URL** is filled.

---

## 5. Runbook – Internal Team

### 5.1 Select brand and month

1. Select the brand in the top brand picker.
2. Select the month with the month selector. **Confirm the month before adding rows**, because additions apply to the selected month. The selector applies to both Upload CSV and Add Manually.

### 5.2 Add rows

**Option A – Upload a CSV**

1. Click **Download Sample CSV** and use it as the template.
2. Fill one row per video. Columns: `keyword`, `optimized_title`, `optimized_description`, `optimized_tags`, `file_name`, `thumbnail_name`, `first_comment`, `playlist`, `video_url`.
3. Click **Upload CSV**, select the brand and month, and choose the file.

**Option B – Add Manually**

1. Click **Add Manually** and select the brand and month.
2. Fill the form (same fields as the CSV) and save.

### 5.3 Data rules

| Rule | Detail |
|------|--------|
| Mandatory field | Only **Keyword**. All other fields can be empty |
| Tags | Written as comma-separated text in the CSV (for example `running shoes, beginner running`). The page shows them as chips |
| Descriptions | May contain line breaks. The CSV reader must handle text inside quotes |
| Video URL | If filled, it must be a valid YouTube link: `youtube.com/watch?v=`, `youtu.be/`, and also `m.youtube.com` and `youtube.com/shorts/` |
| Invalid file | The **whole upload is rejected** with a clear reason (for example "Column optimized_tags is missing") |
| Valid file | All rows are added as **Approval Pending** |
| Duplicates | **No duplicate check for now.** The same keyword and title can be added twice |

### 5.4 Read the table

| Item | Behaviour |
|------|-----------|
| Columns | Keyword, Optimized Title, Optimized Description, Optimized Tags, File Name, Thumbnail Name, First Comment, Playlist, Video URL, Status, Comment, Actions |
| Description, First Comment | Long text is cut short. A **Copy icon** copies the full text |
| Tags | Shown as small chips, with a **Copy icon** |
| Video URL | Shown as **Open ↗**, opening the video in a new tab |
| Empty fields | Shown as "—" |
| Actions | **Edit** and **Delete**, internal team only |
| Search / filters | Search by keyword, title or tags. Filter by status. Columns button shows or hides columns |

### 5.5 After a disapproval

1. Read the brand's **comment** on the row.
2. Click **Edit**, change the fields as per the comment and save. The row goes back to **Approval Pending**.
3. Click **Notify changes** (see 5.8).

### 5.6 Edit a row

1. Click **Edit**. A form opens with all fields.
2. Save. The row becomes **Approval Pending** and is counted under **Notify changes**.

### 5.7 Delete a row

1. Click **Delete**.
2. Confirm in the confirmation message. Deleting a row is **not** counted under Notify changes. A deleted row **cannot be recovered**. Rows in **any status, including Live on Website**, can be deleted.

### 5.8 Mark Live on Website

1. After approval, publish the video on YouTube.
2. Edit the row and add the **Video URL**, then mark it **Live on Website**. The brand user can also mark it Live.
3. Live needs the row to be **Approved** and the **Video URL** filled. Adding or changing the Video URL, or marking Live, does **not** reset the status to Approval Pending (section 4.2). Changing any other field still does.

### 5.9 Emails

**No emails are sent automatically.** Emails to the brand are sent with the **Notify** buttons below the table (internal team only). The email to the brand's assigned team lead is sent by the brand user with the **Notify** button on their dashboard.

| Email | Goes to | When | Button |
|-------|---------|------|--------|
| **Notify new rows** | Brand | Team clicks it. Tells the brand new YouTube details are ready for review | Notify new rows (count) |
| **Notify changes** | Brand | Team clicks it after editing rows as per the brand's comments | Notify changes (count) |
| **Disapproval summary** | Brand's assigned team lead | When the brand user clicks the **Notify** button on their dashboard after disapproving rows with a comment. **Plain text** with only the approved and disapproved counts | **Notify** button on the brand user's dashboard (same on all pages) |

| Topic | Detail |
|-------|--------|
| What one click sends | **Everything changed since the last click**, for the selected brand and month |
| Brand dashboard Notify button | One click sends the disapproval summary for the brand's rows across **all pages**, not only this page |
| Counts on the buttons | Rows waiting to be included. **New rows** counts added rows. **Changes** counts edited rows. Deleted rows are **not** counted |
| Recipients, sender, logging | As on Meta Tags: every external user of the brand, sent by the platform's AI agent, each send logged *(not verified for this page)* |

---

## 6. Runbook – Brand User

1. Open **Execution → Controlled Channels → YouTube** and select the month.
2. For each row, read the title, description, tags, file name, thumbnail name, first comment and playlist. Use the **Copy** icons if needed.
3. **Approve** the row if it is correct.
4. **Disapprove** it if it needs a change, and **add a comment** saying what to change.
   When you finish reviewing, click the **Notify** button on your dashboard. This sends your brand's assigned team lead a plain-text summary with the approved and disapproved counts.
5. After the team edits the row, it returns to **Approval Pending**. Review it again.
6. When the video is published, the row can be marked **Live on Website** by the team or by you. Use **Open ↗** to view the video.

---

## 7. What the Page Looks Like Today (Observed)

The UI document ([UI/youtube.md](../UI/youtube.md)) records a view with a month selector, a search box, a status filter and an 11-column table, and **no Add, Upload, Edit, Delete, Notify or comment controls**.

Differences from the flow above:

- No Actions column, Columns button, Upload or Add controls, or Notify buttons.
- The **Comment** column showed "—" on every row.

**Reason:** that view was a **brand user's view**, not the internal team's. The internal-team controls are not visible to brands. In that view, the approve and disapprove controls are also not described in the UI document *(not verified)*.

## 8. Troubleshooting

| Situation | What to do |
|-----------|------------|
| Upload rejected | Read the reason shown. Download the sample CSV again and match its columns and format |
| Video URL rejected | Use a valid YouTube link (`youtube.com/watch?v=`, `youtu.be/` and the other accepted formats) |
| Empty table | Check the month, search box and status filter. The current month may have no rows |
| Cannot approve or disapprove | The internal team cannot do this. Only the brand can |
| Row went back to Approval Pending | It was edited. Every edit resets the status |
| Brand did not get an email | No emails are sent automatically. Click **Notify new rows** or **Notify changes** |
| Team lead did not get the disapproval summary | The brand user must click the **Notify** button on their dashboard |
