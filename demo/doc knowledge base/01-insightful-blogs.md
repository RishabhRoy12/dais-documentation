# Knowledge Base → Insightful Blogs

| | |
|---|---|
| **Route** | `/insightful-blogs` |
| **Page title** | Insightful Blogs |
| **Subtitle** | None |
| **Breadcrumb** | DareAISearch › {Brand} › Insightful Blogs |
| **Sidebar location** | KNOWLEDGE BASE group → Insightful Blogs (1st of 2 items) |
| **Shared shell** | Top bar, sidebar, breadcrumb and the Miss Daring assistant are documented in [../doc analytics/00-global-layout.md](../doc%20analytics/00-global-layout.md) |

> Documented from the live app, **Sub-Admin** view, on three brands. Titles, dates and counts are placeholders such as `{Blog title}` and `{n}`. Text in quotes is exact on-screen text. The articles themselves live on the DareAISearch website; only the cards were documented, not the articles.

---

## 1. Purpose

A read-only library of DareAISearch's own articles on AI search and GEO (generative engine optimisation), shown as cards so a brand's team can keep up with changes in AI search. Each card links out to the full article on the DareAISearch website.

---

## 2. Page sections (top to bottom)

| # | Section | Contents |
|---|---|---|
| 1 | Page title | "Insightful Blogs" (no subtitle) |
| 2 | Toolbar | **Refresh** button at the right |
| 3 | Article grid | One card per article, three per row |

There is no data-freshness banner, filter, search box, AI insight line, Recommended Actions or ⓘ tooltip.

---

## 3. Section details

### 3.1 Refresh
Outlined button with a refresh icon, top right. Reloads the article list from the server; the list in the test was unchanged after pressing it.

### 3.2 Article card
Cards are ordered **newest first** and wrap three to a row.

| Part | Details |
|---|---|
| Thumbnail | Wide image at the top of the card. Some articles have their own artwork; others use the same generic DareAISearch banner ("DareAISearch — AI Search Optimization & GEO") |
| Title | Bold, up to three lines |
| Meta line | Calendar icon · **{Month D, YYYY}** · a dot · author name (**DareAISearch** on every card seen) |
| Description | One short paragraph (two to three lines) summarising the article |
| **Read More ↗** | Teal text link with an external-link icon. Opens the full article on the DareAISearch website in a **new browser tab** (`dareaisearch.com/blogs/{article-slug}`) |

The title and the thumbnail are **not** links; only **Read More** opens the article.

### 3.3 Date problem on one card
The last card in the sampled list shows **"Invalid Date"** in place of its date. It is an article that has no usable publish date; such an article is listed at the **end** of the grid.

---

## 4. UI element inventory

### Buttons, dropdowns and toggles
| Control | Where | Action |
|---|---|---|
| Refresh | Toolbar | Reload the article list |
| Read More ↗ | Each card | Open the article in a new tab |

### Not present on this page
Search box, category or date filters, sort control, pagination or "load more" (all cards load at once), bookmark or share buttons, AI insight line, Recommended Actions, ⓘ tooltips.

### Badges and labels
| Label | Where | Meaning |
|---|---|---|
| {Month D, YYYY} | Card meta line | Publish date |
| DareAISearch | Card meta line | Author |
| Invalid Date | One card | Article without a valid date |

### Status and empty states
No empty-state text was captured: all three brands showed articles.

---

## 5. Data sources and API calls

| Data block | Call | Input |
|---|---|---|
| Article list | `GET knowledge_articles` | selected columns including `status` and `source_type`, ordered, limited |

Pressing **Refresh** repeats the same single call. Shell calls (roles, subscription, notifications) are listed in the global layout document, section 5.

---

## 6. Behaviour rules

- **Not brand scoped:** the same list (58 cards in the sample) appeared for all three brands tested, so the page shows DareAISearch's articles, not content about the selected brand.
- **Newest first:** ordered by publish date, newest at the top.
- **Published articles only:** the call filters on article `status`, so drafts are presumably not shown (the filter value was not captured).
- **Read-only:** the page cannot add, edit or delete articles; it only lists them and links out.
- **External links:** every **Read More** opens in a new tab with `noopener noreferrer`, so the platform stays open.
