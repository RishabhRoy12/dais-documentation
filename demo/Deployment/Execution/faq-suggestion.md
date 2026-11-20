# FAQ Suggestion – Execution Runbook

> Path in the platform: **Execution → Owned Channels → FAQ Suggestion** (`/execution/faq-suggestion`)
>
> This document explains **how the work is carried out**: who does what, in which order, and how status changes. For screen layout, columns, filters and observed data, see the UI document: [UI/faq-suggestion.md](../UI/faq-suggestion.md). For the workflow as a flowchart, see [Flowcharts/faq-suggestion.md](../Flowcharts/faq-suggestion.md).
>
---

## 1. Purpose

The FAQ Suggestion page is used to suggest **frequently asked questions and answers** for pages of a brand's website. Work is organised **per brand and per month**. Each row is one Page URL with one Suggested Question and its Suggested Answer.

The internal team prepares the suggestions, the brand approves or disapproves each one, and the row is marked live once the FAQ is added to the website.

## 2. End-to-End Flow

1. Internal team selects the **brand** and the **month**.
2. Team adds rows (**Download Sample CSV** then **Upload CSV**, or **Add Manually**).
3. Every new row starts as **Approval Pending**.
4. The team clicks the **send email** button below the table to notify the brand. There are **no automatic emails**.
5. **Brand reviews** each suggested question and answer and **approves** or **disapproves** it (a disapproval needs a comment).
6. After a disapproval, the team reads the comment, **edits the question or answer** with the pencil icon and resubmits. The row returns to **Approval Pending**.
7. Steps 5–6 repeat until the brand approves.
8. Once the FAQ is added to the website, the row is marked **Live on Website** (by the team or the brand).
9. The team clicks the **send email** button again to notify the other side of the changes.

---

## 3. Roles and Scope

| Role | Brands in scope | What they can do | What they cannot do |
|------|-----------------|------------------|---------------------|
| **SEO Team Lead** | All brands | Select brand and month, upload CSV, Add Manually, edit, **delete** (with confirmation), add comments, mark Live, send the email | Cannot approve or disapprove |
| **SEO Team Member** | Assigned brands only | **Same access as the Team Lead**, including the send email button | Cannot approve or disapprove |
| **Brand user** | Own brand only | View rows, **approve** or **disapprove** each FAQ (a disapproval needs a comment), mark Live. Can comment **only when disapproving** (this applies on all pages) | Cannot add, edit or delete rows |
| **Admin** | All brands | Same as the Team Lead, including **delete** | Cannot approve or disapprove |

Notes:

- Team Members see **only their own brands**.
- The **internal team** can delete a row. A **confirmation** is asked first.
- Team Leads and Team Members can **add comments** (and edit, delete and mark Live, as in the table above). They cannot approve or disapprove.
- A row can hold **several comments**. Hovering shows all of them and **who wrote each one**.

---

## 4. Status Control – Who Can Change Status, and To What

### 4.1 Status definitions

Standard status names are used on every page. The page's filter shows **Live on Website**. The product flow calls the same status **Live** (short alias).

| Status | Meaning |
|--------|---------|
| **Approval Pending** | Default for every new row. Waiting for the brand's review. Also the state a row returns to after the team resubmits an edited entry. |
| **Approved** | The brand accepted the FAQ. The team can add it to the page. |
| **Disapproved** | The brand did not accept the FAQ and left a comment explaining what to change. |
| **Live on Website** (also called **Live**) | The FAQ has been added to the website. |

### 4.2 Who changes status, and how

| Change | Done by | How |
|--------|---------|-----|
| New row → **Approval Pending** | System | Automatic on upload or manual add |
| Approval Pending → **Approved** | Brand user | Approves the FAQ |
| Approval Pending → **Disapproved** | Brand user | Disapproves and adds a comment |
| **Any status → Approval Pending** | System | Automatic whenever the internal team **edits** the row, whether it was Approved, Disapproved, Live on Website or Approval Pending |
| Approved → **Live on Website** | Team or brand user | Marks the row Live after the FAQ is on the website |

### 4.3 Rules to remember

- A disapproval needs a comment. Brand users can comment **only when disapproving**.
- **Any edit resets the row to Approval Pending**, whatever its status, so the brand reviews it again.
- The disapprove → edit → resubmit cycle repeats until the brand approves.
- A row can be marked **Live on Website** only if it is **Approved**.

---

## 5. Runbook – Internal Team

### 5.1 Select brand and month

1. Select the brand in the top brand picker.
2. Select the month with the month selector (for example *October 2026*). **Confirm the month before adding rows**, because additions apply to the selected month.

### 5.2 Add rows

**Option A – Upload a CSV**

1. Click **Download Sample CSV** and use it as the template.
2. Fill one row per suggestion.
3. Click **Upload CSV** and choose the file.

**Option B – Add Manually**

1. Click **Add Manually**.
2. Fill in the three fields below and save. The exact form is not described in the flow *(not verified)*.

| Field | Meaning |
|-------|---------|
| Page URL | The page where the FAQ is meant to go |
| Suggested Question | The proposed FAQ question |
| Suggested Answer | The proposed answer |

Rules (from the flow):

| Situation | What happens |
|-----------|--------------|
| Invalid file | The **whole upload is rejected** with a clear reason |
| Duplicate entry | An error is shown. A duplicate is the **same Page URL with the same Suggested Question** |
| Several questions for one URL | Allowed. Each question is its own row |
| Valid rows | Appear in the table, each as **Approval Pending** |

### 5.3 Read the table

| Item | Behaviour |
|------|-----------|
| Page URL | Opens the page in a new tab |
| Suggested Question / Suggested Answer | Long answers are cut short. A **copy icon** next to each answer copies it |
| Status | Approval Pending, Approved, Disapproved or Live on Website |
| Comment | Feedback on the row. Several comments are possible. **Hover** to see all of them and who made each |
| Actions | **Pencil** (edit) and **bin** (delete) |
| Search | Search by URL, question or answer |
| Filter | Filter by status |

### 5.4 After a disapproval

1. Read the brand's **comment** on the row.
2. Click the **pencil** icon and edit the question or answer.
3. Resubmit. The row goes back to **Approval Pending**.

### 5.5 Delete a row

1. Click the **bin** icon on the row.
2. Confirm in the confirmation message. A deleted row **cannot be recovered**. Rows in **any status, including Live on Website**, can be deleted.

### 5.6 Mark Live on Website

1. Confirm the FAQ is added to the website.
2. Mark the row **Live on Website**. The team or the brand can do this.

### 5.7 Emails

**No emails are sent automatically.** All emails are sent manually with the **send email** button below the table, in the same way as on Meta Tags (see [Meta Tags §5.5](meta-tags.md)).

| Topic | Detail |
|-------|--------|
| Who can use it | Team Leads, and Team Members for their own brands |
| What one click sends | **Everything changed since the last click**, for the selected brand and month |
| Email content, CC and BCC | A separate flow, **not covered** here |
| **Disapproval summary** (to the brand's assigned team lead) | Not sent by this button. The brand user sends it with the **Notify** button on their dashboard after reviewing. **Plain text**, with **only the approved and disapproved counts**. One click covers **all pages** |

Whether this page has one button or two is not stated *(not verified)*.

---

## 6. Runbook – Brand User

1. Open **Execution → Owned Channels → FAQ Suggestion** and select the month.
2. For each row, read the **Suggested Question** and **Suggested Answer**. Use the Page URL link to open the page.
3. **Approve** the FAQ if it is correct. The team can then add it to the page.
4. **Disapprove** it if it needs a change, and **add a comment** saying what to change.
5. After the team edits the entry, the row returns to **Approval Pending**. Review it again.
6. When the FAQ is on the website, the row can be marked **Live on Website** by the team or by you.
7. When you finish reviewing, click the **Notify** button on your dashboard. It emails your brand's assigned team lead a plain-text **Disapproval summary** with the approved and disapproved counts, covering all pages.

---

## 7. What the Page Looks Like Today (Observed)

The UI document ([UI/faq-suggestion.md](../UI/faq-suggestion.md)) records an observed view that was **read-only**. It had a month selector, a search box, a status filter and a **5-column** table, with **no Add, Upload, Approve or Disapprove controls**. All 17 rows seen were Approval Pending.

Differences from the flow above:

- There was **no Actions column** (no pencil or bin).
- The **Comment** column showed "—" on every row and had **no Add comment** link.
- The page used the name **Live on Website**.

The cause is **not confirmed**. It may depend on the role or brand used when the page was observed, or on the features not being released at the time.

## 8. Troubleshooting

| Situation | What to do |
|-----------|------------|
| Upload rejected | Read the reason shown. Download the sample CSV again and match its format. |
| Duplicate error | The same Page URL and question already exist for the month. Remove it from the file, or edit the existing row. |
| Empty table | Check the month, search box and status filter. The current month may have no rows. |
| Cannot approve or disapprove | Team Leads and Team Members cannot do this. Only the brand can. |
| Row stuck on Approval Pending | The brand has not reviewed it yet, or it was edited. Every edit resets the status. |
| Team lead did not get the disapproval summary | The brand user must click the **Notify** button on their dashboard after reviewing. |
| Brand did not get an email | No emails are sent automatically. Click the send email button below the table. |
