# Brand Voice – Execution Runbook

> Path in the platform: **Intelligence › Brand Voice** (`/intelligence/brand-voice`)
>
> This document explains **how the page works from end to end**: who can use it, what feeds the document, how it is built and how drafts are reviewed. For the workflow as a flowchart, see [Flowchart/brand-voice.md](../Flowchart/brand-voice.md).
>
> Source: *Brand Voice working flow* (prepared 20 Nov 2026). Based on the page's setup and a read-only look at saved records; the flow was not run live.

---

## 1. Purpose

Brand Voice turns a brand's **approved blogs** (and, where available, its **brand book**) into a written **Brand Voice Document**: a 12-part guide that tells writers how the brand should sound. A second tab then uses that document to **review any new draft** and say what is on-brand, off-brand and what needs fixing.

- **Page title:** Brand Voice, subtitle "AI-powered brand voice generation and content review".
- **Two tabs:** **Brand Voice Generator** (called **Brand Voice Document** for brand users) and **Brand Voice Review**.
- **Brand shown:** the brand picked in the top brand picker (admins, internal staff); the user's own brand for brand logins.
- **No emails, WhatsApp messages or in-app alerts** are sent from this page.

## 2. End-to-End Flow

| Stage | What happens | Who |
|-------|--------------|-----|
| 1 | **Page opens**: brand book, approved blogs, current document and monthly switch load; automatic blog sync runs | Admin |
| 2 | **Blogs prepared**: approved blogs synced from Deployment › Blogs, or added by hand | System, Admin |
| 3 | **Generate / Regenerate**: AI builds a new 12-section document version | Admin |
| 4 | **Document used**: read, searched, copied; old versions viewed in History | Everyone with access |
| 5 | **Draft reviewed** against the active document | Any user |
| 6 | **Review saved** to Review History | System |

---

## 3. Roles and Scope

The page is open to **every signed-in user, including Lite (trial) users**, and appears in every sidebar.
| Role | Generator tab | Review tab |
|------|---------------|------------|
| **Admin** | Full control: approved blog list, **Add Blog**, delete blogs, **Generate / Regenerate**, monthly switch, History, Copy | Reviews drafts; sees **every review** for the brand; can delete any review |
| **Sub-admin / internal team** | Sees the manager layout (blog list, Generate button) **but the blog list loads empty and generation is refused ("Admin only")** | Reviews drafts. Sub-admins see **all** reviews for the brand; other internal staff see **their own** |
| **Brand user** | Read-only **Brand Voice Document** tab: latest document, search, section shortcuts, Copy, History. Blog list and Generate are hidden | Reviews drafts against their brand voice; sees and deletes **only their own** reviews |

---

## 4. What the Document Is Built From

| Source | How it gets in | How it is used |
|--------|----------------|----------------|
| **Brand book** (optional, source of truth) | Added by the team behind the scenes from a stored file. **No upload button** on the page. A banner shows its title, word count and date | Treated as the authority: **where blogs disagree, the brand book wins**. On its own it is enough to generate |
| **Approved blogs** | **Automatic:** on every page open, approved/live blogs from Deployment › Blogs are pulled in by live link (or content-deck link if no live link). **Manual:** **Add Blog**, paste text or fetch from a URL, with a title, at least about **50 words** | Used to learn real writing patterns and examples. **At least 3** are needed when there is no brand book |

### Automatic sync from Deployment › Blogs (runs on page open)

1. Read the brand's Deployment › Blogs board and keep only entries marked **Approved, Live on Website, Live or Published**.
2. **Remove** link-imported blogs that are **no longer approved** in Deployment. **Manually pasted blogs are always kept.**
3. Collapse duplicate titles, keeping the newest copy.
4. If a blog came in through its content-deck link and now has a live link, **upgrade the saved link**.
5. Fetch and add new approved blogs; show "Synced from Deployment – N approved blogs auto-imported".

A **month picker** filters the list by Deployment month. Each blog shows word count, month, a link and one tag:

| Tag | Meaning |
|-----|---------|
| Included in last generation | Used to build the current document |
| Added after last generation | Added since; **Regenerate** to include it |
| Not in last generation | Older blog that was not part of the current document |
| Not yet generated | No document exists for the brand yet |

---

## 5. Flow A: Building the Brand Voice Document

1. Admin selects the brand. The page loads the brand book (if any), approved blogs, current document and monthly switch, then runs the sync.
2. **Generate Brand Voice** is active with **3 or more approved blogs, or a brand book**. Otherwise it shows "Add N more blogs to enable generation".
3. On click, the AI reads the **brand book first, blogs second**, following the team's saved Brand Voice instructions plus fixed rules: stay grounded in the material, **no invented traits**, every line **positively framed** (what the customer gains, never fear-based).
4. Generation takes about **30–60 seconds**. The result is saved as a **new version** (v1 = *AI Generated*, later = *AI Refreshed*). It becomes the **active** version; the previous one stays in History.
5. The document appears on the right with a short overview, search box, jump links to each section and **Copy** buttons (whole document or one section).
6. To update later: add or remove blogs, then **Regenerate**. Deleting a blog only affects future versions.

### The 12 sections of every document

| # | Section | What it covers |
|---|---------|----------------|
| 1 | Brand Understanding | What the brand does, who it serves, what makes it different |
| 2 | Target Audience | Primary and secondary audiences, motivations, pain points |
| 3 | Brand Voice Summary | Tone and persona in a few lines |
| 4 | Writing Style | Sentence and paragraph length, formality, use of data and examples |
| 5 | Blog Structure Guidelines | Intro, headings, body, conclusion, FAQ use, length |
| 6 | SEO & GEO Guidelines | Keywords, headings, AI-answer readiness, location framing |
| 7 | Language Guidelines | Preferred and banned words, spelling, brand-name styling |
| 8 | Do's and Don'ts | Table: Do / Don't / Explanation / Example (12–20 rows) |
| 9 | CTA Guidelines | How calls to action sound and where they go |
| 10 | Approved Content Patterns | Recurring structures seen across approved blogs |
| 11 | Content Examples | 3–6 model snippets: intro, definition, CTA, FAQ answer |
| 12 | Quality Checklist | Grouped under Brand Voice, SEO, Structure, Accuracy, Final Review |

---

## 6. Flow B: Reviewing a Draft (Brand Voice Review tab)

1. The tab checks the brand has an **active Brand Voice Document**. If not, it warns to generate one first and **Review Content stays disabled**.
2. User adds an optional title and **pastes the draft** (blog, landing page, FAQ, product description, caption) or **uploads a .txt / .md file** up to about **1.5 MB**. At least **20 words** are needed.
3. **Review Content** sends the draft to the AI with the brand book (if any) and the active document, using the team's saved review instructions.
4. The result shows an overall **verdict** (**Approved, Needs Revision or Disapproved**), three groups (**Approved / Disapproved / Needs Revision**, each with reasons or fixes), a **scorecard** and the full written report (copyable).
5. Every review is **saved automatically**. **History** lists past reviews with verdict and counts; clicking one reloads the draft and result. Reviews can be deleted from History.

---

## 7. History and Versions

- **Brand Voice History** (Generator tab): up to **50 versions**, newest first, each with version number, label (*AI Generated*, *AI Refreshed* or *Manual Seed*), **Active** tag, date and number of blogs used. Click to preview any old version. **Older versions cannot be re-activated from the page.**
- **Review History** (Review tab): up to **50 past reviews** for the brand, filtered by who may see them (Section 3).
- Brands saved under **two names** (e.g. ACC / ACC Cement) show their documents, blogs and reviews together.

## 8. Where Information Is Kept

| Information | Notes |
|-------------|-------|
| Approved blogs | One record per blog: title, text, word count, paste or link. **Admin access only** |
| Brand Voice Documents | Every version kept; one marked active. Readable by anyone with access to the brand |
| Brand book | One primary document per brand; earlier ones kept but no longer primary |
| Review history | Draft, report, verdict, groups and scorecard for each review |
| AI instructions | One active set for generation, one for reviews; managed by admins outside this page |
| Monthly switch | Saved per brand (admin only) |

## 9. Current Snapshot (read on 20 Nov 2026)

- **18 brands** have a document. Most are on v1; Alliance Street, Asics, Chaat Bazaar, Decode Age on v2; Sotheby's Motorsport on v3; Origin Nutrition on v4 (17 Nov 2026).
- **453 approved blogs** across 12 brands (Asics 162, Alliance Street 96, Chaat Bazaar 70, Suncasa 42).
- **1 brand book** in use: Origin Nutrition Brand Playbook (Nov 2025).
- **23 reviews** across 4 brands (Sotheby's Motorsport 18, Alliance Street 2, Perona 2, Asics 1).
- **Monthly switch:** on for Earthful; off for IITM Sonipat and Sotheby's Motorsport; not set elsewhere.

---

## 10. Things to Know (observed, not changed)

1. **Only admins can actually generate.** Sub-admins and internal staff see Generate but get "Admin only"; their blog list loads empty because blog records are admin-only.
2. **"Auto-refresh monthly" saves a setting only.** Nothing re-generates documents each month yet, so it has no effect (including for Earthful).
3. **The automatic sync can remove blogs.** Each time an admin opens the page, link-imported blogs no longer approved in Deployment › Blogs are deleted from the list. Pasted blogs are safe.
4. **Alternate brand names:** the page shows blogs under either name, but **generation only uses blogs saved under the exact selected name**.
5. The welcome tour says "Every AI tool on the platform writes using this voice", but **no other tool** (Blog Generator, FAQ Generator etc.) currently reads the document.
6. **Brand book has no upload button**; adding or replacing it needs a team-side step.
7. **Activity tracking:** the time tracker looks for a different page address, so time here may not be labelled "Brand Voice" in activity reports.
8. **Earthful** has only 2 approved blogs (3 needed without a brand book). Its existing v1 stays in place.
