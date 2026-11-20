# Schema Markup – Execution Runbook

> Path in the platform: **Execution → Owned Channels → Schema Markup** (`/execution/schema-markup`)
>
> This document explains **how the work is carried out**: who does what, in which order, and how status changes. For screen layout, cards, columns and observed data, see the UI document: [UI/schema-markup.md](../UI/schema-markup.md). For the workflow as a flowchart, see [Flowcharts/schema-markup.md](../Flowcharts/schema-markup.md).
>
---

## 1. Purpose

The Schema Markup page is used to plan, review and track the **structured data (schema markup)** for pages of a brand's website. Work is organised **per brand and per month**. Each row is one **URL and Missing Schema pair**, with the recommended schema code.

The internal team prepares recommendations, the brand approves or disapproves each one, and the row is marked live once the schema is added to the website.

## 2. End-to-End Flow

1. Internal team selects the **brand** and the **month**.
2. Team adds rows (**CSV upload** or **Add Manually**).
3. Every new row starts as **Approval Pending**.
4. The team clicks the **send email** button below the table to notify the brand. There are **no automatic emails**.
5. **Brand reviews** each suggested schema and **approves** or **disapproves** it (a disapproval needs a comment).
6. After a disapproval, the team reads the comment, **edits the entry** and resubmits. The row returns to **Approval Pending**.
7. Steps 5–6 repeat until the brand approves.
8. Once the schema is added to the website, the row is marked **Live on Website** (by the internal team or the brand).
9. The team clicks the **send email** button again to notify the other side of the changes.

---

## 3. Roles and Scope

| Role | Brands in scope | What they can do | What they cannot do |
|------|-----------------|------------------|---------------------|
| **SEO Team Lead** | All brands | Select brand and month, upload CSV, Add Manually, edit entries, add comments, mark Live, send the email | Cannot approve or disapprove |
| **SEO Team Member** | Assigned brands only | Same as Team Lead on this page | Cannot approve or disapprove |
| **Brand user** | Own brand only | View rows, **approve** or **disapprove** each schema (a disapproval needs a comment), mark Live. Can comment **only when disapproving** (this applies on all pages) | Cannot add, edit or delete rows |
| **Admin** | All brands | Same as the Team Lead | Cannot approve or disapprove |

Notes:

- Team Leads and Team Members can **add comments** (and edit entries and mark Live, as in the table above). They cannot approve or disapprove.
- A row can hold **several comments**, including the brand's.
- Any **Approved** row can be marked Live by the **internal team or a brand user**.

---

## 4. Status Control – Who Can Change Status, and To What

### 4.1 Status definitions

| Status | Meaning |
|--------|---------|
| **Approval Pending** | Default for every new row. Waiting for the brand's review. Also the state a row returns to after the team resubmits an edited entry. |
| **Approved** | The brand accepted the schema. The team can implement it on the website. |
| **Disapproved** | The brand did not accept the schema and left a comment explaining what needs to change. |
| **Live on Website** | The schema has been added to the website. |

### 4.2 Who changes status, and how

| Change | Done by | How |
|--------|---------|-----|
| New row → **Approval Pending** | System | Automatic on upload or manual add |
| Approval Pending → **Approved** | Brand user | Approves the schema |
| Approval Pending → **Disapproved** | Brand user | Disapproves and adds a comment |
| **Any status → Approval Pending** | System | Automatic whenever the internal team **edits** the row, whether it was Approved, Disapproved, Live on Website or Approval Pending |
| Approved → **Live on Website** | Internal team or brand user | Marks the row Live after the schema is on the website |

### 4.3 Rules to remember

- Each **URL and schema pair** is approved **on its own**. One URL with several Missing Schema values has one row, and one status, per value.
- A disapproval needs a comment. Brand users can comment **only when disapproving**.
- **Any edit resets the row to Approval Pending**, whatever its status, so the brand reviews it again.
- Standard status names are used on every page: Approval Pending, Approved, Disapproved, Live on Website (the short names *Pending* and *Live* are only aliases).
- The disapprove → edit → resubmit cycle repeats until the brand approves.
- Only **Approved** rows can be marked Live.

---

## 5. Runbook – Internal Team

### 5.1 Select brand and month

1. Select the brand in the top brand picker.
2. Select the month with the month selector. **Confirm the month before adding rows**, because additions apply to the selected month.

### 5.2 Add rows

**Option A – Upload a CSV**

1. Download the **sample CSV** and use it as the template.
2. Fill one row per URL and schema pair.
3. Upload the file.

**Option B – Add Manually**

1. Click **Add Manually**.
2. Fill in the three fields below and save.

| Field | Meaning |
|-------|---------|
| Website Page URL | The page that needs the schema |
| Missing Schema | The schema type missing on the page, **chosen from a dropdown** of standard schema names. The page showed **FAQ Schema**; the full list was not seen *(not verified)* |
| Recommended Schema | The schema code, written as **JSON-LD** |

Rules (from the flow):

| Situation | What happens |
|-----------|--------------|
| Invalid file | The **whole upload is rejected** with a specific reason |
| Same URL twice under the same schema | A **duplicate error** is shown |
| Same URL under different schemas | Allowed. Each pair is approved separately |
| Recommended Schema | **Checked as JSON-LD** for both CSV and manual entries. What exactly is rejected is not stated *(not verified)* |
| Valid rows | Appear in the table, each as **Approval Pending** |

### 5.3 Read the table

| Item | Behaviour |
|------|-----------|
| Recommended Schema | A short code preview. **Hover** to see the full code. The **Copy code** button copies it. |
| Older entries | Entries that were Google Docs links show as **Open Document** |
| Status | Approval Pending, Approved, Disapproved or Live on Website |
| Comment | Holds feedback on the row. A row can have several comments. |

### 5.4 After a disapproval

1. Read the brand's **comment** on the row.
2. Edit the entry (for example, correct the JSON-LD).
3. Resubmit. The row goes back to **Approval Pending**.

### 5.5 Mark Live on Website

1. Confirm the schema is added to the website.
2. On an **Approved** row, mark it **Live on Website**. The internal team or the brand can do this.

### 5.6 Emails

**No emails are sent automatically.** All emails are sent manually with the **send email** button below the table, in the same way as on Meta Tags (see [Meta Tags §5.5](meta-tags.md)).

| Topic | Detail |
|-------|--------|
| When | Only when the team clicks the button |
| What one click sends | **Everything changed since the last click**, for the selected brand and month |
| To the brand | An update on the team's edits and new rows |
| **Disapproval summary** (to the brand's assigned team lead) | Not sent by this button. The brand user sends it with the **Notify** button on their dashboard after reviewing. **Plain text**, with **only the approved and disapproved counts**. One click covers **all pages** |
| Email content, CC and BCC | A separate flow, **not covered** here |

Whether this page has one button or two (new rows and changes, as on Meta Tags) is not stated *(not verified)*.

---

## 6. Runbook – Brand User

1. Open **Execution → Owned Channels → Schema Markup** and select the month.
2. For each row, check the **Missing Schema** and read the **Recommended Schema** (hover for the full code, or use **Copy code**). Use the Website Page URL link to open the page.
3. **Approve** the schema if it is correct. The team can then implement it.
4. **Disapprove** it if it needs a change, and **add a comment** saying what needs to change.
5. After the team edits the entry, the row returns to **Approval Pending**. Review it again.
6. When the schema is on the website, an **Approved** row can be marked **Live on Website** by the team or by you.
7. When you finish reviewing, click the **Notify** button on your dashboard. It emails your brand's assigned team lead a plain-text **Disapproval summary** with the approved and disapproved counts, covering all pages.

---

## 7. What the Page Looks Like Today (Observed)

The UI document ([UI/schema-markup.md](../UI/schema-markup.md)) records an observed view that was **mostly read-only**. It had a month selector, 4 summary cards (Total Pages, Approved, Approval Pending, Disapproved), a **Search by URL** box and a 6-column table. The only action was **Add comment** → **Send**. There was **no Add Manually, Upload, Approve, Disapprove or Mark Live** control, and only one row (Approval Pending) existed.

Two differences from the flow above:

- The observed page had **no Add or Upload controls and no Approve or Disapprove controls**.
- There was **no Live on Website** summary card.

The cause is **not confirmed**. It may depend on the role or brand used when the page was observed, or on the features not being released at the time.

## 8. Troubleshooting

| Situation | What to do |
|-----------|------------|
| Upload rejected | Read the reason shown. Download the sample CSV again and match its format. |
| Duplicate error | The same URL already exists under that schema for the month. Remove it from the file, or edit the existing row. |
| Recommended Schema rejected | Check the code is valid JSON-LD. |
| Empty table | Check the month and the search box. The current month may have no rows. |
| Cannot approve or disapprove | Team Leads and Team Members cannot do this. Only the brand can. |
| Row stuck on Approval Pending | The brand has not reviewed it yet, or it was edited. Every edit resets the status. |
| Team lead did not get the disapproval summary | The brand user must click the **Notify** button on their dashboard after reviewing. |
| Brand did not get an email | No emails are sent automatically. Click the send email button below the table. |
