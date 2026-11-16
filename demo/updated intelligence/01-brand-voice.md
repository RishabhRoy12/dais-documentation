# Intelligence → Brand Voice

| | |
|---|---|
| **Route** | `/intelligence/brand-voice` |
| **Page title** | Brand Voice |
| **Subtitle** | "AI-powered brand voice generation and content review" |
| **Breadcrumb** | DareAISearch › {Brand} › Brand Voice |
| **Sidebar location** | INTELLIGENCE group → Brand Voice (1st item) |
| **Shared shell** | Top bar, sidebar, breadcrumb and the Miss Daring assistant are documented in [../updated analytics/00-global-layout.md](../updated%20analytics/00-global-layout.md) |

> Documented from the live app. The full page below is the **Sub-Admin** view, captured on a brand that already has a generated brand voice and one saved content review. A **Pro User** view of a brand with no voice was captured earlier and is described in section 7, because the tab name and layout differ. Brand names, dates and counts are placeholders such as `{n}`. Text in quotes is exact on-screen text. The Generate, Regenerate and Review actions were **not run**, so what they do while running is not documented.

---

## 1. Purpose

Builds a written **brand voice document** for the selected brand from the blogs the brand has approved, and then **reviews any draft content against that voice**. The voice document is the reference for tone, structure, SEO and wording used when content is written for the brand.

---

## 2. Page sections (top to bottom)

| # | Section | Contents |
|---|---|---|
| 1 | Page header | Title and subtitle |
| 2 | Tab switch | **Brand Voice Generator** (default) · **Brand Voice Review** |
| 3 | Tab content | Two side-by-side cards for the selected tab |

The tab switch is a rounded pill group; the active tab has a darker filled background.

---

## 3. Tab: Brand Voice Generator

Two cards side by side: **Approved Blogs** (left) and **Brand Voice Document** (right).

### 3.1 Approved Blogs card (left)
| Element | Details |
|---|---|
| Heading | **Approved Blogs** |
| Counter | "{n} blogs added" |
| Sync status | Small spinner with **"Syncing from Deployment…"** while blogs are being pulled in from the brand's Blogs deployment |
| **Add Blog** | Teal filled button with a plus icon. Opens the Add Approved Blog dialog (section 3.3) |
| Blog list | The added blogs. When none: document icon and **"No approved blogs yet. Add at least 3 to generate."** |
| **Generate Brand Voice** | Wide teal button with a sparkle icon, at the bottom. **Disabled** until at least **3** blogs exist; the line below it then reads **"Add {n} more blogs to enable generation."** |
| Last generated line | "Last generated {D Mon YYYY, hh:mm am/pm} · v{n}" (shown once a voice exists) |
| **Auto-refresh monthly** | Bold label with a switch (off by default) and the note **"Re-generate the brand voice each month automatically."** |

### 3.2 Brand Voice Document card (right)
| Element | Details |
|---|---|
| Heading | Sparkle icon + **Brand Voice Document** |
| Sub-line | `{Brand}` · version chip **v{n}** · source chip (**AI Refreshed** or **AI Generated**) · "· Updated {D Mon YYYY, hh:mm am/pm}" |
| **History** | Outlined button. Opens the version drawer (below) |
| **Copy** | Outlined button. Copies the whole document |
| **Regenerate** | Outlined button with a refresh icon. Creates a new version from the current approved blogs |
| Search box | "Search this brand voice…" |
| Section chips | 12 numbered chips that jump to a section (list below) |
| Overview card | Label **OVERVIEW** and a two-to-three sentence summary of the voice, in italics |
| Document body | The 12 sections, each with a numbered heading, a copy icon at its right and sub-headings with bullet lists |

**The 12 sections**
| # | Section | What it holds |
|---|---|---|
| 1 | Brand Understanding | What the brand does, who it serves, category and positioning, customer problems solved, what makes it different |
| 2 | Target Audience | Primary and secondary audiences, demographics and psychographics, motivations and pain points, decision criteria, content expectations |
| 3 | Brand Voice Summary | Short list of voice traits |
| 4 | Writing Style | Sentence and paragraph length, structure and formatting, balance and technicality, use of data and frameworks, tone and formality |
| 5 | Blog Structure Guidelines | Standard blog skeleton with word range, heading patterns, recurring closers |
| 6 | SEO & GEO Guidelines | Keyword use, structure for AI and answer engines, internal linking, regional nuance |
| 7 | Language Guidelines | Spelling, naming and wording rules |
| 8 | Do's and Don'ts | Dos and don'ts |
| 9 | CTA Guidelines | How calls to action are written |
| 10 | Approved Content Patterns | Reusable patterns found in approved content |
| 11 | Content Examples | Sample lines and sections |
| 12 | Quality Checklist | Final checks before content goes out |

The section list is the same for every brand; the text inside is generated for the brand.

**Version drawer (History)** — a side panel from the right, titled **Brand Voice History**, "All generated versions for {Brand}."
| Part | Details |
|---|---|
| Row | Version chip (**v{n}**) · source chip (**AI Generated** for a first version, **AI Refreshed** for later ones) · **Active** chip on the current version · "{D Mon YYYY, hh:mm am/pm} · {n} blogs" |
| Close | **Close** button and an X at the top right |

### 3.3 Add Approved Blog dialog
Title **Add Approved Blog**, text "Paste the blog content directly or import it from a URL. Add a clear title."

| Element | Details |
|---|---|
| Blog Title | Text box |
| **Paste Content** tab | Large text box with a live word counter ("{n} words") |
| **Import from URL** tab | URL box with a **Fetch** button that pulls the blog text |
| Buttons | **Cancel** · **Save Blog** |

---

## 4. Tab: Brand Voice Review

Two cards side by side: **Content Input** (left) and **Review Output** (right).

### 4.1 Content Input
| Element | Details |
|---|---|
| Heading | Document icon + **Content Input** |
| **History** | Outlined button. Opens **Review History** drawer (below) |
| **Upload .txt** | Outlined button. Loads a text file into the draft box |
| Content Title (optional) | Text box, placeholder "e.g. Spring sale landing page draft" |
| Content Draft | Large monospaced text box, placeholder "Paste your blog, landing page, FAQ, product description or social caption here…" |
| Word counter | "{n} words" under the box |
| **Review Content** | Wide teal button with a sparkle icon. Sends the draft for review |

**Review History drawer** — title **Review History**, "Past content reviews for {Brand}. Click a row to reload it."
| Part | Details |
|---|---|
| Row | Bold title · "{D Mon, hh:mm am/pm} · {n} words" · verdict chip (for example **Needs Revision — {short reason}**) · counts ✓ {n} approved, ✗ {n} disapproved, ⚠ {n} needs revision |
| Click a row | Reloads that review: the title and draft go back into Content Input and the result into Review Output |

### 4.2 Review Output
**Before a review:** centred text **"Paste your content on the left to get a brand voice review broken down into Approved, Disapproved and Needs Revision."**

**After a review:**
| Element | Details |
|---|---|
| **Copy Report** | Outlined button at the top right. Copies the full report |
| Summary card | Sparkle icon, content title (bold) and a one-line verdict, for example "Needs Revision — {reasons}" |
| Count tabs | Three tabs with a count each: **Approved** ({n}) · **Disapproved** ({n}) · **Needs Revision** ({n}). **Needs Revision** is selected by default in the sampled review |
| Reason list | Numbered cards, each with a bold title and a one-line explanation. The list heading depends on the tab: **WHAT NEEDS TO BE CHANGED** (Needs Revision), **WHY APPROVED** (Approved), **WHY NOT APPROVED** (Disapproved) |
| **Full Scorecard ({n})** | Expandable table with columns **Parameter · Score · Comments** |
| **Full Report (Markdown)** | Expandable full written report |

**Scorecard parameters (9)**
| Parameter | Score format |
|---|---|
| Brand Voice Alignment | {n}/100 |
| Tone Consistency | {n}/100 |
| Writing Quality | {n}/100 |
| Audience Relevance | {n}/100 |
| SEO Readiness | {n}/100 |
| AI Search Readiness | {n}/100 |
| Structure & Flow | {n}/100 |
| CTA Quality | {n}/100 |
| Product/Brand Mention Quality | {n}/100 |

The Markdown report adds a tenth row, **Revision Risk** (High / Medium / Low), and an **Overall Score** out of 100.

**Full report sections (11)**
1. Overall Verdict · 2. Scorecard · 3. What Is Working Well · 4. Brand Voice Gaps (table: Issue, Why It Is a Problem, Suggested Fix) · 5. SEO Review (intent, primary keyword, headings, on-page basics, semantic coverage, internal links, meta title and description suggestions) · 6. AI Search / GEO Review · 7. Line-Level Feedback (table: Current Line/Section, Issue, Suggested Rewrite) · 8. Missing Opportunities · 9. Rewritten Sections · 10. Final Checklist (table of checks with Yes / Partly / No) · 11. Final Recommendation

---

## 5. UI element inventory

### Buttons, dropdowns and toggles
| Control | Where | Action |
|---|---|---|
| Brand Voice Generator / Brand Voice Review | Tab switch | Switch tab |
| Add Blog | Approved Blogs | Open Add Approved Blog dialog |
| Paste Content / Import from URL / Fetch | Add Blog dialog | Choose how to add the blog; fetch the URL text |
| Cancel / Save Blog | Add Blog dialog | Close, or save the blog |
| Generate Brand Voice | Approved Blogs | Create the first voice (needs 3+ blogs) |
| Auto-refresh monthly | Approved Blogs | Switch on or off monthly regeneration |
| History | Document card | Open version drawer |
| Copy | Document card, each section | Copy the document, or that section |
| Regenerate | Document card | Create a new version |
| Search this brand voice… | Document card | Search the document text |
| Numbered section chips | Document card | Jump to a section |
| History | Content Input | Open Review History drawer |
| Upload .txt | Content Input | Load a text file |
| Review Content | Content Input | Run the review |
| Approved / Disapproved / Needs Revision | Review Output | Switch reason list |
| Copy Report | Review Output | Copy the report |
| Full Scorecard, Full Report (Markdown) | Review Output | Expand details |

### Not present on this page
Date filters, AI insight line, Recommended Actions, ⓘ tooltips, download or export file.

### Status and empty states
| State | Text |
|---|---|
| No approved blogs | "No approved blogs yet. Add at least 3 to generate." |
| Generate blocked | "Add {n} more blogs to enable generation." |
| Blogs syncing | "Syncing from Deployment…" |
| No voice yet (Sub-Admin) | "No brand voice document yet. Add at least 3 approved blogs and click Generate Brand Voice." |
| No review yet | "Paste your content on the left to get a brand voice review broken down into Approved, Disapproved and Needs Revision." |

---

## 6. Data sources and API calls

| Data block | Call | Input |
|---|---|---|
| Voice settings (auto-refresh) | `GET brand_voice_settings` | brand name |
| Voice versions | `GET brand_voices` | brand name, `is_active`, ordered, limited |
| Source documents | `GET brand_voice_source_docs` | brand name, `is_primary`, ordered, limited |
| Approved blogs | `GET brand_voice_blogs` | brand name, ordered |
| Blogs from the deployment | `POST fetch-execution-blogs` | `{ brandOverride: "{Brand}" }` |

Shell calls are listed in the global layout document, section 5. The calls for Generate, Regenerate and Review were not captured because those actions were not run.

---

## 7. Behaviour rules and differences by role

- **Brand scoped:** the page follows the brand selected in the top bar; each brand has its own blogs, voice versions and review history.
- **Three-blog minimum:** the voice cannot be generated until at least 3 approved blogs exist.
- **Versions:** every generation or monthly refresh adds a version; exactly one is **Active** and is the one shown. Each version records how many blogs it used (the sampled brand's v2 used more blogs than the Approved Blogs card listed, so the card does not always show every blog behind a version).
- **Reviews are checked against the active voice** and are saved to Review History per brand.
- **Pro User view (earlier capture):** the first tab is named **Brand Voice Document** and shows a single card with the heading, the brand name, a **History** button and, when no voice exists, **"The brand voice document is being prepared. It will appear here once it's ready."** The Approved Blogs panel, Generate, Add Blog and Auto-refresh controls were not visible in that captured view (their names were found in the page markup, so they may exist for that role in a state that was not seen).
