# Intelligence → YouTube Intelligence

| | |
|---|---|
| **Route** | `/youtube-intelligence` |
| **Page title** | YouTube Intelligence |
| **Subtitle** | None in the header; a tagline sits in the page body |
| **Breadcrumb** | DareAISearch › {Brand} › YouTube Intelligence |
| **Sidebar location** | INTELLIGENCE group → YouTube Intelligence (5th item) |
| **Shared shell** | Documented in [../doc analytics/00-global-layout.md](../doc%20analytics/00-global-layout.md) |

> Documented from the live app. The page and its input form were captured; **Generate YouTube Title & Description was not submitted**, and no brand tested had saved results, so the generated output and the saved-result list are **not captured**. Text in quotes is exact on-screen text.

---

## 1. Purpose

Generates AI-written YouTube **titles and descriptions**, with content strategy and optimisation insights, for a video the brand plans. The user gives the idea, a keyword from the brand's Keyword Ranking and a prompt from its Prompt Ranking. Each result is stored and listed on the page.

---

## 2. Page sections (top to bottom)

| # | Section | Contents |
|---|---|---|
| 1 | Page title | "YouTube Intelligence" |
| 2 | Intro block | Red circle icon with a play symbol, tagline |
| 3 | Generate card | Description text and the generate button |

---

## 3. Section details

### 3.1 Intro block
Centred. A round dark-red badge with a red YouTube-style play icon, and under it the tagline **"AI-powered YouTube content intelligence for your brand"**.

### 3.2 Generate card
Same layout as the FAQ Creator card.

| Element | Details |
|---|---|
| Text | **"Generate AI-powered YouTube content strategy and optimization insights."** |
| **Generate YouTube Title & Description** | Teal filled button. Opens the **YouTube Intelligence** form dialog |

### 3.3 YouTube Intelligence form (dialog)
Red play icon + title **YouTube Intelligence**, text "Enter your video details for AI-powered analysis." Closes with the X at the top right. A star (*) marks required fields.

| Field | Type | Details |
|---|---|---|
| Video Idea * | Text box | Placeholder "e.g. How to choose the right running shoes for your gait". Has focus when the dialog opens |
| Primary Keyword * | Search-and-pick box | Placeholder "e.g. best running shoes 2026". A chip shows **"{n} from Keyword Ranking"**, the number of the brand's tracked keywords offered as suggestions |
| Target Prompt | Search-and-pick box (optional) | Placeholder "e.g. What are the best running shoes for beginners?". A chip shows **"{n} from Prompt Ranking"** |
| Tone | Dropdown, default "Select tone" | **Professional** · **Casual** · **Educational** · **Entertaining** · **Inspirational** |
| Optional Context | Multi-line box | Placeholder "e.g. Highlight {brand} technology like {feature}…" |
| **Generate YouTube Title & Description** | Wide teal button with a sparkle icon | Submits the form |

### 3.4 Saved results
The page loads the user's earlier results, newest first. None existed for the brands tested, so how they are displayed is **not captured**.

---

## 4. UI element inventory

### Buttons, dropdowns and toggles
| Control | Where | Action |
|---|---|---|
| Generate YouTube Title & Description | Page card | Open the form |
| Video Idea, Primary Keyword, Target Prompt, Tone, Optional Context | Form | Inputs |
| Generate YouTube Title & Description | Form | Submit |
| X | Form | Close |

### Not present on this page
Filters, tabs, search box on the page itself, AI insight line, Recommended Actions, ⓘ tooltips, export.

### Status and empty states
| State | Text |
|---|---|
| No saved results | Intro and generate card only, no error message |

---

## 5. Data sources and API calls

| Data block | Call | Input |
|---|---|---|
| Count of saved results | `HEAD youtube_intelligence_results` | filtered by `user_id` |
| Saved results | `GET youtube_intelligence_results` | `user_id`, ordered by `created_at` |
| Keyword and prompt suggestions | Not captured | Taken from the brand's Keyword Ranking and Prompt Ranking |
| Generation | Not captured | Starts when the form is submitted |

---

## 6. Behaviour rules

- **Brand scoped suggestions, user scoped storage:** keyword and prompt suggestions come from the selected brand; saved results are stored per **user** (`user_id`).
- **Required fields:** Video Idea and Primary Keyword must be filled; Target Prompt, Tone and Optional Context are optional.
- **Newest first:** saved results are ordered by creation time.
- **Different from YouTube Analytics:** this page *creates* title and description suggestions; the YouTube Analytics page only *reports* on existing videos.
- **Same view for Pro User and Sub-Admin:** no difference was seen.
