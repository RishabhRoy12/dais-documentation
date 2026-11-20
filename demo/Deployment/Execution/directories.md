# Directories – Execution Runbook

> Path in the platform: **Execution → Third Party Channels → Directories** (`/execution/directories`)
>
> This document explains **how the work is carried out**: who does what, in which order, and how status changes. For screen layout, columns and observed data, see the UI document: [UI/directories.md](../UI/directories.md). For the workflow as a flowchart, see [Flowcharts/directories.md](../Flowcharts/directories.md).
>
> Email content, CC and BCC are a separate flow and are **not covered** here.

---

## 1. Purpose

The Directories page is used to plan and track **business-directory websites where a brand is listed or submitted for listing**. A directory listing is an online mention of the brand (name, category and a link to its website). Work is organised **per brand and per month**. Each row is a **Link** to a directory listing.

The internal team adds the links, the brand approves or disapproves each one, and the row is marked **Live on Website** once the directory listing is published.

## 2. End-to-End Flow

1. SEO Team Lead or Team Member selects the **brand** and the **month**. The month selector shows a count, for example *"August 2026, 20 links"*.
2. They add links (**Download Sample CSV** then **Upload CSV**, or **Add Manually**).
3. Every new row starts as **Approval Pending**.
4. The team clicks **Notify new rows** to tell the brand. There are **no automatic emails**.
5. **Brand reviews** each link and **approves** it, or **disapproves** it with a comment saying what to change.
6. After a disapproval, the team reads the comment, **edits or replaces the link** with the pencil icon and saves. The row goes back to **Approval Pending** for another review.
7. The team clicks **Notify changes** to tell the brand about the updates.
8. Once the directory listing is published, the row is marked **Live on Website**.
9. When the brand has finished reviewing, the brand clicks the **Notify** button on its dashboard to email the brand's assigned team lead.

---

## 3. Roles and Scope

| Role | Brands in scope | What they can do | What they cannot do |
|------|-----------------|------------------|---------------------|
| **Admin** | All brands | Same as the Team Lead, including **adding comments** at any time | Cannot approve or disapprove |
| **SEO Team Lead** | Assigned brands only | Select brand and month, upload CSV, Add Manually, **edit** and **delete** rows, change status with the dropdown (**Approval Pending** and **Live on Website** only), **add comments at any time**, send **Notify new rows** and **Notify changes** | Cannot set **Approved** or **Disapproved**, even on the brand's behalf |
| **SEO Team Member** | Assigned brands only | Same as the Team Lead | Same as above |
| **Brand user** | Own brand only | View rows, **approve** or **disapprove**, mark **Live on Website**, add a comment **only when disapproving** (applies on all pages), click the dashboard **Notify** button | Cannot add, edit or delete rows |

Notes:

- **Admins, Team Leads and Team Members** can all **add comments at any time** (the same on every Third Party Channels page).
- The **comment box looks the same for the brand and the team**. A row can hold **several comments**, each shown with **who wrote it**.
- The status dropdown, the admin and brand rights, and the Live rule are the same as on [Guest Post](guest-post.md) and [Classified](classified.md).

---

## 4. Status Control – Who Can Change Status, and To What

### 4.1 Status definitions

Standard status names are used on every page. The product flow calls the first and last ones *Pending* and *Live*.

| Status | Meaning |
|--------|---------|
| **Approval Pending** | Default for every new row. Waiting for the brand's review. Also the state **any edited row** returns to. |
| **Approved** | The brand accepted the link. |
| **Disapproved** | The brand did not accept the link and left a comment explaining what to change. |
| **Live on Website** | The directory listing is published. |

The *Review* status seen in the UI document is **not** a standard status. It is treated as **Approval Pending** (see section 7).

### 4.2 Who changes status, and how

The status is a **dropdown on each row**.

| Change | Done by | How |
|--------|---------|-----|
| New row → **Approval Pending** | System | Automatic on upload or manual add |
| Approval Pending → **Approved** | Brand user | Approves the link |
| Approval Pending → **Disapproved** | Brand user | Disapproves and adds a comment |
| **Any status → Approval Pending** | System | Automatic whenever the link is **edited or replaced** (pencil icon), whether the row was Approved, Disapproved, Live on Website or Approval Pending (applies on all pages) |
| Team sets **Approval Pending** | Team Lead or Team Member | From the status dropdown. This is a status change, not an edit of the link |
| Approved → **Live on Website** | Team Lead, Team Member or brand user | After the directory listing is published |

### 4.3 Rules to remember

- A disapproval needs a comment.
- Adding a comment never changes a row's status.
- The disapprove → edit → resubmit cycle repeats until the brand approves.
- A row can be marked **Live on Website** only if it is **Approved**.
- Changing the status with the dropdown does **not** reset the row to Approval Pending. Editing or replacing the link does.

---

## 5. Runbook – Internal Team (Team Lead and Team Member)

### 5.1 Select brand and month

1. Select the brand in the top brand picker.
2. Select the month with the month selector. **Confirm the month before adding rows**, because additions apply to the selected month.

### 5.2 Add links

**Option A – Upload a CSV**

1. Click **Download Sample CSV** and use it as the template. It has **one column, `Links`**.
2. Fill one link per row.
3. Click **Upload CSV** and choose the file.

**Option B – Add Manually**

1. Click **Add Manually**.
2. Enter the link and save.

Each row has **one field only: the Link**.

| Rule | What happens |
|------|--------------|
| Link format | Must be a valid `https://` URL |
| Duplicate link | The **same link cannot be added twice for a brand in the same month**. An error is shown. **In different months the same link is allowed** |
| Invalid file | The **whole upload is rejected** with a clear reason |
| Valid rows | Appear in the table, each as **Approval Pending** |

### 5.3 Read the table

| Item | Behaviour |
|------|-----------|
| Links | Each link is clickable and opens in a new tab |
| Status | Dropdown on each row |
| Comment | **Add comment** on each row. Several comments possible, each with its author |
| Actions | **Pencil** (edit) and **bin** (delete), internal team only |

### 5.4 After a disapproval

1. Read the brand's **comment** on the row.
2. Click the **pencil** icon and **edit or replace** the link, then save. The row goes back to **Approval Pending**.
3. Click **Notify changes** (see 5.7).

### 5.5 Delete a row

1. Click the **bin** icon and confirm in the confirmation message.
2. A deleted row **cannot be recovered**. Rows in **any status, including Live on Website**, can be deleted.
3. Deleting a row is **not** counted under **Notify changes**.

### 5.6 Mark Live on Website

1. Confirm the directory listing is published and the row is **Approved**.
2. Set the status to **Live on Website** with the dropdown. The brand user can also do this.

### 5.7 Emails

**No emails are sent automatically.** Two buttons sit below the table, each with a counter. They are for the internal team and work as on [Guest Post](guest-post.md).

| Email | Goes to | When | Button |
|-------|---------|------|--------|
| **Notify new rows** | Brand | Emails the brand about links **added since the last notification** | **Notify new rows (count)**. The counter shows how many new rows are waiting |
| **Notify changes** | Brand | Emails the brand about **updates to existing rows**, such as **status changes or edits** | **Notify changes (count)**. The counter shows how many changes are waiting |
| **Disapproval summary** | The brand's assigned team lead | Sent by the brand user when it clicks **Notify** on its dashboard after reviewing. Plain text with only the approved and disapproved counts | **Notify** on the brand user's dashboard (same on all pages, one click covers all pages) |

| Topic | Detail |
|-------|--------|
| What one click sends | **Everything changed since the last click**, for the selected brand and month |
| Counter at (0) | Nothing is pending to send |
| Deleted rows | Not counted |
| Email content, CC and BCC | A separate flow, **not covered** here |

---

## 6. Runbook – Brand User

1. Open **Execution → Third Party Channels → Directories** and select the month.
2. Click each **link** to open and review the directory listing.
3. **Approve** the link if it is correct.
4. **Disapprove** it if it needs a change, and **add a comment** saying what to change. This is the only time you can comment.
5. After the team edits the link, the row returns to **Approval Pending**. Review it again.
6. When the directory listing is published, you or the team can mark the row **Live on Website** (the row must be **Approved**).
7. When you have finished reviewing, click the **Notify** button on your dashboard. This sends your brand's assigned team lead a plain-text summary with the approved and disapproved counts.

---

## 7. What the Page Looks Like Today (Observed)

The UI document ([UI/directories.md](../UI/directories.md)) records a view with a month selector, a count label and a **3-column** table (Links, Status, Comment). The status was a plain badge, and there was **no status dropdown, Add, Upload, Edit, Delete or Notify control**. It was explored with a Sub-Admin account.

Differences from the flow above:

- The status was a badge, not a dropdown, and there was no **Actions** column.
- The statuses seen were **Live** (the short name for **Live on Website**) and **Review**. **Review** is not a standard status and is treated as **Approval Pending**.
- The comment box was **read-only**, with no text area and no **Send** button, and it showed "No comments yet." In the flow, the team can comment at any time and the brand only when disapproving.
- Six links appeared in both October and September 2026. This is allowed: the same link can be used in different months.
- The page appeared in the sidebar **only for some brands**. This was observed on screen. The flow does not describe which brands see it.
- The bottom of the page, where the **Notify** buttons and counters sit, was not seen.

The cause of the missing controls is **not confirmed**. It may depend on the role used when the page was observed, or on features not being released at that time.

## 8. Troubleshooting

| Situation | What to do |
|-----------|------------|
| Upload rejected | Read the reason shown. Download the sample CSV again and match its single `Links` column. |
| Link rejected | Use a valid `https://` URL. |
| Duplicate error | The same link already exists for this brand in this month. Remove it from the file. The same link in a different month is allowed. |
| Row went back to Approval Pending | The link was edited or replaced. Every edit resets the status. |
| Row shows *Review* | An older status name. Treat it as **Approval Pending**. |
| Cannot set Live | The row must be **Approved** first. |
| Cannot set Approved or Disapproved | Only the brand user can do this. |
| Brand did not get an email | No emails are sent automatically. Click **Notify new rows** or **Notify changes**. |
| Counter shows (0) | Nothing is waiting to be sent. |
| Team lead did not get the disapproval summary | The brand user must click the **Notify** button on their dashboard. |
| Brand cannot comment | Brands can comment only when disapproving. |
| Directories missing from the sidebar | The page appeared only for some brands when observed. Check the brand selected. |
