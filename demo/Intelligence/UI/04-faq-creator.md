# Intelligence → FAQ Creator

| | |
|---|---|
| **Route** | `/faq-generator` |
| **Page title** | FAQ Creator |
| **Subtitle** | None in the header; a tagline sits in the page body |
| **Breadcrumb** | DareAISearch › {Brand} › FAQ Creator |
| **Sidebar location** | INTELLIGENCE group → FAQ Creator (4th item) |
| **Shared shell** | Documented in [../doc analytics/00-global-layout.md](../doc%20analytics/00-global-layout.md) |

> Documented from the live app. The page and its create form were captured on three brands. None had saved FAQ sets, and **Create FAQs was not submitted**, so the generated output and the saved-set list are **not captured**. Text in quotes is exact on-screen text.

---

## 1. Purpose

Generates a set of FAQs for a page of the brand, shaped by the AI-search prompts the brand is tracking. The user chooses the page, up to three prompts, the answer style and the answer length. Each generated set is stored and can be seen again on this page.

---

## 2. Page sections (top to bottom)

| # | Section | Contents |
|---|---|---|
| 1 | Page title | "FAQ Creator" |
| 2 | Intro block | Circle icon with a question mark (teal), tagline |
| 3 | Create card | Prompt text and the **Create FAQs** button |

---

## 3. Section details

### 3.1 Intro block
Centred. A round dark-teal badge with a teal **?** icon, and under it the tagline **"Create comprehensive FAQs based on AI search patterns"**.

### 3.2 Create card
A bordered rounded card, centred, narrower than the page.

| Element | Details |
|---|---|
| Text | **"Click below to configure and create FAQs for your brand."** |
| **Create FAQs** | Teal filled button. Opens the **FAQ Creator Form** dialog |

### 3.3 FAQ Creator Form (dialog)
Title **FAQ Creator Form**, text "Fill in the details below to create your FAQs". Closes with the X at the top right.

| Field | Type | Details |
|---|---|---|
| Brand Name | Read-only box (greyed) | Filled with the selected brand |
| Website URL | Read-only box (greyed) | Filled with the brand's website |
| Target Page URL | Text box | Placeholder **"Which Target Page URL do you want me to analyze for FAQs?"**. Has focus when the dialog opens |
| Target Prompts | Search-and-pick box with a counter chip **0/3** | Placeholder "Search prompts from Prompt Ranking, or type your own". Help line: **"Pick up to 3 from your Prompt Ranking, or type a custom prompt and press Enter."** |
| Answer Policy | Dropdown | **Factual only** (default) · **Persuasive allowed** · **Include CTA** |
| Word Length | Dropdown | **Short (≤50 words)** (default) · **Medium (60–120 words)** · **Long (>150 words)** |
| **Create FAQs** | Wide teal button | Submits the form |

### 3.4 Saved FAQ sets
The page loads the user's earlier FAQ results (count and list, newest first). No brand tested had any, so how saved sets are displayed is **not captured**.

---

## 4. UI element inventory

### Buttons, dropdowns and toggles
| Control | Where | Action |
|---|---|---|
| Create FAQs | Page card | Open the form |
| Target Page URL | Form | Page to analyse |
| Target Prompts | Form | Choose up to 3 prompts or type your own |
| Answer Policy | Form | Choose answer style |
| Word Length | Form | Choose answer length |
| Create FAQs | Form | Submit |
| X | Form | Close |

### Not present on this page
Filters, tabs, search box on the page itself, AI insight line, Recommended Actions, ⓘ tooltips, export.

### Status and empty states
| State | Text |
|---|---|
| No saved FAQs | Intro and create card only, no error message |

---

## 5. Data sources and API calls

| Data block | Call | Input |
|---|---|---|
| Count of saved sets | `HEAD faq_results` | filtered by `user_id` |
| Saved sets | `GET faq_results` | `user_id`, ordered by `created_at` |
| Prompt suggestions in the form | Not captured | Taken from the brand's Prompt Ranking |
| Generation | Not captured | Starts when the form is submitted |

---

## 6. Behaviour rules

- **Brand scoped form, user scoped storage:** the form uses the selected brand, but saved results are stored per **user** (`user_id`).
- **Up to 3 prompts:** the counter shows `{n}/3`; custom prompts are added with Enter.
- **Locked fields:** brand name and website cannot be edited; they come from the brand's settings.
- **Newest first:** saved sets are ordered by creation time.
- **Same view for Pro User and Sub-Admin:** no difference was seen.
