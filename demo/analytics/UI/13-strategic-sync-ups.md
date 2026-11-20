# Analytics → Strategic Sync-ups

| | |
|---|---|
| **Route** | `/analytics/brand-mom` |
| **Page title** | Strategic Sync-ups |
| **Subtitle** | "AI-powered Minutes of Meeting — Extract tasks, decisions & summaries automatically" |
| **Breadcrumb** | DareAISearch › {Brand} › Analytics › Strategic Sync-ups |
| **Sidebar location** | ANALYTICS group → Strategic Sync-ups (last item) |
| **Shared shell** | Top bar, sidebar, breadcrumb and the Miss Daring assistant are documented in [00-global-layout.md](00-global-layout.md) |

> Documented from the live app, using a brand that has meetings (list and detail) and brands that have none (empty state). This page is documented on its own; how its data connects to other pages is left for a later pass. Names, dates and notes are **placeholders such as `{n}`**. Text in quotes is exact on-screen text.
>
> **Not exercised (to avoid changing a live client's records):** the **New Meeting → Process with AI** submission and the AI output of a brand-new meeting, **Regenerate**, the edit forms behind the pencil icons, **Add Decision**, and the delete icons on meeting cards. These controls are listed, but their forms and results are not documented.

---

## 1. Purpose

Lets the team record **minutes of meeting (MoM)** for a brand: raw notes are pasted in, an AI extracts a **summary, tasks (DAIS-side and brand-side) and decisions**, and the result can be edited. Saved meetings are listed and searchable.

---

## 2. Views

| View | When shown |
|---|---|
| **Meeting list** | Default view of the route |
| **Empty state** | List view when the brand has no meetings |
| **Meeting detail** | After clicking a meeting card (same route, the URL does not change) |
| **New Meeting Notes dialog** | After clicking either **New Meeting** button |

---

## 3. Meeting list

### 3.1 Toolbar
| Element | Details |
|---|---|
| **Search box** | Full-width, magnifier icon, placeholder **"Search meetings..."**. Filters the list as you type; matches text in the meeting (e.g. words from the title or summary) |
| **New Meeting** | Teal filled button with **+**, right of the search box. Opens the New Meeting Notes dialog |
| No-match message | **"No matches found"** with the sub-text **"Try a different search term."** |

### 3.2 Meeting card
Cards stacked vertically, newest meeting first.

| Part | Details |
|---|---|
| Title | Bold meeting title |
| Status badge | Small green pill, e.g. **processed** |
| Date | Calendar icon + `{DD Mon YYYY}` |
| Brand | Building icon + brand name |
| Summary | Grey paragraph: the AI-written summary |
| Count chips | Icons with counts, shown only when greater than zero: **"{n} internal"** (DAIS-side tasks), **"{n} brand"** (brand-side tasks), **"{n} decisions"** |
| Delete | Trash icon button per card (not exercised) |

Clicking a card opens the **Meeting detail**.

### 3.3 Empty state
| Element | Details |
|---|---|
| Icon | Brain icon (grey outline) |
| Heading | **No meetings yet** |
| Message | "Create your first AI-powered meeting notes to get started." |
| Button | Second teal **+ New Meeting** button |

---

## 4. Meeting detail

### 4.1 Header
| Element | Details |
|---|---|
| **←** | Back arrow, returns to the list |
| Title | Meeting title (large) |
| Meta line | Calendar icon + `{DD Mon YYYY}`, building icon + brand, people icon + attendees (comma-separated) |
| Status badge | **processed** (green pill), top-right |
| **Regenerate** | Outlined button with a refresh icon, top-right (not exercised; presumably re-runs the AI on the original notes) |

### 4.2 Meeting Summary
Card with a brain icon and heading **Meeting Summary**.
| Element | Details |
|---|---|
| Sentiment badge | Pill, e.g. **Neutral** (with a dash icon) |
| Urgency badge | Pill, e.g. **High Urgency** (red) |
| Edit | Pencil icon at the right |
| Text | The AI summary paragraph |

### 4.3 DAIS Tasks and Brand-Side Tasks
Two cards with the same structure: **DAIS Tasks** (internal team) and **Brand-Side Tasks** (client team). Each has a count badge at the top-right.

| Column | Description |
|---|---|
| **Task** | Task description |
| **Assigned To** | Team or person (bold), or **—** |
| **Priority** | Pill: **high** (red), **medium** (green/neutral); a low value is expected but was not seen |
| **Status** | Pill, e.g. **pending** |
| **Due Date** | `{YYYY-MM-DD}` or **—** |
| (actions) | Pencil (edit) and trash (delete) icons per row |

- Empty states: **"No internal team tasks yet."** and **"No brand-side tasks yet."**
- **+ Add Task** button below each table. **Observed behaviour:** clicking it **immediately saves** a placeholder task (text "New task", priority medium, status pending, no assignee or date) and shows it with an "(edited)" marker; there is no form step before saving. The row can then be edited with its pencil icon.
- The delete (trash) icon on a task removes it **immediately, with no confirmation dialog**.

### 4.4 Decisions Taken
Card with a gavel icon, heading **Decisions Taken** and a count badge.
| Element | Details |
|---|---|
| Decision row | Teal target icon, decision text, italic sub-line **"Original: {text from the raw notes}"**, category pill (e.g. **Strategic**), pencil and trash icons |
| Empty state | **"No decisions yet."** |
| **+ Add Decision** | Button below the list (not exercised; assumed to behave like Add Task) |

### 4.5 Original Notes
Collapsible card (chevron at the right) titled **Original Notes**. Expanding it shows the raw notes exactly as entered, one line per point.

---

## 5. New Meeting Notes dialog
A centred modal with a dimmed background. Header: sparkle icon + **New Meeting Notes**, **✕** at the top-right.

| Field | Type | Details |
|---|---|---|
| **Meeting Title** | Text input, placeholder "e.g. Weekly Sync Call" | Optional; focused when the dialog opens |
| **Meeting Date** | Date button with calendar icon, default today (`{D Mon YYYY}`) | Single-month calendar, no disabled days |
| **Brand** | Text input, pre-filled with the current brand, placeholder "e.g. Decode Age" | Editable |
| **Attendees** | Text input, placeholder "e.g. Rahul, Priya, Client team" | Comma-separated names. Suggestion chips with team-member names sit below; clicking a chip adds the name, clicking again removes it |
| **Raw Meeting Notes \*** | Multi-line text area (required) | Placeholder "Paste or write your raw meeting notes here in any language, any format. The AI will handle the rest…" plus a four-bullet example. Helper text: "Write freely — AI will extract tasks, decisions & summary automatically." |

| Button | Behaviour |
|---|---|
| **Cancel** | Closes the dialog without saving |
| **Process with AI** | Disabled while Raw Meeting Notes is empty; enabled once any notes are typed. Saves the meeting and sends the notes for AI processing |
| **✕ / Close** | Closes the dialog |

---

## 6. UI element inventory

### Buttons, dropdowns and toggles
| Element | Location | Type |
|---|---|---|
| Search meetings… | List toolbar | Text search |
| New Meeting (×2) | Toolbar and empty state | Opens the dialog |
| Meeting cards | List | Open detail |
| Trash on card | List | Delete meeting |
| ← | Detail header | Back to list |
| Regenerate | Detail header | Re-run AI |
| Pencil / trash icons | Summary, tasks, decisions | Edit / delete |
| Add Task / Add Decision | Detail cards | Add item |
| Original Notes chevron | Detail | Expand / collapse |
| Dialog fields and buttons | Dialog | See section 5 |

### Not present on this page
Tabs, filters other than search, pagination, export, ⓘ tooltips, AI insight line, Recommended Actions.

### Badges and labels
| Label | Where | Meaning |
|---|---|---|
| processed | Card and detail | AI processing finished |
| Neutral / High Urgency | Summary | Sentiment and urgency of the meeting |
| high / medium, pending | Task rows | Priority and status |
| Strategic | Decision row | Decision category |
| {n} internal / {n} brand / {n} decisions | Card | Counts |
| (edited) | After task text | Item was added or changed manually |

### Status and empty states
| Message | Where |
|---|---|
| "No meetings yet" | List with no meetings |
| "No matches found" / "Try a different search term." | List, search without result |
| "No internal team tasks yet." / "No brand-side tasks yet." / "No decisions yet." | Detail sections |

---

## 7. Data sources and API calls (all `POST manage-mom`)

| Purpose | Body |
|---|---|
| List meetings | `{ "action": "list", "brand_name": "{Brand}" }` |
| Open a meeting | `{ "action": "get", "meetingId": "{uuid}" }` |
| Add a task | `{ "action": "add_item", "table": "mom_action_items", "meetingId": "{uuid}", "data": { "task_type": "{internal or brand}", … } }` |
| Delete a task | `{ "action": "delete_item", "table": "mom_action_items", "id": "{uuid}" }` |
| Create a meeting (not run) | `manage-mom` with a create/process action; fields from the dialog |
| Brand access | `GET sub_admin_brands` (select `user_id`, filter `brand_name`) |
| Names for chips and permissions | `GET profiles` (name, email, brand_name, website_url, team_type) |
| Role checks | `POST rpc/has_role` for `admin`, `sub_admin`, `internal_team` |
| Usage tracking | `POST user_page_sessions` (`page_path: "/analytics/brand-mom"`) |

Shell calls are listed in [00-global-layout.md](00-global-layout.md) section 5. This is the only analytics page that **writes** data.

---

## 8. Behaviour rules

- **Brand scoped:** the list is for the selected brand; the dialog's Brand field is pre-filled but editable.
- **Required input:** only the raw notes are required.
- **AI output:** summary, sentiment, urgency, tasks (split into DAIS-side and brand-side), decisions and their "Original" source line come from the AI after **Process with AI**.
- **Immediate saves:** Add Task and delete actions save at once (no confirmation); treat them as live edits.
- **Role-aware:** the page loads the user's roles (admin, sub-admin, internal team) and sub-admin brand assignments.
