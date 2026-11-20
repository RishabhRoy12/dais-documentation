# Kapiva → Sentiment Overview (differences only)

Compared with [../UI/07-sentiment-overview.md](../UI/07-sentiment-overview.md). Only what is **different or new** for Kapiva is listed. Anything not mentioned works the same as in the existing doc.

| | |
|---|---|
| **Route** | `/analytics/concepts` (same) |
| **Checked on** | 20 Nov 2026, with a **Sub-Admin** account. Some differences may come from the role, not only from the brand |
| **Models enabled** | ChatGPT, Gemini, Perplexity, AI Overview (four) |

---

## 1. Summary of differences

| Area | Existing doc | Kapiva |
|---|---|---|
| Top of page | Static model pill | **Four summary cards** and **four working model tabs** |
| Date control | **Month dropdown** | **From / To date inputs**, refresh and download icons |
| Concepts Aggregated | Sentiment bars, negative bars mostly empty | Negative bars are **visible**; legend reads Positive / Neutral / Negative |
| **Brand Sentiment Leaderboard** | Not present | **New** stacked bar chart, one bar per brand |
| Concepts by Brand | One number per brand, model dropdown | **Pos / Neu / Neg** sub-columns per brand, **Download Excel**, no model dropdown |
| Data call | `fetch-concept-data`, `fetch-concept-by-brand` | One call: `fetch-kapiva-concept-sentiment` |

---

## 2. Summary cards (new)

Four cards in a row under the title. The numbers are **averages per day** for the selected model and period.

| Card | Details | ⓘ tooltip |
|---|---|---|
| **Positive Sentiment** | Thumbs-up icon, number (sample `58.9`) | "Average positive Kapiva mentions per day for {Model} in the selected period." |
| **Negative Sentiment** | Thumbs-down icon, number (`22.0`) | Same pattern for negative |
| **Neutral Sentiment** | Dash icon, number (`85.4`) | Same pattern for neutral |
| **Mentions by sentiment** | Donut chart with the total in the centre (`166.3`) and a legend: Neutral (grey), Positive (teal), Negative (red) | "Average Kapiva mentions per day for {Model}, split by sentiment." |

While loading, the cards show dots and the donut card shows "Loading…".

## 3. Model tabs (changed)

| Item | Existing doc | Kapiva |
|---|---|---|
| Control | One static pill, clicking does nothing | **Four tabs**: ChatGPT (default), Gemini, Perplexity, AI Overview |
| Effect | None | Switches **the whole page**: the four cards, Concepts Aggregated, the leaderboard and Concepts by Brand. No new call is made |

Row counts change with the model (for example 209 rows for ChatGPT, 246 for Gemini, 226 for Perplexity, 287 for AI Overview).

## 4. Concepts Aggregated – {Model}

| Item | Existing doc | Kapiva |
|---|---|---|
| Month dropdown | Present | **Removed** |
| Date range | None | **From / To** date inputs (default last 7 days, `13-11-2026` to `19-11-2026`) |
| Refresh icon | None | Next to the dates (not exercised) |
| Download icon | None | Next to the refresh icon (not exercised) |
| Key labels | "Sentiments Positive / Neutral / Negative" | **Positive / Neutral / Negative** |
| Mentions header | "Mentions ({Month YYYY})" | "Mentions ({D Mon YYYY})" (the end date of the range) |
| Sentiment values | Plain numbers | Positive and negative counts are **coloured** (teal and red) and **underlined** |
| Negative bars | Empty in every row checked | **Drawn in red** where the value is above 0, and an empty track at 0 |
| Footer | "1 - {n} / {n}" | Same (`1 - 209 / 209`) |

The concept names still use the `__` hierarchy, and the row order and scroll behaviour are the same.

## 5. Brand Sentiment Leaderboard (new)

| Element | Details |
|---|---|
| Title | **Brand Sentiment Leaderboard**, with an ⓘ icon and the range label "(13 Nov 2026 – 19 Nov 2026)" |
| Chart | Horizontal **stacked bar**, one bar per brand (Kapiva, Dabur, Himalaya Wellness, Baidyanath, Upakarma Ayurveda). Each bar is split into negative (red), neutral (grey) and positive (teal) |
| Axis | Mention count from 0 to a rounded maximum (0, 291, 582, 873, 1164 in the sample) |
| Legend | "Sentiment" then negative, neutral, positive |
| Order | Kapiva first in the ChatGPT view; the other brands' order varies with the model |

The Concepts by Brand tooltip says this chart is the sum of that table per brand.

## 6. Concepts by Brand

| Item | Existing doc | Kapiva |
|---|---|---|
| Date label | "({YYYY-MM-DD})" snapshot date | Range "(13 Nov 2026 – 19 Nov 2026)" |
| Header control | Model dropdown | **Download Excel** button (not exercised). The model dropdown is gone, since the tabs now switch the model |
| ⓘ tooltip | "…Source: SEMrush." | "Positive, neutral and negative mentions of each concept for every brand in {Model} answers during the selected period. The leaderboard above adds these up per brand." |
| Columns | One column per competitor, own brand last in lower case | **Brand groups with three sub-columns each: Pos, Neu, Neg.** Kapiva is the **first** group, written **Kapiva**, then Dabur, Himalaya Wellness, Baidyanath, Upakarma Ayurveda |
| Cell colours | Dimmed grey for 0 | Pos teal, Neu white, Neg red, and 0 dimmed grey |
| No data | `0` | **—** when the brand has no data for the concept |
| Concept names | Top-level concepts, alphabetical | Specific topics (for example price, ingredients, herbal ingredients, heavy metal testing). **Not alphabetical** |
| First column | Pinned | Pinned |

## 7. Data sources and calls (different)

| Data block | Existing doc | Kapiva |
|---|---|---|
| All sections | `fetch-concept-data` (month) and `fetch-concept-by-brand` | **`POST fetch-kapiva-concept-sentiment`** `{ "start": "2026-11-13", "end": "2026-11-19", "refresh": false }` |

One call fills the cards, both tables and the leaderboard, and the model tabs work on the loaded data. The usage-tracking call is the same, and its page label is **Concepts**.

## 8. Not checked

Changing the date range, the refresh and download buttons, and hover tooltips on the leaderboard bars and the donut.
