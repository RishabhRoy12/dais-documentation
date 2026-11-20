# Meta Tags – Execution Runbook

> Path in the platform: **Execution → Owned Channels → Meta Tags** (`/execution/meta-tags`)
>
> This document explains **how the work is carried out**: who does what, in which order, and how status changes. For screen layouts, buttons, columns and dialogs, see the UI document: [UI/meta-tags.md](../UI/meta-tags.md). For the workflow as a flowchart, see [Flowcharts/meta-tags.md](../Flowcharts/meta-tags.md).

---

## 1. Purpose

The Meta Tags page is used to improve the **URL, Title, Meta Description and H1** of a brand's website pages. Work is organised **per brand and per month**. Each row is one website page with its keywords, its current values and the recommended values.

The internal team prepares recommendations, the brand approves or rejects each one, and the team marks approved rows as live once they are published.

## 2. End-to-End Flow

1. Internal team selects the **brand** and the **month**.
2. Team adds pages (**upload** or **Add Item**).
3. **AI fills** any missing recommendations.
4. **Team Lead reviews** the AI output and corrects it.
5. Team clicks **Notify new rows** – the brand is emailed.
6. **Brand reviews** each recommendation (approve or reject, with remarks) and submits.
7. Status updates automatically.
8. Team **updates rejected recommendations** and clicks **Notify changes**.
9. Brand reviews the updated recommendations again.
10. When a row is **Approved** and published on the website, the team marks it **Live on Website**.

---

## 3. Roles and Scope

| Role | Brands in scope | What they can do | What they cannot do |
|------|-----------------|------------------|---------------------|
| **Admin** | All brands | Upload, add, edit, delete, generate with AI, review AI changes, change column layout, mark Live, send Notify emails | – |
| **SEO Team Lead** | All brands | Same as Admin on this page, including the Review AI changes window | – |
| **SEO Team Member** | Assigned brands only | Upload, add, edit, delete, generate with AI, change column layout, mark Live, send Notify emails | Does not get the Review AI changes window |
| **Brand user** | Own brand only | View all rows of their brand, approve or reject each recommendation, write remarks, submit the month review | Cannot add, edit or delete rows, cannot change column layout, cannot generate, cannot mark Live, cannot edit Live rows |

Notes:

- Internal users(SEO Team Leads and Team Members) can change or add data **only for the brands assigned to them**.
- Brand users never see internal staff names; updates by staff are shown as **DAIS**.
- These rules are enforced by the platform, not only hidden on screen.

---

## 4. Status Control – Who Can Change Status, and To What

Status is **never typed in**. The platform recalculates it every time a row is saved, based on the brand's answers. The only manual status action is **Mark Live on Website**.

### 4.1 Status definitions

| Status | Meaning |
|--------|---------|
| **Approval Pending** | Default for new rows. At least one recommendation is not yet answered, or the row has no recommendations. |
| **Disapproved** (shown as *Needs Update* on the summary card; earlier called *Changes Requested*) | At least one recommendation is rejected (disapproved). |
| **Approved** | Every recommendation on the row is approved. |
| **Live on Website** | Approved row published on the website and marked Live by the team. |

Only recommendations that have a value and are in a **visible column** count towards the status. Empty recommendations are ignored.

### 4.2 Who changes status, and how

| Change | Done by | How |
|--------|---------|-----|
| New row → **Approval Pending** | System | Automatic on creation |
| Approval Pending → **Approved** | Brand user | Approves every recommendation on the row and submits |
| Approval Pending / Approved → **Disapproved** | Brand user | Rejects at least one recommendation, adds remarks, submits |
| Disapproved → **Approved** | Brand user | Approves all recommendations after the team has updated the rejected ones |
| Approved / Disapproved → **Approval Pending** | Internal team (indirectly) | Editing a recommended value clears the brand's answer for that field, so the row needs a fresh review. If another field is still rejected, the row stays Disapproved. |
| **Any status → Approval Pending** | System | Automatic whenever the internal team **edits** the row, whether it was Approved, Disapproved, Live on Website or Approval Pending |
| **Approved** → **Live on Website** | Internal team | Mark Live action on an Approved row |
| Any row → **Approval Pending** (re-evaluated) | System | When a hidden Recommended column is shown again, brand answers for that field are cleared for all rows of the brand and statuses are recalculated |

### 4.3 Rules to remember

- **The status can set Live on Website by internal team or brand user**, and only on a row that is already Approved and was not edited in the same save.
- **A rejection (disapproval) always needs remarks.** Brand users can comment **only when disapproving** (this applies on all pages).
- **Any edit resets the row to Approval Pending**, whatever its status.
- Standard status names are used on every page: Approval Pending, Approved, Disapproved, Live on Website (the short names *Pending* and *Live* are only aliases).
- Removing a recommended value also clears its answer.
- Hiding a Recommended column removes it from brand review and from the status calculation.

---

## 5. Runbook – Internal Team

For the screens and buttons mentioned below, see [UI/meta-tags.md](../UI/meta-tags.md).

### 5.1 Select brand and month

1. Select the brand in the top brand picker.
2. Select the month in the page header. **Always confirm the month before uploading or adding items**, because all additions apply to the selected month and re-upload matching only works inside that month.

### 5.2 Add pages

**Option A – Upload (CSV / Excel)**

1. Click **Download Sample CSV** and use it as the template. See UI doc §3.3.
2. Fill the file. Headers must match the sample **exactly and in the same order**; otherwise the whole file is rejected.
3. Click **Upload Meta Tags** and choose a `.csv`, `.xlsx` or `.xls` file. Rows are saved immediately; there is no confirm step.

Upload rules:

| Topic | Rule |
|-------|------|
| Sheets | Only the first sheet of an Excel file is read. Empty lines are ignored. |
| Required value | **Current URL** is required. Rows without it are skipped. |
| Optional values | Current Title, Description and H1 may be blank. Recommended values may be blank (AI will fill them). |
| Keywords | One keyword per line. Extra keywords for the same page go on the following lines with all other columns blank. |
| Avg. Monthly Searches | Must be a number. Otherwise it is left blank. |
| Approval and Status columns | Present for format only. Values are **not** imported. Approvals are given on the platform and status is calculated by the platform. |
| Remarks | Saved on new rows. Existing remarks are not changed. |
| Sr No | Assigned automatically by the platform. |
| New vs existing rows | A row is matched with an existing row in the **same month** by **Current URL plus keywords**. A match updates that row; no match adds a new row. |
| Blank values on update | Blank Current Title, Description or H1 keep the saved value. **Blank Recommended values and blank keywords overwrite what is saved.** |

**Safe practice for re-upload:** keep all Recommended cells filled with the wording you want to keep. A blank Recommended cell clears the saved value, and AI will then fill it again, replacing earlier wording.

After upload:

- A summary shows how many rows were added and updated, how many were skipped for a missing Current URL, and how many items need AI generation.
- Detailed row-level warnings are **not** displayed; only the final summary appears.
- Uploads save **row by row**. If an upload fails part-way, earlier rows stay saved. Check the table, then re-upload the file if needed (matching by URL plus keywords will update rather than duplicate).

**Option B – Add Item**

1. Click **Add Item** and fill the dialog (UI doc §3.5). Keywords can be picked from suggestions based on the brand's keyword ranking.
2. Click **Save**. The row is saved in the selected month with source **Manual**.

### 5.3 AI fills missing recommendations

| Topic | Detail |
|-------|--------|
| When it runs | Automatically after an upload for rows missing any recommendation, or when you click **Generate missing (n)** |
| Who can run it | Internal team only |
| How it runs | One row at a time from your browser, with a banner showing progress |
| What it fills | **Only missing fields.** Existing recommendations are never overwritten. |

> **Do not refresh or close the page while generation is running.** Leaving can stop it before all fields are filled. If it stops, click **Generate missing (n)** to resume with the remaining rows.

Writing rules the AI follows:

| Field | Rule |
|-------|------|
| Title | 50–60 characters, primary keyword near the start, brand suffix only if it fits, no keyword stuffing or all caps |
| Description | 140–160 characters, primary plus one secondary keyword, clear value and a soft call to action, active voice |
| H1 | One clear heading, 20–70 characters, matches search intent, similar to but different from the title, no brand suffix |
| URL | Same scheme and domain as the current URL; short, lowercase, hyphenated slug with the primary keyword; no stop words, dates, IDs, parameters or file extensions; unchanged if already optimal |
| Keywords | Highest-search keyword is primary; otherwise the first keyword |
| Accuracy | Stays on the brand and page topic; never invents facts, prices, offers or statistics |

Outcomes:

- **Success:** "Generation complete".
- **Partial:** "Generation finished with errors – x filled, y failed". Use **Generate missing (n)** to retry.
- **AI errors** (busy, credits exhausted, failed, unreadable answer): wait a moment and retry. If credits are exhausted, escalate to an Admin.

### 5.4 Team Lead review of AI output

1. When a generation run finishes, the **Review AI changes** window opens automatically for **Admins and SEO Team Leads**. SEO Team Members do not get this window.
2. Check each row that was filled. Fields written by AI carry an **AI filled** tag.
3. Edit any value and click **Save** on that row.
4. The window can be reopened with **Review changes**. It exists only for the current session and is cleared on refresh.

Review the AI output **before** notifying the brand.

### 5.5 Notify the brand

Notify buttons appear below the table for Admins, SEO Team Leads, and SEO Team Members of the assigned brand. Counts refresh automatically.

| Button | Use when | Counts | Email subject |
|--------|----------|--------|---------------|
| **Notify new rows (n)** | New rows are ready for the brand's first review | Rows added by upload or Add Item since the last "new rows" email | DAIS added new Meta Tags suggestions for {brand} ({month}) |
| **Notify changes (n)** | You have updated rows after the brand's feedback | Rows edited by the team after the brand left feedback, since the last "changes" email | DAIS updated your Meta Tags suggestions as requested ({month}) |

Email behaviour:

- One email is sent to **every external user of that brand**.
- The sender is the platform's AI agent. Replies and copies go to the Customer Success and Product teams.
- Each send is logged, and the last send time per brand, month and type is stored.
- Result messages: **"Brand notified"** with the number of emails sent, **"Nothing sent"** (nothing pending, or no recipients), or **"Notify failed"**.

Brand-side email (sent by the brand user, not the team):

| Email | Goes to | When | Button |
|-------|---------|------|--------|
| **Disapproval summary** | Brand's **assigned team lead** | When the brand user clicks **Notify** on their dashboard after reviewing. **Plain text** with only the approved and disapproved counts. One click covers **all pages** | **Notify** button on the brand user's dashboard |

### 5.6 Update rejected recommendations

1. Filter your attention to rows with **Disapproved** status and read the brand's **Remarks**.
2. Click **Edit** on the row, correct the recommended values, and **Save**.
3. Saving a changed recommended value **clears the brand's answer for that field**, so the brand must review it again.
4. When all corrections are done, click **Notify changes (n)**.

> There is no search or filter on this page. The page has no export. Use the summary cards and the Status column to find rows.

### 5.7 Mark Live on Website

1. Confirm the approved changes are published on the website.
2. On an **Approved** row, click the **rocket** icon in the Actions column.
3. The status becomes **Live on Website** and the row is locked for the brand.

The rocket appears only on Approved rows. The platform refuses Live on any other status.

### 5.8 Edit, delete and column layout

- **Edit:** any edit sets the row back to **Approval Pending**, whatever its status. Changes to any recommended value also reset the brand's answer for that field.
- **Delete:** removes the row and the brand's answers for it. This cannot be undone.
- **Column layout:** the team can reorder columns, show or hide columns, and reset to default. The layout is saved **per brand** and is the same for everyone viewing that brand, including brand users.
  - At least one column must stay visible.
  - Hiding a Recommended column removes it from brand review and from status calculation.
  - Showing a hidden Recommended column again **clears brand answers for that field for all rows of the brand**. Check with the brand before doing this.

---

## 6. Runbook – Brand User

1. Open **Execution → Owned Channels → Meta Tags** and select the month.
2. All rows of your brand are visible. A recommendation that has not been filled yet appears empty and cannot be reviewed; the row stays **Approval Pending** until the team fills it in.
3. For each recommended value (URL, Title, Description, H1), tick **Approve** to approve it. Leave it unticked or use **Reject** to reject it.
4. Use **Approve all** or **Reject all** on a row to set every visible recommendation on that row at once.
5. Write **Remarks** for any row with a rejected recommendation. Remarks are mandatory in this case. You can comment **only when disapproving**.
6. Click **Approve** or **Reject** in the bottom bar to submit. **Nothing is saved until you submit.** All changed rows for the month are submitted together.
7. The status of each row updates automatically.
8. After the team revises rejected rows, you receive a "changes" email. Open the page and review the updated recommendations again.
9. Rows marked **Live on Website** are locked and cannot be changed.
10. When you finish reviewing, click the **Notify** button on your dashboard. It emails your brand's assigned team lead a plain-text **Disapproval summary** with the approved and disapproved counts, covering all pages.

Submit checks:

| Situation | What happens |
|-----------|--------------|
| Nothing changed | "No review changes – select or reject at least one suggestion before submitting." |
| **Approve** clicked while something is rejected | Refused. Use **Reject** to submit a review that contains rejections. |
| **Reject** clicked while nothing is rejected | Refused. Reject at least one suggestion first. |
| Rejected row without remarks | "Remarks required – add remarks for the item before submitting." |
| Success | "Month review submitted – n items updated." |

Scope reminder for brand users: only approvals and remarks can be changed. Hidden-column recommendations cannot be reviewed and do not count towards status.

---

## 7. Summary Cards and What They Count

See the UI doc §3.2 for the layout.

| Card | Counts |
|------|--------|
| Total Pages | All rows in the selected month |
| Approved | Rows that are Approved or Live on Website |
| Pending Approval | Rows in Approval Pending |
| Needs Update | Rows in Disapproved status |


---

## 8. Data and Storage (Generalised)

The platform keeps:

- The **month-wise Meta Tags records** (keywords, current and recommended values, brand answers, remarks, status, source, who last updated and when).
- A **column layout** per brand.
- A **backup** of the imported sheet rows.
- A **notification record** (last send per brand, month and email type) and an **email log**.

Permissions are checked by the platform for every read and write, in line with section 3.

---

## 9. Troubleshooting

| Message / situation | What to do |
|---------------------|------------|
| "Headers must match the sample CSV exactly" | Download the sample file again and use its headers in the same order. |
| "Every row is missing Current URL" | Add the Current URL to the rows and upload again. |
| Rows missing after upload | Rows without Current URL are skipped. Check the skipped list in the summary. |
| Recommendations disappeared after re-upload | Blank Recommended cells in the file overwrite saved values. Re-upload with those cells filled. |
| New rows created instead of updated | The URL or keywords in the file differ from the saved row, or the wrong month was selected. Check both. |
| AI generation stopped | Do not refresh. Click **Generate missing (n)** to resume. |
| "AI is busy right now" | Retry after a moment. |
| "AI credits are exhausted" | Contact an Admin. |
| "Could not save" | Read the reason shown (for example a field format issue) and correct it. |
| "Remarks required" (brand) | Add remarks for each row with a rejection. |
| Notify shows "Nothing sent" | No pending rows, or the brand has no external users. |
| Team lead did not get the disapproval summary | The brand user must click the **Notify** button on their dashboard after reviewing. |
| Row went back to Approval Pending | It was edited. Every edit resets the status. |
| Rocket icon not visible | The row is not Approved, or you do not have access to the brand. |
| Brand cannot edit a row | The row is Live on Website, or the field is not an approval or remark. |
| Failed to load meta tags | Retry later. |
