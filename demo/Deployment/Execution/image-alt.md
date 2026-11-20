# Image Alt – Execution Runbook

> Path in the platform: **Execution → Owned Channels → Image Alt** (`/execution/image-alt`)
>
> This document explains **how the work is carried out**: who does what, in which order, and how status changes. For screen layout, columns, filters and observed data, see the UI document: [UI/image-alt.md](../UI/image-alt.md). For the workflow as a flowchart, see [Flowcharts/image-alt.md](../Flowcharts/image-alt.md).
>
---

## 1. Purpose

The Image Alt page is used to improve the **ALT text** of images on a brand's website pages. Work is organised **per brand and per month**. Each row is one image on one website page, with its current ALT text and the suggested ALT text.

The internal team prepares suggestions, the brand approves or disapproves each one, and the team marks approved rows as live once the ALT text is updated on the website.

## 2. End-to-End Flow

1. Internal team selects the **brand** and the **month**.
2. Team adds rows (**CSV upload** or **manually**).
3. Every new row starts as **Approval Pending**.
4. **Brand reviews** each suggested ALT text and **approves** or **disapproves** it (a disapproval needs a comment).
5. After a disapproval, the team reads the comment, **edits the Suggested ALT** and resubmits. The row returns to **Approval Pending**.
6. Steps 4–5 repeat until the brand approves.
7. Once the ALT text is updated on the website, the row is marked **Live on Website** (by the team or the brand).
8. The team clicks the **send email** button below the table to notify the other side.

---

## 3. Roles and Scope

| Role | Brands in scope | What they can do | What they cannot do |
|------|-----------------|------------------|---------------------|
| **SEO Team Lead** | All brands | Select brand and month, upload CSV, add rows, edit Suggested ALT, add comments, mark Live, send the email | Cannot approve or disapprove for the brand |
| **SEO Team Member** | Assigned brands only | Same as Team Lead on this page | Cannot approve or disapprove for the brand |
| **Brand user** | Own brand only | View rows, **approve** or **disapprove** each suggestion (a disapproval needs a comment), mark Live. Can comment **only when disapproving** (this applies on all pages) | Cannot add, edit or delete rows |
| **Admin** | All brands | Same as the Team Lead | Cannot approve or disapprove for the brand |

Notes:

- Team Leads and Team Members can **add comments** (and edit Suggested ALT and mark Live, as in the table above). They cannot approve or disapprove on the brand's behalf.
- Internal users can change data only for the brands assigned to them, as on Meta Tags *(not verified for this page)*.

---

## 4. Status Control – Who Can Change Status, and To What

### 4.1 Status definitions

The statuses below come from the page's status filter. Meanings are based on the supplied flow.

| Status | Meaning |
|--------|---------|
| **Approval Pending** | Default for every new row. The suggestion is waiting for the brand's review. Also the state a row returns to after the team resubmits an edited suggestion. |
| **Approved** | The brand accepted the suggested ALT text. The team can implement it on the website. |
| **Disapproved** | The brand did not accept the suggestion and left a comment explaining what should change. |
| **Live on Website** | The ALT text has been updated on the website. |

### 4.2 Who changes status, and how

| Change | Done by | How |
|--------|---------|-----|
| New row → **Approval Pending** | System | Automatic on upload or manual add |
| Approval Pending → **Approved** | Brand user | Approves the suggestion |
| Approval Pending → **Disapproved** | Brand user | Disapproves and adds a comment |
| **Any status → Approval Pending** | System | Automatic whenever the internal team **edits** the row, whether it was Approved, Disapproved, Live on Website or Approval Pending |
| Approved → **Live on Website** | Team or brand user | Marks the row Live after the website is updated |

### 4.3 Rules to remember

- Team Leads and Team Members cannot approve or disapprove for the brand.
- A disapproval needs a comment from the brand. Brand users can comment **only when disapproving**.
- **Any edit resets the row to Approval Pending**, whatever its status, so the brand reviews it again.
- Standard status names are used on every page: Approval Pending, Approved, Disapproved, Live on Website (the short names *Pending* and *Live* are only aliases).
- The cycle of disapprove → edit → resubmit repeats until the brand approves.
- A row can be marked **Live on Website** only if it is **Approved**.

---

## 5. Runbook – Internal Team

### 5.1 Select brand and month

1. Select the brand in the top brand picker.
2. Select the month with the month selector. **Confirm the month before adding rows**, because additions apply to the selected month.

### 5.2 Add rows

**Option A – Upload a CSV**

1. Download the **sample file** first and use it as the template.
2. Fill one row per image with the four fields below.
3. Upload the file.

| Field | Meaning |
|-------|---------|
| Website Page URL | The page where the image appears |
| Image URL | The address of the image |
| Current ALT | ALT text currently on the site |
| Suggested ALT | The recommended ALT text |

Upload rules (from the flow):

| Situation | What happens |
|-----------|--------------|
| Invalid file or wrong format | The **whole upload is rejected** with a clear reason |
| Duplicate entry | An error is shown |
| Valid rows | Appear in the table, each as **Approval Pending** |

Accepted file types, exact error wording and whether row-by-row saving applies are not stated *(not verified)*.

**Option B – Add rows manually**

Add a row with the same four fields. The new row starts as **Approval Pending**. The exact form is not described in the flow *(not verified)*.

### 5.3 After a disapproval

1. Read the brand's **comment** on the row.
2. Edit the **Suggested ALT**.
3. Resubmit. The row goes back to **Approval Pending** for another review.

### 5.4 Mark Live on Website

1. Confirm the ALT text is updated on the website.
2. Mark the row **Live on Website**. The team or the brand can do this.

### 5.5 Send the email

A **manual send email** button sits **below the table**.

| Topic | Detail (from the flow) |
|-------|------------------------|
| What one click sends | Everything that changed **since the last click**, for that brand and month |
| What the brand receives | An update on the team's edits |

The email to the brand's assigned team lead is sent by the brand user, not by this button:

| Email | Goes to | When | Button |
|-------|---------|------|--------|
| **Disapproval summary** | Brand's **assigned team lead** | When the brand user clicks **Notify** on their dashboard after reviewing. **Plain text** with only the approved and disapproved counts. One click covers **all pages** | **Notify** button on the brand user's dashboard |

Email content, CC and BCC are a separate flow and are **not covered** here.

There is one team button. It does not appear to be split into "new rows" and "changes" as on Meta Tags *(not verified)*.

---

## 6. Runbook – Brand User

1. Open **Execution → Owned Channels → Image Alt** and select the month.
2. For each row, compare **Current ALT** with **Suggested ALT**. Use the Website Page URL and Image URL links to check the page and image.
3. **Approve** the suggestion if it is correct. The team can then implement it.
4. **Disapprove** it if it needs a change, and **add a comment** saying what should change.
5. After the team edits the suggestion, the row returns to **Approval Pending**. Review it again.
6. When the ALT text is updated on the website, the row can be marked **Live on Website** by the team or by you.
7. When you finish reviewing, click the **Notify** button on your dashboard. It emails your brand's assigned team lead a plain-text **Disapproval summary** with the approved and disapproved counts, covering all pages.

---

## 7. What the Page Looks Like Today (Observed)

The UI document ([UI/image-alt.md](../UI/image-alt.md)) records an observed view of this page that was **read-only**: it had a month selector, a search box, a status filter and a 6-column table, with **no Add, Upload, Edit, Approve or Comment buttons**. All 53 rows seen were **Approval Pending**.

This does not match the workflow above. The difference may be due to the role or brand used when the page was observed, or the actions may not be released yet. Which one applies is **not confirmed**.

## 8. Troubleshooting

| Situation | What to do |
|-----------|------------|
| Upload rejected | Read the reason shown. Download the sample file again and match its format. |
| Duplicate error | The same entry already exists for the month. Remove the duplicate from the file. |
| Empty table | Check the month, search box and status filter. The current month may have no rows. |
| Cannot approve or disapprove | Team Leads and Team Members cannot do this. Only the brand can. |
| Row stuck on Approval Pending | The brand has not reviewed it yet, or it was edited. Every edit resets the status. |
| Team lead did not get the disapproval summary | The brand user must click the **Notify** button on their dashboard after reviewing. |
