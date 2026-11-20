# Blog Generator – Execution Runbook

> Path in the platform: **Intelligence › Blog Generator** (`app.dareaisearch.com/blog-generator-v2`)
>
> This document explains **how the page works from end to end**: who does what, in which order, how status changes and what is sent to whom. For the workflow as a flowchart, see [Flowchart/blog-generator.md](../Flowchart/blog-generator.md).
>
> **This page is different from the Deployment pages.** It has **its own statuses, roles and approvals**. The Deployment rules (CSV upload of rows, Approval Pending / Approved / Disapproved / Live on Website, brand dashboard Notify) **do not apply** here. The brand works on the same page as the team, but **only sees what has been shared with them**.

---

## 1. Purpose

The Blog Generator is where a blog goes **from an idea to a published article** for a brand.

1. Each idea starts as a **request**: a primary keyword, optional secondary keywords and an optional prompt.
2. The SEO team turns the request into one or more **topics**, either with AI suggestions or by typing them, and shares them with the brand.
3. The brand **approves, rejects or asks for changes** on each topic.
4. An approved topic is **assigned to a Content team writer**, who adds the blog draft link (content deck) and shares it.
5. The brand reviews the draft. Once it is accepted, a team lead adds the **live link** and marks it **Published**.

## 2. End-to-End Flow

| Stage | What happens | Who |
|-------|--------------|-----|
| 1 | **Request raised** | Internal user, or the brand (Try a Blog!) |
| 2 | **Idea reviewed** (brand keyword ideas only) | Team lead or Admin |
| 3 | **Topics created and shared** with the brand | SEO lead or Admin, or the person the idea was handed to |
| 4 | **Brand decides** on each topic | Brand user |
| 5 | **Writer drafts and shares** the blog | Content team writer |
| 6 | **Brand accepts, then the team publishes** | Brand user, then Team lead or Admin |

---

## 3. Roles and Scope

| Role | Who (today) | What they can do |
|------|-------------|------------------|
| **Admin** | Platform admins | **Everything:** raise requests, review brand ideas, generate or add topics, share, assign, publish, change the column layout, delete topics and **delete whole requests** |
| **SEO team lead** | Rahul, Arpita | Raise requests (one by one or from a sheet), approve or reject brand ideas, generate or add topics, notify the brand, assign work, publish blogs, delete topics, change columns |
| **Content team lead** | Dhimayee | Same as an SEO lead **except running topic generation** (unless the request is handed to her): reviews ideas, assigns writers, edits blog drafts, notifies the brand, publishes |
| **Team member** | SEO: Manav, Mohit G., Mohit R., Parveen, Shreyansh, Sonam. Content: Praba | Sees **only requests handed to them and topics assigned to them**. Can work on topics for an idea handed to them, and write and share the blog for a topic assigned to them. **Cannot raise requests or publish** |
| **Brand user** | Client logins of the brand | **Try a Blog!**: suggest a keyword idea or give their own topic. **Approve, reject or request changes** on shared topics and shared blog drafts. Open the published blog |

- Team, team-lead and member roles come from the **saved team list**. Staff who are **not on that list but are internal** (admins, sub-admins, internal team) are treated as **team leads**.
- **Trial (Lite) users cannot open this page.** It is **locked for Kapiva**.

## 4. Page Layout

- **Header:** page title with the brand name, a **Columns** control (internal only) and the **New request** button (brands see **Try a Blog!**).
- **Requests table:** one block per request with its topics underneath. Columns: #, Primary keyword, Secondary, Prompt, Finalized Topic, Topic status, Assigned to (internal only), Blog, Raised by, and an action button that opens the side panel.
- **Filters:** **Month** (defaults to the current month, else the latest month with requests; *All months* is available) and a search box for keyword, topic or person.
- **Bulk bar:** tick several rows to act on them together. Internal users can **Notify brand** (drafts and blogs that are ready). Brands can **Approve** or **Reject** topics waiting for them.
- **Side panel:** opens from the action button. Shows request details, review, topic, blog, comments and the full **Activity history** for that row.
- **Column layout:** internal users can **hide and reorder columns per brand**, and the brand sees the same layout. **Finalized Topic cannot be hidden.**
- Links from **Deployment › Blogs** open this page with the exact topic highlighted.

---

## 5. Status Control

### 5.1 Statuses

| Where | Status | Meaning |
|-------|--------|---------|
| Request | **Awaiting internal review** | Brand idea waiting for the team's review |
| Request | **Rejected internally** | Brand idea turned down by the team |
| Request | **Not started** | Approved, but no topic yet (internal only) |
| Topic | **Draft** | Created by the team, not yet shared. **Never visible to the brand** |
| Topic | **Awaiting brand** | Shared, waiting for the brand's decision |
| Topic | **Accepted / Rejected / Changes requested** | The brand's decision (or a brand's own topic, accepted automatically) |
| Blog | **Being written → Ready to share → Awaiting brand** | Writer working → deck added and marked ready → shared with the brand |
| Blog | **Accepted / Changes requested / Rejected** | The brand's decision on the draft |
| Blog | **Published** | Live link added. The brand sees *"Published blog"* |

### 5.2 Who changes status, and how

| Change | Done by | How |
|--------|---------|-----|
| Internal request → **Not started** | System | Internally raised requests are **approved automatically** |
| Brand idea → **Awaiting internal review** | System | Set when the brand suggests keywords |
| Awaiting internal review → approved (**Not started**) or **Rejected internally** | Team lead or Admin | **Approve** or **Reject** in the side panel. A **note is required to reject** |
| Brand's own topic → **Accepted** | System | A brand's own topic is accepted immediately |
| Draft → **Awaiting brand** | Internal user | Ticks drafts and clicks **Notify brand** (or uses the toggle in the side panel) |
| Awaiting brand → **Accepted / Rejected / Changes requested** | Brand | In the side panel, or **Approve / Reject** in bulk. A **comment is required** to reject or request changes |
| Changes requested → **Draft** | Internal user | Edits the topic text (pencil icon), then re-shares |
| Blog **Being written** → **Ready to share** | Writer | Adds the **Content deck link** (and optionally an image link) and clicks **Save** |
| Ready to share → **Awaiting brand** | Internal user | **Notify brand** (single or bulk) |
| Awaiting brand → **Accepted / Changes requested / Rejected** | Brand | **Accept, Request changes or Reject.** A comment is required for the last two |
| Changes requested or Rejected → shared again | Writer | Updates the deck and clicks **Re-share revision** |
| Accepted → **Published** | Team lead or Admin | Pastes the **Live link** and clicks **Publish** |

---

## 6. Runbook – Internal Team

### 6.1 Raise a request

1. **New request:** fill the **Primary keyword** (required), **Secondary keywords** and an optional **Prompt**. The keyword and prompt boxes suggest the brand's own ranked keywords and prompts with their best rank (for example *"#3"*, *"Not ranking"*). Optionally use **Hand the research to** a team member.
2. **In bulk:** upload a CSV or Excel sheet with **exactly** the columns **Primary Keyword, Secondary Keyword, Prompt, Finalized Topic**. A sample sheet can be downloaded. The limit is **200 rows**. Each row becomes **its own request**, and a Finalized Topic in the row is saved as a **draft topic**.
3. Internally raised requests are **approved automatically**.

### 6.2 Review a brand's idea (brand keyword ideas only)

1. The row shows **Awaiting internal review**. Admins and team leads get an **in-app alert**.
2. A team lead or Admin opens the side panel and clicks **Approve** or **Reject** (a note is required to reject). The brand gets an **email and an in-app alert** either way. A rejected row shows **Rejected internally**.
3. After approval, the idea can be **handed to a team member**, who gets an in-app alert **"Topic research assigned to you"**. Brand ideas cannot be worked on until approved.

### 6.3 Create topics and share them

1. On an approved request with no topic, SEO leads and admins (or the person the idea was handed to) see **Generate topics** and **Add topic yourself**.
2. **Generate topics:** a brief opens with the keywords, prompt, target audience, geography and funnel stage (**TOFU / MOFU / BOFU**). **Save** keeps the brief. **Generate** sends it to the outside AI workflow, which returns **up to 5 topic ideas per round**. Several rounds can be run, your own ideas can be typed in, and the chosen ones are saved as **Draft** topics.
3. **Add topic yourself:** type topics (one per line) and either **Save as drafts** or share them straight away.
4. Drafts are **internal only**. To share, tick the drafts and click **Notify brand** (or use the toggle in the side panel). The topics become **Awaiting brand**. The brand gets **one combined email** (*"N blog topics ready for your review"*) and an in-app alert per topic.

### 6.4 After the brand decides on a topic

1. Team leads, admins and the assigned writer get an **in-app alert** with the decision and comment.
2. **Changes requested:** edit the topic text (pencil icon). It goes back to **Draft** and is re-shared.
3. **All topics rejected:** **Regenerate** or **Add topic yourself** appears on the request.

### 6.5 Assign, write and share the blog

1. A team lead or Admin **assigns the topic to a Content team writer** (in-app alert to the writer). Writers are chosen only from the Content team.
2. The writer may **start once assigned**, but can **share only after the brand has accepted the topic**.
3. The writer adds the **Content deck link** (and optionally an image link) and clicks **Save**. The status becomes **Ready to share**.
4. **Notify brand** (single or bulk). The status becomes **Awaiting brand**. The brand gets **one combined email** (*"N blogs ready for your review"*, with titles) and an in-app alert. **Only now can the brand open the deck.**

### 6.6 After the brand reviews the blog

1. The team is alerted in-app with the brand's decision.
2. If changes were requested or the blog was rejected, the writer updates the deck and clicks **Re-share revision**.
3. Once the blog is **Accepted**, a team lead or Admin pastes the **Live link** and clicks **Publish**. The status becomes **Published**. Team leads, admins, the content team and the brand get an in-app alert, and the brand's **Blog** column links to the live article.

### 6.7 Deleting

- Team leads and admins can **delete a topic**. This removes its comments and history.
- **Only an Admin** can delete a whole request.
- Both ask for confirmation and **cannot be undone**.

## 7. Runbook – Brand User

1. Open **Intelligence › Blog Generator**.
2. Click **Try a Blog!** and either **suggest keywords for the team**, or **write your own topic**. You cannot do both in one request.
   - Your **own topic is accepted immediately** and appears as an accepted topic.
   - A **keyword idea waits for internal review.** You get an email and an in-app alert when it is approved or rejected.
3. When topics are shared, open each one in the side panel and **Approve, Reject or Request changes**, or use **Approve / Reject** in bulk. A **comment is required** to reject or request changes.
4. When a blog is shared, open the draft and choose **Accept, Request changes or Reject** (a comment is required for the last two).
5. After publishing, the **Blog** column links to the live article.

---

## 8. Emails and In-App Alerts

| When | Brand email (from Miss Daring) | In-app alert goes to |
|------|-------------------------------|----------------------|
| Brand raises an idea | – | Team leads and admins (needs review) |
| Idea approved / rejected | *"We're working on your blog request — {keyword}"* / *"An update on your blog request — {keyword}"* (with the reason) | Brand |
| Idea or research handed over | – | The person it was handed to |
| Topics shared | *"N blog topic(s) ready for your review"* (one combined mail) | Brand |
| Brand decides on a topic | – | Team leads, admins and the assigned writer |
| Topic assigned to a writer | – | The writer |
| Blog shared | *"N blog(s) ready for your review"* (with titles) | Brand |
| Brand decides on a blog | – | Team leads, admins and the writer |
| Blog published | – | Team leads, admins, content team and brand |

- Brand emails go to **every client user of that brand** (never internal accounts), **CC product@ and customer.success@dareaisearch.com**, and replies go to customer.success@.
- **Brands on the email block list receive nothing.**
- **Internal staff receive in-app alerts only.** This page sends them no emails.
- **Publishing alerts the brand in-app but does not send an email.**

## 9. What the Brand Sees (and Doesn't)

- **Only shared topics.** Drafts and approved-but-not-started internal rows are hidden.
- Staff names are always shown as **"DAIS"**, never individual team members. The **Assigned to** column is hidden.
- The **content deck opens only after the team has shared the blog.** After publishing, it opens the live article instead.
- The brand **cannot edit topics, assign, publish or delete** anything.

## 10. Built-in Safeguards

- Brand ideas **cannot be worked on until approved internally**, and rejecting needs a note.
- A blog **cannot be shared until its topic is accepted and a content deck link exists**. Publishing needs a **live link and an accepted blog**.
- Team members only see and act on work **handed or assigned to them**. Writers are chosen only from the Content team.
- Deleting a topic removes its comments and history. Deleting a whole request is Admin-only. Both ask for confirmation and cannot be undone.
- Every action is written to the row's **Activity history** (created, shared, decided, assigned, edited, published).

## 11. Points Worth Knowing

- The **target audience, geography and funnel stage** in the brief are kept only while the page is open. The keywords and prompt are saved to the request, but **those three fields are not saved permanently**.
- Topic ideas come from an **outside AI workflow**. If it is unavailable, **"Topic generation failed"** appears and topics can still be **added by hand**.
- **Deployment › Blogs** shows these same statuses **read-only**, month by month, for the brand.

## 12. Troubleshooting

| Situation | What to do |
|-----------|------------|
| Cannot open the page | Trial (Lite) users cannot open it, and it is locked for Kapiva |
| Brand cannot see a topic | It is still a **Draft**. Click **Notify brand** to share it |
| Brand idea cannot be worked on | It must be **approved internally** first |
| Reject will not submit | A **note** (internal) or **comment** (brand) is required |
| **Topic generation failed** | The outside AI workflow is unavailable. Use **Add topic yourself** |
| Writer cannot share the blog | The topic must be **Accepted** and a **Content deck link** must be saved |
| Brand cannot open the deck | The blog has not been shared yet. Use **Notify brand** |
| Cannot publish | The blog must be **Accepted** and a **Live link** must be pasted |
| Team member cannot see a request | Members only see requests handed to them and topics assigned to them |
