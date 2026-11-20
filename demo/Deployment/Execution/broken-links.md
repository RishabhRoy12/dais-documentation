# Broken Links – Execution Runbook

> Path in the platform: **Deployment → Owned Channels → Broken Links** (`/execution/broken-links`)
>
> This document explains **how the work is carried out**: who does what, in which order, and how status changes. For screen layout, columns and observed data, see the UI document: [UI/broken-links.md](../UI/broken-links.md). For the workflow as a flowchart, see [Flowcharts/broken-links.md](../Flowcharts/broken-links.md).
>
> Email content, CC and BCC are a separate flow and are **not covered** here.
>
> **This page is different from the link pages.** Each row describes **one broken link and its fix**, with several fields and **two comment columns**.

---

## 1. Purpose

The Broken Links page is used to plan and track **broken links found for a brand** and the **fix for each one**, for example a 301 redirect. A broken link is a link that leads to a missing or removed page. Work is organised **per brand and per month**. Each row is one broken link.

The internal team adds the entries, the brand reviews the broken links and the proposed fixes, and the row is marked **Live on Website** once the fix is done on the website.

## 2. End-to-End Flow

1. SEO Team Lead or Team Member selects the **brand** and the **month**. The page shows the month selector and a count.
2. They add entries (**Sample CSV** then **Upload CSV**, or **Add row**).
3. Every new row starts as **Approval Pending**.
4. The team clicks **Notify new rows** to tell the brand. There are **no automatic emails**.
5. **Brand reviews** the broken links and the proposed fixes. It **approves** a row, or **disapproves** it with a comment in **Client Comments**.
6. After a disapproval, the team reads the comment, **updates the action or the redirect URL** if needed, and replies in **DIAS Comments**. The row goes back to **Approval Pending**.
7. The team clicks **Notify changes** to tell the brand about the updates.
8. Once the fix is done on the website (for example the 301 redirect is in place), the row is marked **Live on Website**.
9. When the brand has finished reviewing, the brand clicks the **Notify** button on its dashboard to email the brand's assigned team lead.

Each change to a row updates its **Last Updated** time.

---

## 3. Roles and Scope

| Role | Brands in scope | What they can do | What they cannot do |
|------|-----------------|------------------|---------------------|
| **Admin** | All brands | Same as the Team Lead, including adding **DIAS Comments** at any time | Cannot approve or disapprove |
| **SEO Team Lead** | Assigned brands only | Select brand and month, upload CSV, **Add row**, **edit** and **delete** rows, change status with the dropdown (**Approval Pending** and **Live on Website** only), add **DIAS Comments** at any time, send **Notify new rows** and **Notify changes** | Cannot set **Approved** or **Disapproved**, even on the brand's behalf |
| **SEO Team Member** | Assigned brands only | Same as the Team Lead | Same as above |
| **Brand user** | Own brand only | View rows, **approve** or **disapprove**, mark **Live on Website**, write **Client Comments** **only when disapproving** (applies on all pages), click the dashboard **Notify** button | Cannot add, edit or delete rows |

Notes:

- Comments from the team and from the brand sit in **separate columns**, so it is clear who said what. **DIAS Comments** are the internal team's. **Client Comments** are the brand's.
- Each column can hold **several comments**, each shown with **who wrote it**.
- The status dropdown, the admin and brand rights, and the Live rule are the same as on [Classified](classified.md) and [Web 2.0](web-2.md).

---

## 4. Status Control – Who Can Change Status, and To What

### 4.1 Status definitions

Standard status names are used on every page.

| Status | Meaning |
|--------|---------|
| **Approval Pending** | Default for every new row. Waiting for the brand's review. Also the state **any edited row** returns to. |
| **Approved** | The brand accepted the broken link and the proposed fix. |
| **Disapproved** | The brand did not accept the proposed fix and left a comment in **Client Comments** explaining what to change. |
| **Live on Website** | The fix is done on the website. |

### 4.2 Who changes status, and how

The status is a **dropdown on each row**.

| Change | Done by | How |
|--------|---------|-----|
| New row → **Approval Pending** | System | Automatic on upload or Add row |
| Approval Pending → **Approved** | Brand user | Approves the row |
| Approval Pending → **Disapproved** | Brand user | Disapproves and writes a Client Comment |
| **Any status → Approval Pending** | System | Automatic whenever the row is **edited** (for example the action or the redirect URL changes), whether it was Approved, Disapproved, Live on Website or Approval Pending (applies on all pages) |
| Team sets **Approval Pending** | Team Lead or Team Member | From the status dropdown. This is a status change, not an edit of the row |
| Approved → **Live on Website** | Team Lead, Team Member or brand user | After the fix is done on the website |

### 4.3 Rules to remember

- A disapproval needs a comment.
- Adding a comment never changes a row's status.
- The disapprove → edit → resubmit cycle repeats until the brand approves.
- A row can be marked **Live on Website** only if it is **Approved**.
- Changing the status with the dropdown does **not** reset the row to Approval Pending. Editing the row does.

---

## 5. Runbook – Internal Team (Team Lead and Team Member)

### 5.1 Select brand and month

1. Select the brand in the top brand picker.
2. Select the month with the month selector. **Confirm the month before adding rows**, because additions apply to the selected month.

### 5.2 Add entries

**Option A – Upload a CSV**

1. Click **Sample CSV** and use it as the template. The columns are `Page URL`, `Broken Link`, `Reference Screenshot`, `Action To be Taken` and `URL for Redirection`.
2. Fill one broken link per row.
3. Click **Upload CSV** and choose the file.

**Option B – Add row**

1. Click **Add row**.
2. Fill the fields and save.

| Field | Meaning | Required? |
|-------|---------|-----------|
| **Page URL** | The page where the broken link appears | Yes |
| **Broken Link** | The link that is broken | Yes |
| **Reference Screenshot** | A screenshot of the issue, if there is one. In the CSV it is an image link. In the form it is an upload | Optional |
| **Action To be Taken** | The fix, for example *301 redirection* or *Removal*. Other actions exist | Yes |
| **URL for Redirection** | Where the broken link should redirect to | Optional. Filled for redirect actions |

| Rule | What happens |
|------|--------------|
| Link format | **Page URL**, **Broken Link** and **URL for Redirection** (when filled) must be valid `https://` URLs |
| Duplicate | The **same Page URL with the same Broken Link cannot be added twice for a brand in the same month**. An error is shown. **In different months it is allowed** |
| Invalid file | The upload is **rejected** with a clear reason |
| Valid rows | Appear in the table, each as **Approval Pending** |

### 5.3 Read the table

| Column | Behaviour |
|--------|-----------|
| **#** | The row number |
| **Page URL**, **Broken Link**, **URL for Redirection** | Clickable links that open in a new tab |
| **Reference Screenshot** | The screenshot, or a dash if none was added |
| **Action To be Taken** | The fix chosen for the row |
| **DIAS Comments** | Comments from the team, with a comment icon to add or view them |
| **Client Comments** | Comments from the brand. A dash means none yet |
| **Status** | Dropdown on each row |
| **Last Updated** | The date and time of the latest change to the row, for example *"2 Nov 2026, 1:54 pm"*. It fills in **automatically** whenever the row is added or changed. **Nobody enters it** |
| **Actions** | **Pencil** (edit) and **bin** (delete), internal team only |

### 5.4 After a disapproval

1. Read the brand's **Client Comments** on the row.
2. Click the **pencil** icon and **update the action or the redirect URL** if needed, then save. The row goes back to **Approval Pending**.
3. Reply in **DIAS Comments**.
4. Click **Notify changes** (see 5.7).

### 5.5 Delete a row

1. Click the **bin** icon and confirm in the confirmation message.
2. A deleted row **cannot be recovered**. Rows in **any status, including Live on Website**, can be deleted.
3. Deleting a row is **not** counted under **Notify changes**.

### 5.6 Mark Live on Website

1. Confirm the fix is done on the website (for example the 301 redirect is in place) and the row is **Approved**.
2. Set the status to **Live on Website** with the dropdown. The brand user can also do this.

### 5.7 Emails

**No emails are sent automatically.** Two buttons sit below the table, each with a counter. They are for the internal team and work as on [Classified](classified.md).

| Email | Goes to | When | Button |
|-------|---------|------|--------|
| **Notify new rows** | Brand | Emails the brand about entries **added since the last notification** | **Notify new rows (count)**. The counter shows how many new rows are waiting |
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

1. Open **Deployment → Owned Channels → Broken Links** and select the month.
2. For each row, read the **Page URL** (where the broken link is), the **Broken Link**, the **Action To be Taken** and the **URL for Redirection**. Click a link to open it and check it.
3. **Approve** the row if the fix is correct.
4. **Disapprove** it if it needs a change, and write a comment in **Client Comments** saying what to change. This is the only time you can comment.
5. After the team updates the row, it returns to **Approval Pending**. Review it again.
6. When the fix is done on the website, you or the team can mark the row **Live on Website** (the row must be **Approved**).
7. When you have finished reviewing, click the **Notify** button on your dashboard. This sends your brand's assigned team lead a plain-text summary with the approved and disapproved counts.

---

## 7. What the Page Looks Like Today (Observed)

The UI document ([UI/broken-links.md](../UI/broken-links.md)) records a view with a month selector, a count label and a **10-column** table (#, Page URL, Broken Link, Reference Screenshot, Action To be Taken, URL for Redirection, DIAS Comments, Client Comments, Status, Last Updated). The status was a plain badge, and there was **no status dropdown, Add row, Upload, Edit, Delete or Notify control**. It was explored with a Sub-Admin account.

Differences from the flow above:

- There was **no Actions column**, no **Sample CSV**, **Upload CSV** or **Add row** button, and no Notify buttons.
- The statuses seen were **Live on Website** and **Pending**. **Pending** is the short name for **Approval Pending**.
- The **Reference Screenshot**, **DIAS Comments** and **Client Comments** cells were plain text ("—") on every row, with no button to add a comment.
- Only two actions were seen: **301 redirection** and **Removal**. The flow says other actions exist.
- All 15 rows showed the **same Last Updated time**. This may reflect when the data was loaded, not when each fix was made.
- The page appeared in the sidebar **only for some brands**, together with Robot.txt and Sitemap. The flow does not describe which brands see it.
- The bottom of the page, where the **Notify** buttons would sit, was not seen.

The cause of the missing controls is **not confirmed**. It may depend on the role used when the page was observed, or on features not being released at that time.

## 8. Troubleshooting

| Situation | What to do |
|-----------|------------|
| Upload rejected | Read the reason shown. Download the sample CSV again and match its five columns. |
| Link rejected | Use a valid `https://` URL in **Page URL**, **Broken Link** and **URL for Redirection**. |
| Duplicate error | The same Page URL with the same Broken Link already exists for this brand in this month. The same pair in a different month is allowed. |
| Row went back to Approval Pending | The row was edited. Every edit resets the status. |
| Cannot set Live | The row must be **Approved** first. |
| Cannot set Approved or Disapproved | Only the brand user can do this. |
| Last Updated looks wrong | It fills in automatically on every add or change. It cannot be edited. |
| Brand did not get an email | No emails are sent automatically. Click **Notify new rows** or **Notify changes**. |
| Counter shows (0) | Nothing is waiting to be sent. |
| Team lead did not get the disapproval summary | The brand user must click the **Notify** button on their dashboard. |
| Brand cannot comment | Brands can comment only when disapproving. |
| Page missing from the sidebar | The page appeared only for some brands when observed. Check the brand selected. |
