# Intelligence → Blog Generator

| | |
|---|---|
| **Route** | `/blog-generator-v2` |
| **Page title** | Blog Generator |
| **Subtitle** | The brand name in capitals, for example "{BRAND}" |
| **Breadcrumb** | DareAISearch › {Brand} › Blog Generator |
| **Sidebar location** | INTELLIGENCE group → Blog Generator (3rd item) |
| **Shared shell** | Documented in [../doc analytics/00-global-layout.md](../doc%20analytics/00-global-layout.md) |

> Documented from the live app, **Sub-Admin** view. One brand had a single request and two brands had none. The New request dialog and the request drawer were opened but **nothing was submitted, approved or rejected**, so the steps after approval (assigning the research, proposing or generating a topic, the blog itself) are **not captured**. Names, emails, dates and counts are placeholders such as `{n}`. Text in quotes is exact on-screen text.

---

## 1. Purpose

A request board for blog topics. A request starts as a **keyword** (optionally with secondary keywords and a ranked prompt). It is reviewed internally, then handed to a team member who generates or writes a topic for it, and the topic leads to a blog. The page lists every request for the brand with its status.

---

## 2. Page sections (top to bottom)

| # | Section | Contents |
|---|---|---|
| 1 | Page header | Title, brand name, and two buttons at the right: **Columns** and **New request** |
| 2 | Requests card | Heading with count, month filter, search box, requests table |

---

## 3. Section details

### 3.1 Header buttons
| Control | Details |
|---|---|
| **Columns** | Outlined button with a columns icon. Opens a menu to show or hide table columns (section 3.4) |
| **New request** | Teal filled button with a plus icon. Opens the New request dialog (section 3.5) |

### 3.2 Requests card
| Element | Details |
|---|---|
| Heading | **Requests** with a round count chip, "{n}" |
| Month filter | Dropdown, default **All months**; then one entry per month that has requests, shown as "{Month YYYY}" |
| Search box | Placeholder **"Search keyword, topic or person"** |

### 3.3 Requests table
| Column | Content |
|---|---|
| (first, narrow) | Empty narrow cell before the row number; its purpose was not determined |
| **#** | Row number |
| **PRIMARY KEYWORD** | The keyword, in bold |
| **SECONDARY** | Secondary keywords, or "—" |
| **PROMPT** | The linked ranked prompt, or "—" |
| **FINALIZED TOPIC** | The agreed topic, or the italic text "No topic yet" |
| **TOPIC STATUS** | Coloured dot and label. Seen: **Awaiting internal review** (amber). Other statuses were not captured |
| **ASSIGNED TO** | Team member, or italic "Not assigned" |
| **BLOG** | Link to the blog once it exists, or "—" |
| **RAISED BY** | Round initials badge and the email of the person who raised the request |
| **ACT** | Edit icon button ("Open actions") that opens the request drawer |

Empty state when a brand has no requests: **"Nothing here yet. Raise a request to get started."** (counter shows 0).

### 3.4 Columns menu
Small panel with the note **"Shown to brand users too. Drag headers to reorder."**, a check box per column — **#, Primary keyword, Secondary, Prompt, Finalized Topic, Topic status, Assigned to, Blog, Raised by** — and a **Reset columns** link. The note means the chosen columns apply to the brand's own users as well, not only to the person who changed them.

### 3.5 New request dialog
Title **New request**, sub-line "For {BRAND}". Closes with the X.

| Element | Details |
|---|---|
| **Upload a sheet (optional)** | Block at the top with a **Sample sheet** download link, the rule **"Columns must be exactly: Primary Keyword, Secondary Keyword (comma separated), Prompt (one per line), Finalized Topic. Each row becomes its own request."** and a **Choose file** button |
| Primary keyword * | Required. Search-and-pick box, placeholder "Search your keywords, or type one" (suggests the brand's tracked keywords, or accepts a new one) |
| Secondary keywords | Search-or-type box, placeholder "Search or type, press Enter", with an **Add** button; added keywords become chips |
| Prompt (optional) | Search-and-pick box, placeholder "Pick from your ranked prompts" |
| Notes | Multi-line box, placeholder "Anything the topic should take into account" |
| Hand the research to (optional) | Dropdown, default **Keep it with me**. The other options are team members, each shown as "{email} · {Content or SEO}". Help line: **"They can generate topics with AI or add topics themselves for this request."** |
| Buttons | **Cancel** · **Submit request** |

### 3.6 Request drawer (Act button)
A panel from the right with an X to close.

| Part | Details |
|---|---|
| Header | Keyword (large) and the origin label, for example **Brand-submitted** |
| DETAILS | Secondary, Prompt, Raised by |
| INTERNAL REVIEW | Status chip (**Awaiting internal review**), a note box **"Add a note (required to reject)"**, and two buttons: teal **Approve** and dark-red **Reject** |
| FINALIZED TOPIC | While unreviewed: **"Approve this keyword/prompt idea first — then you can assign it or propose a topic."** and "No topic yet." After approval the assign and propose-topic controls presumably appear there (**not captured**) |
| ACTIVITY | Log of what happened to the request; "Nothing logged yet." when new |

---

## 4. UI element inventory

### Buttons, dropdowns and toggles
| Control | Where | Action |
|---|---|---|
| Columns | Header | Show, hide, reset columns |
| New request | Header | Open the request dialog |
| All months | Requests card | Filter by month |
| Search keyword, topic or person | Requests card | Filter rows |
| Edit icon (ACT) | Each row | Open the request drawer |
| Sample sheet / Choose file | New request | Download the template, upload a sheet of requests |
| Primary keyword, Secondary keywords + Add, Prompt, Notes | New request | Request details |
| Hand the research to | New request | Choose who does the research |
| Cancel / Submit request | New request | Close, or raise the request |
| Approve / Reject | Drawer | Review decision (note required for Reject) |

### Not present on this page
Date range picker, AI insight line, Recommended Actions, ⓘ tooltips, pagination.

### Status and empty states
| State | Text |
|---|---|
| Topic not set | "No topic yet" |
| Not assigned | "Not assigned" |
| Under review | "Awaiting internal review" |
| Brand has no requests | "Nothing here yet. Raise a request to get started." |
| Drawer, not reviewed | "Approve this keyword/prompt idea first — then you can assign it or propose a topic." |

---

## 5. Data sources and API calls

| Data block | Call | Input |
|---|---|---|
| Team members (assignee list) | `GET team_members` | select, limited |
| Column layout | `GET blog_column_layouts` | brand name |
| Brand | `GET brands` | name, limited |
| Brand reference | `POST rpc/get_blog_v2_brand_ref` | `{ _name: "{Brand}" }` |
| Requests | `GET blog_topic_generation_v2` | brand id, ordered, limited |

The calls behind Submit request, Approve, Reject and topic generation were not captured because those actions were not run.

---

## 6. Behaviour rules

- **Brand scoped:** the board shows only the selected brand's requests; two of the three brands tested had none.
- **Review before work:** a new request is **Awaiting internal review**; it must be approved before it can be assigned or given a topic. Rejecting needs a written note.
- **One keyword, one request:** a sheet upload creates one request per row.
- **Hand-off:** the requester can keep the research or hand it to a Content or SEO team member, who can generate topics with AI or add them by hand.
- **Shared layout:** the saved column layout is stored per brand (`blog_column_layouts`) and is also seen by the brand's own users.