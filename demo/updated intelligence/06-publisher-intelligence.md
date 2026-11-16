# Intelligence → Publisher Intelligence

| | |
|---|---|
| **Route** | `/intelligence` |
| **Page title** | Publisher Intelligence |
| **Subtitle** | "Discover, evaluate, and order placements on premium publisher websites — powered by AI." |
| **Breadcrumb** | DareAISearch › {Brand} › Publisher Intelligence |
| **Sidebar location** | INTELLIGENCE group → Publisher Intelligence (6th item). **Shown only for some accounts and roles** (see global layout, section 6); it was present for the Sub-Admin account and for one Pro User account |
| **Shared shell** | Documented in [../updated analytics/00-global-layout.md](../updated%20analytics/00-global-layout.md) |

> Documented from the live app. All three tabs were opened on three brands. The marketplace was **empty for every brand** ("No publishers match your filters"), so a publisher card and the order flow are **not captured**. Text in quotes is exact on-screen text.

---

## 1. Purpose

A marketplace to find publisher websites, judge them by authority and traffic, and **order paid placements** on them. The AI Recommendations switch narrows the list to publishers suggested for the brand. Placed orders are tracked on the other two tabs.

---

## 2. Page sections (top to bottom)

| # | Section | Contents |
|---|---|---|
| 1 | Page header | Title and subtitle |
| 2 | Tab switch | **Marketplace** (default) · **My Orders** · **Analytics** |
| 3 | Tab content | Depends on the tab (below) |

---

## 3. Tab: Marketplace

A **Filters** panel on the left and the publisher results area on the right.

### 3.1 Filters panel
Heading **Filters** with a **Reset** link at the right that clears every filter.

| Filter | Type | Options |
|---|---|---|
| Search | Text box, placeholder "Domain…" | Search publishers by domain |
| AI Recommendations | Switch with sparkle icon, off by default | Show only AI-recommended publishers |
| Niche | Check-box list (multi-select) | SaaS · Tech · Finance · Health · Legal · Crypto · eCommerce · News · Lifestyle · Entertainment · Education · Travel · Business · Marketing · Sports · Politics · Automotive · Food (18) |
| DA range | Two-handle slider, **0–100** | Domain Authority of the publisher |
| Monthly traffic | Radio buttons | **Any** (default) · **< 10k** · **10k – 100k** · **100k – 500k** · **500k+** |
| Country | Dropdown | **Any** (default) · United States · United Kingdom · Canada · Germany · Australia · Singapore · India |
| Language | Dropdown | **Any** (default) · English · German · French · Spanish |
| Max budget ($) | Number box, placeholder "No limit" | Highest price to pay |

### 3.2 Results area
Empty state seen for all brands tested: globe icon, bold **"No publishers match your filters"**, and the hint **"Try widening the DA range or clearing niches."** When publishers exist they are listed here; the card layout (columns, price, order button) was **not captured**. Switching the AI Recommendations switch on did not change the empty state.

---

## 4. Tabs: My Orders and Analytics

Both tabs showed the **same content** for the brands tested, because no order had been placed.

| Element | Details |
|---|---|
| Counters | Four tiles in a row: **Total Orders** · **Pending** · **Published** · **Rejected**, each with a number (all 0 in the sample) |
| Empty state | **"No orders yet"** and **"Browse the marketplace to place your first order."** |

What the tabs show once orders exist (order rows, and charts or totals on Analytics) was **not captured**. The counters imply an order moves from Pending to Published or Rejected.

---

## 5. UI element inventory

### Buttons, dropdowns and toggles
| Control | Where | Action |
|---|---|---|
| Marketplace / My Orders / Analytics | Tab switch | Switch view |
| Reset | Filters heading | Clear all filters |
| Domain… | Filters | Text search |
| AI Recommendations | Filters | On/off switch |
| Niche check boxes | Filters | Pick one or more niches |
| DA range | Filters | Slider |
| Traffic radio buttons | Filters | Pick a traffic band |
| Country, Language | Filters | Dropdowns (default Any) |
| Max budget ($) | Filters | Number input |

### Not present on this page
Date filters, AI insight line, Recommended Actions, ⓘ tooltips.

### Status and empty states
| State | Text |
|---|---|
| No publisher matches | "No publishers match your filters" / "Try widening the DA range or clearing niches." |
| No orders | "No orders yet" / "Browse the marketplace to place your first order." |

---

## 6. Data sources and API calls

| Data block | Call | Input |
|---|---|---|
| Publisher list | `GET publisher_websites_public` | ordered |
| Orders and analytics | Not captured | |

The table name `publisher_websites_public` suggests the list comes from a public view of publisher data; it returned no rows for the brands tested.

---

## 7. Behaviour rules

- **Role gated:** the sidebar item appears only for some accounts, so a user without it has no link to this page.
- **Filters combine:** niche, DA, traffic, country, language and budget all narrow the same list; **Reset** returns to the full list (inferred from the filter layout).
- **Empty is not an error:** zero matches shows the hint above.
- **Brand scoped orders:** order counters are for the selected brand (inferred; all were 0).
