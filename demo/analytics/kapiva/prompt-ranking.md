# Kapiva → Prompt Ranking (differences only)

Compared with [../UI/04-prompt-ranking.md](../UI/04-prompt-ranking.md). Only what is **different or new** for Kapiva is listed. Anything not mentioned works the same as in the existing doc.

| | |
|---|---|
| **Route** | `/analytics/prompt-ranking` (same) |
| **Checked on** | 20 Nov 2026, with a **Sub-Admin** account. Some differences may come from the role, not only from the brand |
| **Models enabled** | ChatGPT, Gemini, Perplexity, AI Overview (four) |

---

## 1. Summary of differences

| Area | Existing doc | Kapiva |
|---|---|---|
| Date control | None on the page | **Period button** at top right (`November 2026`) |
| Visibility cards | Two cards, no toggle | **Four cards** with a **Latest / Average** toggle |
| Insight line and actions | Insight line plus RECOMMENDED ACTIONS cards | Insight line only; **no Recommended Actions** seen |
| AI Rankings filters | Model tabs only | Model tabs plus **Funnel, SKU / Unit, Theme, Sub-tag** filters |
| AI Rankings export | None | **Download Excel** button |
| Prompt rows | Plain text | Each prompt has a **"N brands ranked" / "No brands ranked"** tag |
| Status tags | None | **Response available (n)** and **No response this week (n)** |
| Weekly columns | One column per week (26 in the sample) | **Only the weeks inside the chosen period** (one column, `18-Nov-2026`) |
| Pagination | None | **50 prompts per page** |
| Extra section | None | **Ranking Gaps – Prompt Wise** table |

---

## 2. Period button (new)

A button at the top right of the page header, showing the selected period (default **November 2026**). Opens a popover:

| Element | Details |
|---|---|
| **Month** / **Custom range** | Two modes at the top |
| Year and month grid | `2026`, then **Jan … Dec** |
| **Compare with previous period** | Checkbox |
| **Reset** / **Apply** | Buttons at the bottom |

The period drives the visibility cards and the weekly columns in the rank grid.

## 3. Current AI Visibility & Readiness

| Item | Kapiva |
|---|---|
| Sub-line | "Latest weekly run in {Month} · as of {D Mon YYYY}" |
| **Latest / Average toggle** | Pill toggle at the right of the section title. **Latest** is the default |
| Cards | **Four**, full width in one row: **ChatGPT, Gemini, Perplexity, AI Overview Visibility %** |
| Card sub-text | Latest: "as of {D Mon YYYY}". Average: "{n} weekly run(s)" |
| Average mode | Sub-line changes to "Average of {n} weekly run in {Month}". Tooltip: "Share of tracked prompts where your brand appeared in {Model} responses, pooled across the weekly runs in the period." |

In the existing doc the cards do not change with any control. Here the **Latest / Average toggle and the period** both change them. The model tabs in AI Rankings still do not.

## 4. Insight line

- Shown under the visibility cards with a **BETA** pill, but it appears **after a delay** (it was missing on first paint and showed up later).
- Sample wording: "Kapiva ranks in {a} of {b} tracked prompts ({n}% coverage) but ChatGPT visibility is currently at 0%." The sentence says **0% ChatGPT visibility** while the ChatGPT card showed **34.40%**. The two do not agree.
- **No RECOMMENDED ACTIONS cards** were seen.

## 5. AI Rankings

| Item | Kapiva |
|---|---|
| Header | **Download Excel** button at the top right (not exercised) |
| Model tabs | ChatGPT, Gemini, Perplexity, AI Overview (four) |
| **Filters** (new) | **Funnel**, **SKU / Unit**, **Theme**, **Sub-tag**, each a dropdown with a **count next to every option** |
| Prompt count | "{n} prompts" at the right of the filters (250) |
| **Status tags** (new) | **Response available ({n})** and **No response this week ({n})**. Not clickable |
| Legend line (new) | "Tags show the latest weekly results in the selected period for the selected model. N brands ranked = ranked brands found; No brands ranked = none found." |

**Filter options seen**

| Filter | Options |
|---|---|
| Funnel | BOFU, MOFU, POST, REP, TOFU |
| SKU / Unit | Ayurveda, Dia Free, Diabetes, Kapiva, Liver, Liver Care, Reputation-Ayurveda, Reputation-Diabetes, Reputation-Liver, Reputation-Shilajit, Shilajit |
| Theme | 23 options (for example Best Product Choice, Kapiva Reputation, Trust & Verification) |
| Sub-tag | About 140 options (for example best-brand, heavy-metals, vs-competitor) |

**Rank grid**

| Item | Existing doc | Kapiva |
|---|---|---|
| Prompt cell | Prompt text only | Prompt text **plus a small tag**: "No brands ranked" (grey) or "{n} brand(s) ranked" (teal) |
| Date columns | All weekly scans (26) | Only the weekly runs in the selected period (one: `18-Nov-2026`) |
| Header menu | Sort Ascending (1→10) / Sort Descending (10→1) | Same menu |
| Body | 500 px scroll box, no pagination | **Paginated, 50 per page**: footer "Showing 1–50 of 250 prompts" with **Previous, 1 2 3 4 5, Next** |
| Row click | Not clickable | Not clickable (same) |

Rank cells are a number or **-**, same as the existing doc. A prompt can show **"5 brands ranked"** while the Kapiva cell is **-**, meaning other brands ranked but Kapiva did not.

## 6. Ranking Gaps – Prompt Wise (new section)

Below the rank grid. Title only (no ⓘ).

| Element | Details |
|---|---|
| **From / To** | Two date inputs, default last 7 days (`13-11-2026` to `19-11-2026`) |
| **All models** | Dropdown: All models, ChatGPT, Gemini, Perplexity, AI Overview |
| **All topics** | Dropdown with about 70 topics |
| Download icon | Exports the table (not exercised) |
| Refresh icon | Reloads the data (not exercised) |
| Count | "{n} prompts" at the right (536) |

| Column | Description |
|---|---|
| **#** | Row number |
| **Prompt** | Prompt text |
| **Model** | Model with its icon |
| **Days w/o Mention** | Number of days the brand has gone without being mentioned for that prompt and model |
| **Topic** | Topic name |
| **Topic Volume** | Search volume number, or **Coming Soon** with an hourglass (seen for Perplexity rows) |
| **Ranking Brands** | Brands ranked for the prompt, or **—** |
| **Number of Brands** | Count of ranked brands |

Rows are ordered by **Days w/o Mention**, highest first. The table has its own scroll area. Footer: "1–50 of {n}" with **‹ 1 / 11 ›** page buttons.

## 7. Data sources and calls (different or new)

| Data block | Call |
|---|---|
| Weekly runs | `POST fetch-prompt-run-history` `{ "brandOverride": "Kapiva" }` |
| Prompt filters (funnel, SKU, theme, sub-tag) | `GET prompts_brandwise` (select `prompts, funnel, sku_unit, theme, sub_tag`) |
| Rank data per run | `GET semrush_prompt_product_rankings` (select `prompt, model, date_start, date_end, ranked_brand`) |
| Ranking Gaps | `POST fetch-kapiva-ranking-gaps` `{ "start": "2026-11-13", "end": "2026-11-19", "refresh": false }` |

The visibility, model config, rank grid and insight calls are the same as in the existing doc.

## 8. Not checked

Download Excel and refresh buttons, the Compare with previous period option, Custom range, and the Gemini, Perplexity and AI Overview rank grids in detail.
