# Web 2.0 – Execution Runbook

> Path in the platform: **Execution → Third Party Channels → Web 2.0** (`/execution/web-two`)
>
> This document explains **how the work is carried out**: who does what, in which order, and how status changes. For screen layout, columns and observed data, see the UI document: [UI/web-2.md](../UI/web-2.md). For the workflow as a flowchart, see [Flowcharts/web-2.md](../Flowcharts/web-2.md).
>
> Email wording is a separate flow and is **not covered** here.

---

## 1. Purpose

The Web 2.0 page is used to plan and track **posts published for a brand on third-party Web 2.0 sites** (free blogging and content-sharing websites). Work is organised **per brand and per month**. Each row is a single **Link** to a post.

The internal team adds the links, the brand approves or disapproves each one, and the row is marked **Live on Website** once the Web 2.0 post is published.

## 2. End-to-End Flow

1. SEO Team Lead or Team Member selects the **brand** and the **month**. The month selector shows the link count, for example *"September 2026, 6 links"*.
2. They add links (**Download Sample CSV** then **Upload CSV**, or **Add Manually**).
3. Every new row starts as **Approval Pending**.
4. The team clicks **Notify new rows** to tell the brand. There are **no automatic emails**.
5. **Brand reviews** each link and **approves** it, or **disapproves** it with a comment saying what to change.
6. After a disapproval, the team reads the comment, **edits or replaces the link** with the pencil icon and saves. The row goes back to **Approval Pending** for another review.
7. The team clicks **Notify changes** to tell the brand about the updates.
8. Once the Web 2.0 post is published, the row is marked **Live on Website**.
9. When the brand has finished reviewing, the brand clicks the **Notify** button on its dashboard to email the brand's assigned team lead.

---

## 3. Roles and Scope

| Role | Brands in scope | What they can do | What they cannot do |
|------|-----------------|------------------|---------------------|
| **Admin** | All brands | Same as the Team Lead | Cannot approve or disapprove |
| **SEO Team Lead** | Assigned brands only | Select brand and month, upload CSV, Add Manually, **edit** and **delete** rows, change status with the dropdown (**Approval Pending** and **Live on Website** only), add comments, send **Notify new rows** and **Notify changes** | Cannot set **Approved** or **Disapproved**, even on the brand's behalf |
| **SEO Team Member** | Assigned brands only | Same as the Team Lead | Same as above |
| **Brand user** | Own brand only | View rows, **approve** or **disapprove**, mark **Live on Website**, add a comment **only when disapproving** (applies on all pages), click the dashboard **Notify** button | Cannot add, edit or delete rows |

Notes:

- The **comment box looks the same for the brand and the team**. A row can hold **several comments**, each shown with **who wrote it**.
- **Admins, Team Leads and Team Members** can all **add comments** (the same on every Third Party Channels page).

---

## 4. Status Control – Who Can Change Status, and To What

### 4.1 Status definitions

Standard status names are used on every page. The product flow calls the first and last ones *Pending* and *Live*.

| Status | Meaning |
|--------|---------|
| **Approval Pending** | Default for every new row. Waiting for the brand's review. Also the state **any edited row** returns to. |
| **Approved** | The brand accepted the link. |
| **Disapproved** | The brand did not accept the link and left a comment explaining what to change. |
| **Live on Website** | The Web 2.0 post is published. |

### 4.2 Who changes status, and how

The status is a **dropdown on each row**.

| Change | Done by | How |
|--------|---------|-----|
| New row → **Approval Pending** | System | Automatic on upload or manual add |
| Approval Pending → **Approved** | Brand user | Approves the link |
| Approval Pending → **Disapproved** | Brand user | Disapproves and adds a comment |
| **Any status → Approval Pending** | System | Automatic whenever the link is **edited or replaced** (pencil icon), whether the row was Approved, Disapproved, Live on Website or Approval Pending (applies on all pages) |
| Team sets **Approval Pending** | Team Lead or Team Member | From the status dropdown. This is a status change, not an edit of the link |
| Approved → **Live on Website** | Team Lead, Team Member or brand user | After the Web 2.0 post is published |

### 4.3 Rules to remember

- A disapproval needs a comment.
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
| Link format | Must be a valid `https://` URL. No other check |
| Duplicate link | The **same link cannot be added twice for a brand** in the same month. An error is shown. **On this page the same link can appear in different months** |
| Invalid file | The **whole upload is rejected** with a clear reason |
| Valid rows | Appear in the table, each as **Approval Pending** |

### 5.3 Read the table

| Item | Behaviour |
|------|-----------|
| Links | Each link is clickable and opens in a new tab. Long links are cut short in the table |
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

1. Confirm the Web 2.0 post is published and the row is **Approved**.
2. Set the status to **Live on Website** with the dropdown. The brand user can also do this.

### 5.7 Emails

**No emails are sent automatically.** Notifications work as on the other pages. Buttons are below the table.

| Email | Goes to | When | Button |
|-------|---------|------|--------|
| **Notify new rows** | Brand | Tells the brand new links have been added | **Notify new rows (count)**, internal team |
| **Notify changes** | Brand | Tells the brand about updates made after its feedback | **Notify changes (count)**, internal team |
| **Disapproval summary** | The brand's assigned team lead | Sent by the brand user when it clicks **Notify** on its dashboard after reviewing. Plain text with only the approved and disapproved counts | **Notify** on the brand user's dashboard (same on all pages, one click covers all pages) |

| Topic | Detail |
|-------|--------|
| What one click sends | **Everything changed since the last click**, for the selected brand and month |
| Counts on the buttons | The number of rows waiting to be included. **New rows** counts added rows. **Changes** counts edited rows. Deleted rows are **not** counted |
| Email content, CC and BCC | A separate flow, **not covered** here |

---

## 6. Runbook – Brand User

1. Open **Execution → Third Party Channels → Web 2.0** and select the month.
2. Click each **link** to open and review the post.
3. **Approve** the link if it is correct.
4. **Disapprove** it if it needs a change, and **add a comment** saying what to change. This is the only time you can comment.
5. After the team edits the link, the row returns to **Approval Pending**. Review it again.
6. When the post is published, you or the team can mark the row **Live on Website** (the row must be **Approved**).
7. When you have finished reviewing, click the **Notify** button on your dashboard. This sends your brand's assigned team lead a plain-text summary with the approved and disapproved counts.

---

## 7. What the Page Looks Like Today (Observed)

The UI document ([UI/web-2.md](../UI/web-2.md)) records a view with a month selector, a count label ("4 links") and a **3-column** table (Links, Status, Comment). The status was plain text, and there was **no status dropdown, Add, Upload, Edit, Delete or Notify control**. Only **Add comment** was available. All 38 rows were **Live**. It was explored with a Sub-Admin account.

Differences from the flow above:

- The status was a badge, not a dropdown, and there was no **Actions** column.
- The status seen was **Live**, the short name for **Live on Website**.
- The same 10 links appeared in May, June and July 2026. This is allowed: on this page a link can be the same across months.

The cause of the missing controls is **not confirmed**. It may depend on the role used when the page was observed, or on features not being released at that time.

## 8. Troubleshooting

| Situation | What to do |
|-----------|------------|
| Upload rejected | Read the reason shown. Download the sample CSV again and match its single `Links` column. |
| Link rejected | Use a valid `https://` URL. |
| Duplicate error | The same link already exists for this brand in this month. Remove it from the file. The same link in a different month is allowed. |
| Row went back to Approval Pending | The link was edited or replaced. Every edit resets the status. |
| Cannot set Live | The row must be **Approved** first. |
| Cannot set Approved or Disapproved | Only the brand user can do this. |
| Brand did not get an email | No emails are sent automatically. Click **Notify new rows** or **Notify changes**. |
| Team lead did not get the disapproval summary | The brand user must click the **Notify** button on their dashboard. |
| Brand cannot comment | Brands can comment only when disapproving. |
