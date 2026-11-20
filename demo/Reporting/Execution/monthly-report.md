# Monthly Reports – Execution Runbook

> Path in the platform: **Reporting › Monthly Reports** (`app.dareaisearch.com/reporting/monthly`)
>
> This document explains **how the page works from end to end**: who does what, in which order, how status changes and what is sent to whom. For the workflow as a flowchart, see [monthly-report-flowchart.md](monthly-report-flowchart.md).
>
> **Source of this document:** the *Monthly Reports working flow* reference (prepared 19 November 2026). The product team has confirmed that everything in it is true. It is a description only: nothing on the dashboard was changed.
>
> **This page is different from the Deployment pages.** It has its **own approval flow, its own statuses and its own roles**. The Deployment rules (CSV upload, Approval Pending / Approved / Disapproved / Live on Website, brand approval, brand dashboard Notify) **do not apply** here. Here the **approver** is an internal person, and the **brand only sees finished, published reports**.

---

## 1. Purpose

The Monthly Reports page is where each brand opens its **monthly performance report**, a Google Slides deck shown inside the platform.

Behind the scenes it is also an **internal approval desk**:

1. An SEO **uploader** adds the report link.
2. The **approver** checks it and either approves it or sends it back with remarks.
3. Only after approval can the uploader click **Notify Client**.
4. That single click **publishes the report** to the brand's page and sends the brand an **email and/or WhatsApp** message.

Brand users only ever see **finished, published reports**. They never see statuses, remarks or who uploaded them.

## 2. End-to-End Flow

| Stage | What happens | Status afterwards |
|-------|--------------|-------------------|
| 1 | Uploader adds the report link | **Pending Approval** (approver is emailed) |
| 2 | Approver reviews: **Approve** or **Request Changes** | **Approved — Ready to Notify** or **Changes Required** |
| 3 | If changes were requested, the uploader fixes the link and resubmits | **Pending Approval** (approver is emailed again) |
| 4 | Uploader clicks **Notify Client** (email and/or WhatsApp) | Report is **published** to the brand immediately |
| 5 | Messages are delivered | **Client Notified** (or a failed or partly failed notification, see section 6) |

Stages 2 and 3 can repeat as many times as needed.

---

## 3. Roles and Scope

| Role | Who (today) | What they can do |
|------|-------------|------------------|
| **Uploader** | Rahul and Arpita | Upload or replace a report link for the brands **assigned to them**. See a list of everything they uploaded. **Notify Client** after approval. Retry a failed message. **Edit or delete only before it is published**. Add remarks to the activity thread. **Cannot approve** |
| **Approver** | Deepak | Sees every brand's submissions in **one approval queue**. Opens and previews each deck. **Approve**, or **Request Changes** with remarks of **at least 50 characters**. **Cannot upload or notify** the brand, and **cannot approve their own upload** |
| **Admin** | Platform admins | **Full access.** Can review (approve or request changes) and notify, for any brand. The **Upload Report** button itself is shown **only to uploaders** |
| **Brand user** | Client logins of the brand, including users assigned extra brands | Sees the **report cards** for their brand or brands and opens them. **Only published reports appear.** No status badges, remarks, uploader names or action buttons |
| **Demo / sample accounts** | Demo brand and forced-demo accounts | See **one sample report (July 2026)** with a demo banner. **Nothing is saved** |

Who is an uploader or approver is decided by a **saved list of workflow roles on the backend**. Which brands an uploader can upload for comes from the **brands assigned to that person**.

---

## 4. Where the Reports Come From

Every card on the page comes from one of two sources, **combined by month**.

| Source | How it works | Used for |
|--------|--------------|----------|
| **Platform uploads** (current way) | Reports uploaded on this page through the approval flow. Saved in the database together with their status, remarks and full activity history | All brands. Every report since the workflow started (**August 2026** onwards) |
| **Master Google Sheet** (older way) | Read live from the **"Monthly Reports"** tab of the master sheet: one row per brand, one column per month (for example "Feb 26"), each cell holding the Slides link. Cells such as *NA*, *"Client work pending"* or *"Started…"* are skipped. If the sheet cannot be read or has nothing for the brand, a **built-in backup list** of older deck links is used | Skin111, Dorset, Ambuja Cement, Asics, Alliance Street, Perona, Chaat Bazaar, Sunstone, Mylo and ACC (sheet). The backup list also covers older months of other brands |

**Combining rule:** if both sources have a report for the **same month**, the **platform-uploaded report wins** and replaces the sheet link on that card.

- Cards are sorted **newest month first**.
- A **Year selector** (defaulting to the latest year, with an **All years** option) filters them.
- The sheet is **only read**. The page never writes to it.

---

## 5. Status Control

### 5.1 Statuses shown on internal cards

These statuses are **internal only**. Brand users never see them.

| Badge | Meaning |
|-------|---------|
| **Pending Approval** | Uploaded or resubmitted. Waiting for the approver |
| **Changes Required** | The approver sent it back. Remarks are shown in **red** on the card |
| **Approved — Ready to Notify** | Approved. The uploader can now notify the brand. Also remains while a notification is being retried |
| **Client Notified** | Published and all selected messages delivered |
| **Notification in Progress / Partially Failed / Failed** | A **second badge** showing message delivery, with per-channel chips: **Sent**, **Failed** (*Not selected* and *Not sent* are hidden) |

### 5.2 Who changes status, and how

| Change | Done by | How |
|--------|---------|-----|
| Upload or replace → **Pending Approval** | Uploader | Saves the report link. Internal history records "Report uploaded" and "Submitted for approval" |
| Pending Approval → **Approved — Ready to Notify** | Approver or Admin | Clicks **Approve** |
| Pending Approval → **Changes Required** | Approver or Admin | Clicks **Request Changes** with remarks of at least 50 characters |
| Changes Required → **Pending Approval** | Uploader | Clicks **Update Report** (or **Edit** in their list), pastes the new link and clicks **Submit for Approval**. Earlier review details are cleared on the card, and the history is kept |
| Approved → **Client Notified** | Uploader or Admin | Clicks **Notify Client** and all selected messages are delivered |

### 5.3 Rules to remember

- Only the **approver or an admin** can approve or request changes. **Nobody can approve their own upload.**
- **Requesting changes always needs remarks** (minimum **50 characters** on screen).
- A report **cannot be sent to the brand before it is approved**. This is checked on screen, on the server and in the database.
- A report becomes **visible to the brand at the moment Notify Client is clicked**, even while messages are still sending.
- After publishing, **Edit and Delete are locked** (*"Already sent to the brand"*).

---

## 6. Runbook – Internal Team

### 6.1 Uploader: upload a report

1. Select the brand in the top **brand switcher** and click **Upload Report**.
2. In the pop-up, pick the **Brand** (pre-filled with the selected brand; only assigned brands are listed) and the **Report Month** (the current month back **24 months**).
3. Paste the **Google Slides / PPT / PDF link**. It must start with `https://`.
4. If a report already exists for that brand and month, a **yellow warning** appears and the upload is **blocked** until you tick **"Replace the existing report and send it back for approval"**.
5. Save. The report becomes **Pending Approval**. An internal email goes to the approver, and admins and team leads get an in-app **"needs your approval"** alert.

### 6.2 Approver: review

1. Open the **approval queue** at the top of the page. It has four count tiles (**Pending Approval**, **Approved**, **Changes Required**, **Client Notified**) that also act as **filters**, plus **Brand**, **Month**, **Uploader** and **Status** filters and a **Refresh** button.
2. Click **Review** to open the deck preview with its **full activity timeline**.
3. **Approve:** the status becomes **Approved — Ready to Notify**, and the uploader receives an internal **Approved** email.
4. **Request Changes:** enter remarks of **at least 50 characters**. The status becomes **Changes Required**, and the uploader receives an internal email containing the remarks.

### 6.3 Uploader: fix and resubmit (only if changes were requested)

1. Read the **remarks** shown on the card.
2. Click **Update Report** (or **Edit** in your list), paste the new link and click **Submit for Approval**.
3. The report goes back to **Pending Approval**, and the approver is emailed again.

### 6.4 Uploader or Admin: notify the brand

1. Once approved, click **Notify Client**.
2. The pop-up lists the brand's **client users**: main-brand users plus client users assigned that brand. **Internal staff are never included.**
3. You can **remove people**, **add extra email addresses**, and **type or correct a WhatsApp number** for each person. A newly typed number is **saved back to that user's profile**.
4. Choose **Email** and/or **WhatsApp** and confirm. The report is **published to the brand immediately**, even while messages are still sending.
5. People who **already received that exact email are skipped**.

### 6.5 Check the result and retry

| Result | What the page shows |
|--------|---------------------|
| **Everything delivered** | Status **Client Notified**. The card shows the delivery time and **Email: Sent** / **WhatsApp: Sent** chips |
| **One channel failed** | **Notification Partially Failed**. The status stays **Approved**. The error is shown on the card (for example *"Invalid Number"*), with a **Retry Email** or **Retry WhatsApp** button |
| **All channels failed** | **Notification Failed**. Same retry buttons |

A retry **resends only the failed channel**. A channel that already delivered is **never sent again**. The brand can see the report as soon as it is published, **even if a message failed**.

### 6.6 Activity history and remarks

Every action is written to an **Activity history** that internal users can open from each card. It covers upload, submit, review, remarks, each email or WhatsApp sent or failed, and retries. **Uploaders can add follow-up remarks** there. The approver's remarks come from **Request Changes**.

## 7. Runbook – Brand User

1. Open **Reporting › Monthly Reports**. Your own brand is selected.
2. Use the **Year selector** to filter the cards if needed.
3. Click **View Report** on a card. The deck opens **full-screen inside the platform**. Right-click is disabled.
4. Cards with no link show **"Coming Soon"**.

You only see **published** reports. You never see statuses, remarks, uploader names or action buttons. A report appears as soon as the team clicks **Notify Client**.

---

## 8. Emails, WhatsApp and In-App Alerts

| When | Sent to | Subject / message | CC |
|------|---------|-------------------|----|
| Upload or resubmit | Approver | *[INTERNAL] Monthly Report Pending Approval — {Brand} \| {Month}* | The product and customer success team addresses |
| Approved | Uploader | *[INTERNAL] Monthly Report Approved — {Brand} \| {Month}* | Same |
| Changes requested | Uploader | *[INTERNAL] Changes Required — {Brand} \| {Month} Monthly Report* (includes the remarks) | Same |
| Notify Client | Brand users | *Your {Month} Monthly Report is Live — {Brand}*, with a **View Monthly Report** button | Same, plus any **brand-specific CCs** (for example IBIS Academy, StampEight) |
| Notify Client (WhatsApp) | Brand users with a number | The approved AiSensy template with the brand and month and a fixed **View Monthly Report** button | None |

- All emails are signed by **Miss Daring**. Replies go to the customer success address. Every button links to the Monthly Report page.
- **Brands on the email block list (Herbal Chakra, Herby Angel) receive no emails.**
- **Safety net:** every **5 minutes** a background check resends any **internal** approval or review email that did not go out (for example if the browser was closed part-way). It does **not** send brand emails or WhatsApp.
- **In-app bell alerts:** a **"needs your approval"** alert goes to admins and team leads on upload. It is cleared when the report is reviewed, followed by an **"approved"** or **"changes requested"** alert, and a **final alert** when the brand is notified.
- The WhatsApp template is **monthly__report__live__v3**.

---

## 9. Built-in Safeguards

- Only the approver or an admin can approve or request changes, and **nobody can approve their own upload**.
- Requesting changes always needs remarks (minimum 50 characters on screen).
- A report **cannot be sent to the brand before it is approved**. It is checked on screen, on the server and in the database.
- Uploaders can only upload, see, edit or delete reports for **brands assigned to them**, and can **delete only their own unpublished reports**. After publishing, **Edit and Delete are locked**.
- **Duplicate month uploads** need an explicit **Replace** confirmation.
- Brand users can read only **published** reports for brands they have access to. **Internal workflow details are never sent to them.**
- Every action is recorded in the **Activity history**.

## 10. Other Page Behaviour

| Situation | What the page shows |
|-----------|---------------------|
| Viewing a report | **View Report** opens the deck full-screen inside the platform. Right-click is disabled. Cards with no link show **"Coming Soon"** |
| No reports for the brand | *"No reports available yet. Reports will appear here once they are generated."* Uploaders still see the **Upload Report** button |
| Reports could not load | Red message: *"Failed to load reports. Please try again later."* |
| Brand marked as being set up | **"Reports Access Pending"** message. No brand is currently set up this way for Monthly Reports |
| **Kapiva** | The page is **locked** for Kapiva (only its four unlocked analytics pages are open) |
| Trial (Lite) users | Follow the usual trial page rules. Demo accounts see the single sample report |
| Admins and internal staff switching brands | Cards follow the brand chosen in the top brand switcher. The **approver queue and uploader list stay cross-brand** |

---

## 11. Current Snapshot (19 November 2026, read only)

49 platform-uploaded reports are saved: **37 Client Notified** and **12 Approved but not fully delivered**.

- **5 approved, not yet notified:** Dorset Oct 2026 and Aug 2026, Genes Sep 2026, ACC Cement Aug 2026, Ambuja Cement Aug 2026.
- **4 partially failed (email sent, WhatsApp failed):** Dynavac Oct 2026, Ambuja Cement Sep 2026, Dorset Sep 2026, Genes Aug 2026.
- **3 marked failed:** Chaat Bazaar Aug, Sep and Oct 2026. The emails were delivered, but the WhatsApp retries to the UAE number (+971) were rejected as *"Invalid Number"*, so the badge reads failed. These reports are **already published and visible to the brand**.

These numbers are a point-in-time reading and will change as the team uses the page.

## 12. Points Worth Knowing

- A report becomes visible to the brand the moment **Notify Client** is clicked. A **failed WhatsApp does not hide the report**. It only affects the message.
- **Uploader list mismatch:** the on-screen uploader list is fixed in the page itself, while the server uses the saved role list. One of the uploader addresses (the Digidarts one for Arpita) is an uploader on the server but **not** in the page's list, so if Arpita signs in with that address she **may not see the uploader buttons**. This is an observation only.
- Older sheet links are **matched to a brand by name, including partial matches**, so a sheet row with a very similar brand name could in theory be picked up for the wrong brand.
- **International numbers** (for example Chaat Bazaar's UAE number) may be rejected by AiSensy depending on its settings.
- **Nothing on this page writes to Google Sheets.** All approvals, history and delivery results are stored in the platform.

## 13. Troubleshooting

| Situation | What to do |
|-----------|------------|
| Cannot see **Upload Report** | Only uploaders see it. Check the signed-in address is on the uploader list (see section 12) and the brand is assigned to you |
| Upload blocked with a yellow warning | A report already exists for that brand and month. Tick **Replace the existing report and send it back for approval** |
| Link rejected | It must start with `https://` |
| Cannot approve | Only the approver or an admin can. Nobody can approve their own upload |
| **Request Changes** will not submit | Remarks need at least **50 characters** |
| Cannot click **Notify Client** | The report must be **Approved** first |
| **Edit** or **Delete** is locked | The report is already published (*"Already sent to the brand"*) |
| Status shows **Partially Failed** or **Failed** | Read the error on the card (for example *Invalid Number*). Correct the number in the Notify pop-up or use **Retry Email** / **Retry WhatsApp** |
| Brand cannot see a report | It is not published yet. **Notify Client** publishes it |
| Brand sees a report but did not get a message | The report is published. Check the delivery chips and retry the failed channel |
| Brand got no email | The brand may be on the email block list (Herbal Chakra, Herby Angel) |
| Card shows **Coming Soon** | The card has no link |
| Page locked | The brand has a page lock (Kapiva) |
| An internal email did not arrive | The 5-minute safety net resends missing internal emails |

## 14. Related Documents

- Other approval flows, for comparison: [Execution/youtube.md](../../Execution/youtube.md), [Execution/blogs.md](../../Execution/blogs.md)

## 15. Open Items

None. The uploader list mismatch in section 12 is an observation from the source and has not been changed.
