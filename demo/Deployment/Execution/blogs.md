# Blogs – Execution Runbook

> Path in the plat  orm: **Deployment → Owned Channels → Blogs** (`/execution/blogs`). Owned Channels is a sub-section of Deployment.
>
> This document explains **how the page works and where its data comes from**. For screen layout, columns and observed data, see the UI document: [UI/blogs.md](../UI/blogs.md). For the workflow as a flowchart, see [Flowcharts/blogs.md](../Flowcharts/blogs.md).
>
> **This page is different from the other execution pages.** It is a **read-only progress board**. There is no CSV upload, no Add Manually, no edit or delete, no approval on the page, no comments and no Notify buttons or emails. The all-pages rules about comments, edits and the brand dashboard Notify button **do not apply** here. All the work happens in **Blog Generator**, and this page shows the result. The **standard status names** are used for the statuses shown (see section 6).

---

## 1. Purpose

The Blogs page lists every blog for the selected brand, **month by month**, and shows how far each one has got: whether the topic is approved, whether the blog is accepted or published, and the **live link** once it is on the website.

It brings together two sources:

- **New blogs** created in **Blog Generator**.
- **Earlier blogs** recorded in the brand's **old database**.

## 2. End-to-End Flow

1. The team creates blog topics for a brand in **Blog Generator** page.
2. The brand (or the team) **approves** the topic or **disapproves** it (asks for changes or rejects it) in Blog Generator page.
3. Once the topic is approved, the blog is written and reviewed (**Approved** or **Disapproved**) in Blog Generator page.
4. When the blog goes live, it is marked **Live on Website** and/or a **live link** is added in Blog Generator page.
5. Every time someone opens **Blogs**, the page reads the latest Blog Generator statuses.
6. Clicking a Blog Generator row's status opens that exact topic in Blog Generator, where any action can be taken.

---

## 3. Who Can Open the Page and What They See

| Who | What they see |
|-----|---------------|
| **Admin** | Any brand, chosen from the brand picker at the top |
| **Sub-admin / SEO team (internal staff)** | Only the brands assigned to them, chosen from the brand picker. |
| **Brand user** | Their own brand only. No brand picker |
| **Draft topics** | Visible only to internal staff. Brand users never see drafts |
| **Rejected topics** (shown as **Disapproved** when rejected) | Hidden from everyone on this page |

### Extra rules for the earlier (old database) records

- They load only for users on a **Paid or Lite** plan, or admins and sub-admins.
- These brands are allowed without a paid plan: **Playo, Dynavac, IBIS Academy, StampEight, Gumazing, Origin Nutrition**.
- If a brand has **no old database** set up for blogs, only Blog Generator blogs appear.

### Other app-wide rules that also apply

- Users must be signed in. Otherwise they are sent to the login page.
- Brands with **page locks**  are redirected away and cannot open this page.
- Growth-plan users with a **payment pending** are sent to the payment step first.
- Whether **Blogs** appears in the sidebar depends on the brand's Deployment menu settings. Hiding it from the sidebar does **not** block the page itself.

---

## 4. Where the Data Comes From

### 4.1 Blog Generator (new blogs)

- Reads all blog requests for the brand and the topics under them.
- The **Primary Keyword** comes from the original blog request.
- Each topic is placed in the month it was **created**, not the month it was published.
- Statuses are always live: whatever is set in Blog Generator shows on the **next page load**.



---

## 5. What Is on the Screen

- **Page title:** Blogs.
- **Month picker** (top right): lists every month that has blogs, newest first. The newest month is selected by default.
- **Count line:** for example *"12 blogs for November 2026"*.
- **Table** columns:

| Column | What it shows |
|--------|---------------|
| **#** | Dynamic Row number within the selected month |
| **Blog Topic** | The blog title. Earlier sheet rows carry an **Earlier record** badge |
| **Primary Keyword** | Main keyword for the blog |
| **Topic Status** | Approval stage of the topic (Blog Generator), or the status text from the sheet for earlier records |
| **Blog Status** | Writing and review stage of the blog (Blog Generator only). Blank for earlier records |
| **Final Status** | Either **Live on Website** or **In progress** |
| **Live Link** | A **Visit** link that opens the live blog in a new tab |

---

## 6. What Each Status Means

The statuses come from **Blog Generator**, where the approval happens. They are shown here with the **standard status names** used on every page. Blog Generator's own labels are given for reference.

### 6.1 Topic Status (Blog Generator rows)

| Shown as | Blog Generator label | Meaning | Colour |
|----------|----------------------|---------|--------|
| **Approval Pending** | Draft | Topic created but not yet sent to the brand (staff only) | Grey |
| **Approval Pending** | Awaiting brand | Sent to the brand for approval | Amber |
| **Disapproved** | Changes requested | Brand asked for changes to the topic | Amber |
| **Approved** | Accepted | Brand approved the topic. Writing can start | Teal |
| **Disapproved** | Rejected | Topic rejected. Hidden from this page | Red |

### 6.2 Blog Status (Blog Generator rows)

| Shown as | Blog Generator label | Meaning | Colour |
|----------|----------------------|---------|--------|
| **Approval Pending** | Not started | No blog written yet | Grey |
| **Disapproved** | Changes requested | Changes requested on the written blog | Amber |
| **Approved** | Accepted | Written blog approved | Teal |
| **Disapproved** | Rejected | Written blog rejected. The row is still shown | Red |
| **Live on Website** | Published | Blog is published | Blue |

### 6.3 Final Status

- **Live on Website** (blue): the blog is marked **Live on Website** (Published in Blog Generator), **or** it has a live link. For earlier sheet records, the sheet status says "Live on Website" **or** a live link is present.
- **In progress** (grey): everything else.

Adding **any** live link is enough to show **Live on Website**. The link itself is **not checked**.



---

## 7. What Users Can Do on This Page

| Action | Who | Result |
|--------|-----|--------|
| Pick a month | Everyone | Shows that month's blogs |
| Click **Topic Status** or **Blog Status** (Blog Generator rows) | Everyone | Opens that topic in Blog Generator |
| Click **Visit** | Everyone | Opens the live blog in a new tab |
| Switch brand (top bar) | Admins and assigned staff | Reloads the page for that brand |

**Not available on this page, for any role:** adding, editing or deleting rows; changing statuses; approving or rejecting; comments; Notify buttons or emails; importing, exporting or rearranging columns. All of these happen in **Blog Generator**.

**Emails:** this page does **not** send any emails or WhatsApp messages. Blog-related notifications are sent from Blog Generator.

---

## 8. Runbook – Internal Team and Admin

1. Select the brand in the top brand picker (admins: any brand; assigned staff: assigned brands).
2. Select a month with the month picker.
3. Read the table: topic, keyword, Topic Status, Blog Status, Final Status and Live Link.
4. To take any action on a Blog Generator row, **click its Topic Status or Blog Status**. This opens the topic in Blog Generator.
5. After a change in Blog Generator, **reopen or reload** the Blogs page. It shows the new status on the next load.
6. To check a live blog, click **Visit**.

## 9. Runbook – Brand User

1. Open the **Blogs** page. Your own brand is selected, and there is no brand picker.
2. Select a month and read your blogs. You do not see drafts or rejected topics.
3. Click **Topic Status** or **Blog Status** to open the topic in Blog Generator, where you can approve or disapprove it.
4. Click **Visit** to open a live blog.

---

## 10. Loading, Empty and Error States

| State | What shows |
|-------|------------|
| Loading | Five grey placeholder rows until all data is ready |
| Nothing to show | *"No blogs yet – Topics created in Blog Generator will appear here."* |
| Sheet problem and **no** Blog Generator blogs | The same message, with a **red warning icon** instead of the document icon |
| Sheet problem but Blog Generator blogs exist | The table shows Blog Generator blogs only, with no warning |

## 11. Brand-Specific Sheet Set-Ups

| Brand | Sheet notes |
|-------|-------------|
| **ACC / ACC Cement** | Tab "ACC Blog". Serial numbers may be blank. Links are read from smart chips. Both names show the same data |
| **Ambuja Cement** | Serial numbers may be blank in newer months |
| **Sunstone** | Tab "Blog/Linkedin" with a custom column layout |
| **IITM Sonipat / ITM Dehradun** | No serial-number column. Custom status and link columns |
| **Origin Nutrition** | All rows are treated as **November 2026**. No live-link column |
| **Not Drones** | Custom layout with topic-approval and content-link columns |

### Things to be aware of

- The **same blog can appear twice** if it exists both in Blog Generator and in the sheet. The two sources are **not merged**.
- Blog Generator blogs are grouped by the month the topic was **created**, which may differ from the month it went live.
- Saved sheet rows keep their first-seen values. If a status or link is later changed in the sheet, the page still shows the **live sheet value** while the row exists in the sheet, but the saved copy is not updated.
- **Renaming** a topic or **moving it to another month** in the sheet creates a **new saved row**. The old one stays visible.
- Very large brands are capped at **2,000 requests, 5,000 topics and 5,000 saved sheet rows**.
- Comments, content-deck links and image links exist in the data but are **not shown** on this page.

---

## 12. What the Page Looks Like Today (Observed)

The UI document ([UI/blogs.md](../UI/blogs.md)) matches the read-only design, with these differences from the working-flow reference:

- The **Topic Status** seen was **Approved** with a grey dot. In the reference, **Approved** is teal.
- **Blog Status** was empty on every row observed. The reference says it is blank for earlier records, so this fits earlier records only.
- The observed months went back to January 2025.

## 13. Troubleshooting

| Situation | What to do |
|-----------|------------|
| Status looks old | Reload the page. Statuses update only on the next page load |
| A blog appears twice | It exists in both Blog Generator and the sheet. The sources are not merged |
| Earlier records missing | Check the plan (Paid or Lite, or an allowed brand) and that the brand has a old database set up |
| "No blogs yet" with a red warning icon | The old database could not be reached and there are no Blog Generator blogs |
| A topic is missing | Draft topics (**Approval Pending**, not yet sent) are hidden from brand users, and rejected topics are hidden from everyone |
| Blog in the wrong month | Blog Generator blogs use the month the topic was **created** |
| Cannot open the page (for example Kapiva) | The brand has a page lock. The user is redirected away |
| Sent to a payment step | A Growth-plan payment is pending |
| Cannot edit, approve or comment here | Not available. Click the status to open the topic in Blog Generator |
| Blogs not in the sidebar | Depends on the brand's Deployment menu settings. The page itself is still reachable |
