# Intelligence → Prompt Planner

| | |
|---|---|
| **Route** | `/analytics/prompt-research` (the route sits under `/analytics` although the sidebar lists it in INTELLIGENCE) |
| **Page title** | Prompt Planner (with a **BETA** badge at the right) |
| **Subtitle** | "Discover related topics, prompts, brands and sources" |
| **Breadcrumb** | DareAISearch › {Brand} › Analytics › Prompt Planner **Beta** |
| **Sidebar location** | INTELLIGENCE group → Prompt Planner (2nd item, **BETA** badge) |
| **Shared shell** | Documented in [../updated analytics/00-global-layout.md](../updated%20analytics/00-global-layout.md) |

> Documented from the live app. The page was seen with **no research run**, so the column layout of every tab is confirmed but **filled rows are not captured**. Run Research was not pressed. Text in quotes is exact on-screen text.

---

## 1. Purpose

A research tool: the user types a **topic**, picks an AI engine and runs research. The page then lists related topics, the prompts people ask about them, the brands the AI answers mention, and the source domains it cites. It is used to decide which prompts and topics to target.

---

## 2. Page sections (top to bottom)

| # | Section | Contents |
|---|---|---|
| 1 | Page header | Title, subtitle, BETA badge |
| 2 | Research bar | Topic box · engine dropdown · Run Research · Refresh Data |
| 3 | Result tabs | Related Topics · Prompts · Brands · Source Domains |
| 4 | Results table | Table toolbar and the table for the selected tab |

---

## 3. Section details

### 3.1 Research bar
A single rounded bar across the page.

| Element | Details |
|---|---|
| Topic box | Search icon, placeholder **"Enter a topic to analyze"**, wide |
| Engine dropdown | Default **ChatGPT**. Options: **ChatGPT**, **Gemini** |
| **Run Research** | Teal filled button. Runs the query for the typed topic and engine |
| **Refresh Data** | Outlined button with a refresh icon. Reloads the current results |

### 3.2 Result tabs
A pill group; **Related Topics** is selected by default. The same toolbar is shown on every tab.

| Element | Details |
|---|---|
| Hint text | **"Enter a topic above to begin"** (left of the toolbar) |
| Search box | Placeholder "Search…", filters the rows |
| Page size | Dropdown, default **"25 / page"** |
| Empty state (every tab) | **"Run a research query to see results."** |

### 3.3 Tables by tab
All column headers are sortable (arrow icon).

| Tab | Columns |
|---|---|
| Related Topics | **Topic** · **Volume** (default sort, descending) · **Prompts Count** · **Relevance Score** |
| Prompts | **Prompt** · **Model** · **Brands** · **Sources** · **Relevance** |
| Brands | **Brand** · **Domain** · **Example Prompt** · **Mentions** · **Source Domains** |
| Source Domains | **Domain** · **Example Prompt** · **Mentions** · **Sources** · **Organic Traffic** |

Column meaning (inferred from the names; values not captured): Volume is the demand for the topic; Prompts Count is how many prompts relate to it; Relevance is how close a topic or prompt is to the topic typed; Brands and Sources count the brands and cited sources in the AI answers; Mentions counts how often a brand or domain appears.

---

## 4. UI element inventory

### Buttons, dropdowns and toggles
| Control | Type | Action |
|---|---|---|
| Topic box | Text input | Topic to research |
| ChatGPT / Gemini | Dropdown | Choose the AI engine |
| Run Research | Button | Run the query |
| Refresh Data | Button | Reload results |
| Related Topics / Prompts / Brands / Source Domains | Tabs | Switch result view |
| Search… | Text input | Filter table rows |
| 25 / page | Dropdown | Rows per page |
| Column headers | Sort arrows | Sort the table |

### Badges and labels
| Label | Where | Meaning |
|---|---|---|
| BETA | Header (top right), sidebar item, breadcrumb | Feature still in beta |

### Not present on this page
Date filters, AI insight line, Recommended Actions, export, ⓘ tooltips.

---

## 5. Data sources and API calls

| Data block | Call | Input |
|---|---|---|
| Results | Not captured | The page made **no data call on load**; results load only after **Run Research** |

Only the shell calls (subscription, profile, role checks, notifications) were seen.

---

## 6. Behaviour rules

- **Starts empty:** nothing loads until a topic is entered and **Run Research** is pressed.
- **Engine choice:** the default engine is ChatGPT; Gemini is the only other option.
- **Same view for Pro User and Sub-Admin:** no difference was seen between the two roles.
- **Access control:** the app has a permission check for selecting prompts (`get_prompt_selection_access`); whether this page uses it was not confirmed.
