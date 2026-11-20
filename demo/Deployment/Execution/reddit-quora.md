# Reddit/Quora – Execution Runbook

> Path in the platform: **Execution → Third Party Channels → Reddit/Quora** (`/execution/reddit`)
>
> This document explains **how the work is carried out**: who does what, in which order, and how the brand is notified. For screen layout, columns and observed data, see the UI document: [UI/reddit-quora.md](../UI/reddit-quora.md). For the workflow as a flowchart, see [Flowcharts/reddit-quora.md](../Flowcharts/reddit-quora.md).
>
> **This page is different from the other Third Party Channels pages.** It has **no approval step**: no status, no comments, no approve or disapprove, and no Live marking. The all-pages rules about statuses, comments, edits resetting to Approval Pending and the brand dashboard Notify button **do not apply** here.
>
> Email content, CC and BCC are a separate flow and are **not covered** here. This page is not the same as **Analytics → Reddit Overview**.

---

## 1. Purpose

The Reddit/Quora page is used to record **answers posted on Reddit and Quora discussion threads for a brand**. Work is organised **per brand and per month**. Each entry holds the question thread, the answer text and, optionally, the link to the posted answer.

The internal team adds the entries and notifies the brand once. The brand only **views** them.

## 2. End-to-End Flow

1. SEO Team Lead or Team Member selects the **brand** and the **month**. The page shows the month selector and a count, for example *"6 entries for July 2026"*.
2. They add entries (**Download Sample CSV** then **Upload CSV**, or **Add Manually**).
3. They check the rows. They can **edit** or **delete** a row if needed.
4. When all rows are added, they click **Notify** in the bar at the bottom of the page. The bar reads *"Add rows first, then notify the brand"*.
5. The brand receives one email saying the entries are ready, and sees the entries on the page.

There is **no review loop**: the brand does not approve, disapprove or comment.

---

## 3. Roles and Scope

| Role | Brands in scope | What they can do | What they cannot do |
|------|-----------------|------------------|---------------------|
| **Admin** | All brands | Same as the Team Lead | – |
| **SEO Team Lead** | Assigned brands only | Select brand and month, upload CSV, Add Manually, **edit** and **delete** rows, copy answers, click **Notify** | – |
| **SEO Team Member** | Assigned brands only | Same as the Team Lead | – |
| **Brand user** | Own brand only | **View** the entries, open the links, copy answers | Cannot add, edit or delete rows. Cannot approve, disapprove, comment or mark anything Live. Does not use a Notify button on this page |

---

## 4. Fields and Rules

### 4.1 Fields

Each entry has **three fields**. The sample CSV headers are `Question`, `Answer` and `Live Link`.

| Field | Meaning | Required? |
|-------|---------|-----------|
| **Question** | The link to the Reddit or Quora thread | Yes |
| **Answer** | The answer text posted on that thread | Yes |
| **Live Link** | The link to the posted answer | **Optional** |

### 4.2 Rules

| Rule | What happens |
|------|--------------|
| Links | The Question link and the Live Link (if given) must be valid `https://` URLs |
| Invalid file | The upload is **rejected** with a clear reason |
| Duplicates | **No duplicate check** is described for this page |
| Empty Live Link | Allowed. The cell shows a dash |

There is **no status** on this page. Editing a row does not change anything else.

---

## 5. Runbook – Internal Team (Team Lead and Team Member)

### 5.1 Select brand and month

1. Select the brand in the top brand picker.
2. Select the month with the month selector. **Confirm the month before adding rows**, because additions apply to the selected month.

### 5.2 Add entries

**Option A – Upload a CSV**

1. Click **Download Sample CSV** and use it as the template (`Question`, `Answer`, `Live Link`).
2. Fill one entry per row. **Live Link** can be left empty.
3. Click **Upload CSV** and choose the file.

**Option B – Add Manually**

1. Click **Add Manually**.
2. Fill the **Question**, **Answer** and, if available, the **Live Link**, then save.

### 5.3 Read the table

| Column | Behaviour |
|--------|-----------|
| Question | A clickable link that opens the thread in a new tab. Long links are cut short in the table |
| Answer | A short preview of the answer text, with a **copy icon** that copies the full answer |
| Live Link | A clickable link to the posted answer. If it was not provided, the cell shows a dash |
| Actions | **Pencil** (edit) and **bin** (delete), internal team only |

### 5.4 Edit a row

1. Click the **pencil** icon, change the fields and save.
2. There is no status, so the row stays as it is.

### 5.5 Delete a row

1. Click the **bin** icon and confirm in the confirmation message.
2. A deleted row **cannot be recovered**.

### 5.6 Notify the brand

**No emails are sent automatically.** A bar at the bottom of the page reads *"Add rows first, then notify the brand"* and has one **Notify** button, for the internal team.

| Topic | Detail |
|-------|--------|
| What it sends | One email to the brand telling them the entries are ready |
| When to click | **After all rows are added.** Add all the rows first, then notify once |
| One email | The page is built to send **one email per brand**, so avoid clicking before the rows are ready |
| What one click covers | **Everything changed since the last click**, for the selected brand and month, as on the other pages. Deleted rows are not counted |
| Counter | **None.** The bar has no counter |
| Email content, CC and BCC | A separate flow, **not covered** here |

---

## 6. Runbook – Brand User

1. Open **Execution → Third Party Channels → Reddit/Quora** and select the month.
2. Read each entry: the question, the answer and the live link.
3. Click a **Question** or **Live Link** to open the thread or the posted answer in a new tab.
4. Use the **copy icon** to copy an answer if needed.

There is nothing to approve, disapprove or comment on.

---

## 7. What the Page Looks Like Today (Observed)

The UI document ([UI/reddit-quora.md](../UI/reddit-quora.md)) records a **fully view-only** page: a count label, a month selector and a **3-column** table (Question, Answer, Live Link), with **no Add, Upload, Edit, Delete or Notify control**. It was explored with a Sub-Admin account.

Differences from the flow above:

- There was **no Actions column** and no **Notify** bar.
- The **Question** and **Answer** cells were **empty** ("—") on all 11 rows, and the **Live Link** was filled on every row. In the flow, Question and Answer are required for new rows.
- The **Question** column is described as the thread link in the flow, while the UI doc treated it as question text.
- All links were **Reddit** links. No Quora link was seen.
- Two links appeared in both June and July 2026, so the page repeats links across months.
- Whether the answer **copy icon** exists was not seen in the UI doc.

The cause of the missing controls is **not confirmed**. It may depend on the role used when the page was observed, or on features not being released at that time.

## 8. Troubleshooting

| Situation | What to do |
|-----------|------------|
| Upload rejected | Read the reason shown. Download the sample CSV again and match its `Question`, `Answer` and `Live Link` columns. |
| Link rejected | Use a valid `https://` URL. |
| Empty table or "No entries" message | Check the month. The page opens on the current month, which may be empty. |
| Live Link shows a dash | It was not provided. This is allowed. |
| Brand did not get an email | No emails are sent automatically. Click **Notify** at the bottom of the page. |
| Brand asks to approve or comment | Not available. This page has no approval step. |
