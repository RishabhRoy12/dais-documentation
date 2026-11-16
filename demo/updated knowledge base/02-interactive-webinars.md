# Knowledge Base → Interactive Webinars

| | |
|---|---|
| **Route** | `/interactive-webinars` |
| **Page title** | Interactive Webinars |
| **Subtitle** | None |
| **Breadcrumb** | DareAISearch › {Brand} › Interactive Webinars |
| **Sidebar location** | KNOWLEDGE BASE group → Interactive Webinars (2nd of 2 items) |
| **Shared shell** | Top bar, sidebar, breadcrumb and the Miss Daring assistant are documented in [../updated analytics/00-global-layout.md](../updated%20analytics/00-global-layout.md) |

> Documented from the live app, **Sub-Admin** view. Titles, dates, names and counts are placeholders such as `{Webinar title}` and `{n}`. Text in quotes is exact on-screen text. The webinar recordings and the registration pages are on a separate webinar site and were **not** documented.

---

## 1. Purpose

A library of DareAISearch's past webinars on AI search. Each card shows when the session ran, who presented, what it covered, and a **Watch Now** button that leads to the webinar site.

---

## 2. Page sections (top to bottom)

| # | Section | Contents |
|---|---|---|
| 1 | Page title | "Interactive Webinars" (no subtitle) |
| 2 | Webinar grid | One card per webinar, three per row |

There is no toolbar, filter, search box, Refresh button, data-freshness banner, AI insight line, Recommended Actions or ⓘ tooltip.

---

## 3. Section details

### 3.1 Webinar card
Cards are ordered **newest first** and wrap three to a row; the cards in one row stretch to the same height, with the button at the bottom.

| Part | Details |
|---|---|
| Number badge | Round teal badge at the top left with the webinar's number. The **oldest webinar is 1** and the newest has the highest number (6 in the sample), so the numbers run backwards down the page |
| Date | Calendar icon and the date, mostly as **"{D(th) Month YYYY}"** (for example "18th February 2026"). The oldest card uses another style, **"{Month D, YYYY}"** |
| Duration | Clock icon and **"30 minutes"**; the oldest card reads **"45 mins"** |
| Title | Large bold title, up to four lines |
| Speakers | Two people, each with a round initials badge, the name in teal and the job title under it, in the form "{Role}, {Company}". The same two speakers appeared on every card in the sample |
| **What was covered:** | Bold label followed by a bulleted list of 3 to 5 points. Teal dots as bullets; key phrases inside a point are highlighted in teal |
| **Watch Now** | Full-width outlined button with a play icon at the bottom of the card |

### 3.2 Watch Now behaviour
| Card | What happens |
|---|---|
| Five older cards | The button is a link that opens the webinar site's registration page, `webinar.dareaisearch.com/meeting/register?sessionId={id}`, in a **new browser tab** |
| Newest card | **Defect seen in the test:** the button is a plain button that moves the **same tab** to `/interactive-webinars/https:/webinar.dareaisearch.com/meeting/register?sessionId={id}`, an address that does not exist in the app. The page then shows **"404 · Oops! Page not found"** with a **Return to Home** link |

So the newest webinar can't be opened from this page at the time of testing; the other five can.

---

## 4. UI element inventory

### Buttons, dropdowns and toggles
| Control | Where | Action |
|---|---|---|
| Watch Now | Each card | Open the webinar (see 3.2) |

### Not present on this page
Search box, filters, sort control, Refresh, pagination or "load more", speaker links (names are plain text), share or download buttons, AI insight line, Recommended Actions, ⓘ tooltips.

### Badges and labels
| Label | Where | Meaning |
|---|---|---|
| {n} (teal circle) | Top left of card | Webinar number, oldest = 1 |
| What was covered: | Card body | Heading of the topic list |

### Status and empty states
No empty-state text was captured: the sample had six webinars.

---

## 5. Data sources and API calls

| Data block | Call | Input |
|---|---|---|
| Webinar cards | None | The page made **no data call** beyond the shell calls; the six webinars appear to be written into the page itself |

Shell calls (roles, subscription, notifications) are listed in the global layout document, section 5.

---

## 6. Behaviour rules

- **Fixed list:** because there is no data call, adding a webinar needs a change to the app, not an entry in a table (inferred from the absence of a call).
- **Not checked per brand:** the list was read on one brand; whether other brands see the same cards was not tested.
- **Read-only:** the page has no interaction other than **Watch Now** and scrolling.
- **Mixed formats:** dates and durations are not written the same way on every card (see 3.1), which suggests the text is typed by hand per card.
