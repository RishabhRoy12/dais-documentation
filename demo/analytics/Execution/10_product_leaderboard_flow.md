# Product Leaderboard Flow

**Notation:** A **product** = an item sold by the brand. A **scan date** = the week the ranks belong to. The **property ID** = the ID that links the brand to its data in Semrush. The page is titled "ChatGPT Shopping Leaderboard" on screen ("Product Leaderboard" in the sidebar and breadcrumb). This is the one analytics page that is genuinely ChatGPT-specific: it ranks products in ChatGPT Shopping, not in the other AI models enabled for the brand (e.g. Gemini, Perplexity).

**Goal:** the page shows where the brand and each of its products rank in ChatGPT Shopping, week by week. The page data comes directly from **Semrush**, using the **property ID** through the **Semrush API**. Nobody types in or uploads the data, and it keeps updating automatically.

**Only when the project has products:** if the project has products, the Product Leaderboard data is taken from **Semrush** and kept updated. If the project has no products, the leaderboard data is removed and the page shows the empty state.

## Purpose and Access

The page (`/analytics/product-leaderboard`) shows:

1. A summary card: TOTAL PRODUCTS, RANKED (LATEST), TOP 3, TOP 5, AVG RANK.
2. A rank grid ("Product Name" column + one column per scan date, newest first, all dates shown): the brand row first, then every product ever ranked, with a rank (1 to 10, or `-` for not ranked). Ranks 1 to 3 show a gold, silver or bronze medal in a highlighted chip, 4 and 5 a dark chip, 6 to 10 a small grey number.

If the brand has no leaderboard data, the page shows a trophy icon, the heading "No Leaderboard Data Yet" and the message "Product leaderboard data will appear here once ranking data is available." (the empty state replaces the summary card and grid). The client can only view the page. There are no buttons, filters, date picker, search, sorting, pagination, export, tooltips, charts, AI insight line or Recommended Actions.

The page is available only for brands that have it enabled (sidebar: ANALYTICS group → Product Leaderboard).

## In short

1. The brand is linked to its Semrush property ID (once).
2. The data comes from Semrush through the Semrush API.
3. The page takes its data directly from Semrush, and shows it only if the project has products.
4. The page updates automatically as new scan dates arrive (weekly, with occasional extra dates).

## System rules

- The page data comes directly from **Semrush**, matched by the brand's **property ID**, through the **Semrush API**.
- The leaderboard shows data **only when the project has products**.
- The same source is used for the Citation Overview, the Sentiment Overview and the Reddit Overview.
- The data updates **automatically**. There is no manual add or upload.
- The client cannot add or change any data.
- The data is **brand scoped**: it is for the brand selected in the top bar.
- The data is for ChatGPT Shopping only; this page does not follow the brand's AI model configuration.
- The first grid row is the **brand**. Then products ranked in the latest scan (best first), then products ranked only earlier, then products that never ranked recently (all dashes).
- TOTAL PRODUCTS is the number of grid rows (the brand row plus every product ever ranked). The other four numbers are for the **latest scan date** (the first grid column); AVG RANK is the average of the ranks present, to one decimal. Example: ranks 1, 5 and 9 give RANKED 3, TOP 3 = 1, TOP 5 = 2, AVG RANK = 5.0.

## Data and Storage

| Data | Stored where | Notes |
|------|--------------|-------|
| Brand ↔ property ID | Brand setup | Set once per brand |
| Source data | Semrush, read through the Semrush API | Matched by property ID |
| Page data | Semrush | Read directly through the Semrush API |
| Summary card and grid | `POST fetch-product-leaderboard` (the page's single data call) | `{}` for the signed-in brand, or `{ "brandOverride": "{Brand}" }` when a brand is selected in the switcher |
| Usage tracking | `POST user_page_sessions` | `page_path: "/analytics/product-leaderboard"`, `user_id` |

Page details: `doc analytics/10-product-leaderboard.md`.

## Runbook: Client

1. Open **Analytics → Product Leaderboard**.
2. Read the summary card, then scroll the grid sideways to compare weeks (the page scrolls vertically over all rows; the Product Name column is not pinned and the header row stays at the top of its box). Columns and cells are not sortable or clickable.

## Troubleshooting

| Situation | What to check |
|-----------|---------------|
| "No Leaderboard Data Yet" | The data call returned nothing: the brand may have no products or no ranking data yet. If it should have products, check the property ID, then report it to the product team. |
| Product Leaderboard is not in the sidebar | The page is shown only for brands that have it enabled. |
| A product shows only `-` | It was not ranked on those dates (products that never ranked recently sit at the bottom, all dashes). |
| Someone wants to upload ranks | Not needed and not done. |
