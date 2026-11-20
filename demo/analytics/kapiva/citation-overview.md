# Kapiva → Citation Overview (differences only)

Compared with [../UI/06-citation-overview.md](../UI/06-citation-overview.md). Only what is **different or new** for Kapiva is listed. Anything not mentioned works the same as in the existing doc.

| | |
|---|---|
| **Route** | `/analytics/citations` (same) |
| **Checked on** | 20 Nov 2026, with a **Sub-Admin** account. Some differences may come from the role, not only from the brand |
| **Models enabled** | ChatGPT, Gemini, Perplexity, AI Overview (four) |

---

## 1. Summary of differences

| Area | Existing doc | Kapiva |
|---|---|---|
| Insight line wording | "citation rate … explicit absence rate" | "citations in only {a} of {b} tracked prompts … citation rate and … **lost rate** with {n} **WoW delta**" |
| Brand's Citations chart | Same | Same (domains shown include `kapiva.in`) |
| **Source Analysis** | Not present | **New section** with an 809-row source domain table |
| Brand Domain Citations | Model tabs and key only | Adds **Funnel, SKU / Unit, Theme, Sub-tag** filters and a **download icon** |
| Scan dates in grid | 29–30 date columns | **Four** date columns |
| **Citation Gap – Prompt Wise** | Not present | **New section** at the bottom |

---

## 2. Insight line

Sample wording: "Kapiva holds citations in only {a} of {b} tracked prompts on ChatGPT, resulting in a {n}% citation rate and a {n}% lost rate with {n} WoW delta."

Same position and **BETA** pill. It names **ChatGPT** and uses the terms **lost rate** and **WoW delta**.

## 3. RECOMMENDED ACTIONS

Same card layout and categories as the existing doc. Seen: **VISIBILITY (HIGH)**, **RISK (HIGH)** and **GROWTH (MEDIUM)**. The cards are specific to Kapiva: they quote prompts such as "Kapiva ke products ache hain kya?" and "What are good alternatives to Kapiva?" and mention shilajit and liver care.

## 4. Source Analysis (new section)

Sits between the chart card and Brand Domain Citations.

| Element | Details |
|---|---|
| Title / count | **Source Analysis**, with "{n} source domains" at the right (809) |
| **From / To** | Date inputs, default last 7 days (`13-11-2026` to `19-11-2026`) |
| **All models** | Dropdown: All models, ChatGPT, Gemini, Perplexity, AI Overview |
| **Download Excel** | Button (not exercised) |
| Refresh icon | Reloads the data (not exercised) |

| Column | Description |
|---|---|
| **Source Domain** | Domain with a **›** chevron (for example `amazon.in`, `kapiva.in`, `1mg.com`) |
| **Source Type** | "{Group} · {Sub-type}", for example **Other · Marketplaces**, **Owned · E-commerce / Retail**, **Knowledge bases · Official/Institutional**, **Social · Community/Forums**, **Benchmark Competitors · E-commerce / Retail** |
| **Total Citations** | Number |
| **Prompts** | Number of prompts where the domain was cited |
| **AI Models** | Chips for the models that cited the domain |
| **Citation Share** | Percentage with a small bar |
| **URLs** | Number of distinct URLs cited |

- Rows are ordered by **Total Citations**, highest first.
- **Pagination:** 50 per page. Footer "1–50 of 809" with **‹ 1 / 17 ›**.
- **Expanding a row** (click the **›** chevron): a sub-table appears with a **Download {domain} prompts** button and the columns **Prompt, AI Model, Citation Date, URLs, Brand Mentioned, Associated Brands**. "Brand Mentioned" shows **Mentioned**; "Associated Brands" lists brand names.

## 5. Brand Domain Citations

| Item | Existing doc | Kapiva |
|---|---|---|
| Filters (new) | None | **Funnel, SKU / Unit, Theme, Sub-tag** dropdowns, same options and counts as on Prompt Ranking |
| Download icon (new) | None | Icon button at the right of the filters (not exercised) |
| Date columns | One per scan date (29–30) | **Four**: `14th November 2026`, `7th November 2026`, `4th November 2026`, `31st October 2026` |
| Empty cells | Always ✓ or ✗ | A date with no scan for that prompt is **blank** (neither ✓ nor ✗) |
| Chevron and expansion | Same | Same. Rows that were cited show **›**; expanding shows the date and URLs (for example `https://kapiva.in/about-us`) |

Rows seen: prompts such as "Which is the most trusted Ayurvedic brand in India?" (✗ ✗) and "Kapiva vs Patanjali — which ayurvedic brand is better quality?" (✓ on all dates).

## 6. Citation Gap – Prompt Wise (new section)

Last section on the page.

| Element | Details |
|---|---|
| Count | "{n} prompt-model records" at the right (0 in the sample) |
| **From / To** | Date inputs, default last 7 days |
| **All models** / **All topics** | Dropdowns |
| **Download Excel** | Button (not exercised) |
| Refresh icon | Reloads the data (not exercised) |

| Column | Description |
|---|---|
| (select circle) | Selection control in the header |
| **Prompt** | Prompt text |
| **Model** | Model |
| **Days w/o Citation** | Days since the brand was last cited |
| **Topic** / **Topic Volume** | Topic and its volume |
| **Citation Brands** | Brands that were cited |
| **Number of Brands** | Count |

**Empty state:** "No citation-gap source records available for this selection." with footer "0 records" and **‹ 1 / 1 ›**.

## 7. Data sources and calls (different or new)

| Data block | Call |
|---|---|
| Source Analysis table | `POST fetch-kapiva-source-analysis` `{ "start": "2026-11-13", "end": "2026-11-19", "refresh": false }` |
| Citation Gap table | `POST fetch-kapiva-citation-gaps` `{ "start": "2026-11-13", "end": "2026-11-19", "refresh": false }` |
| Filter lists for Brand Domain Citations | `GET prompts_brandwise` (select `prompts, funnel, sku_unit, theme, sub_tag`) |
| Chart series | `GET citation_graph_data` filtered on `brand_name ilike kapiva.in` (the brand's domain, not the brand name) |

The insight, brand grid and source-list calls (`generate-page-insights`, `fetch-citation-data`, `fetch-sources-data`) are the same as in the existing doc.

## 8. Not checked

Download and refresh buttons, the Citation Gap table with data (it was empty), and the Source Analysis model filter.
