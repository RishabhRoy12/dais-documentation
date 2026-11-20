# YouTube Analytics

UI reference: [../UI/09-youtube-analytics.md](../UI/09-youtube-analytics.md)

| | |
|---|---|
| **Data source** | Google Sheet (the team's YouTube tracking sheet) |
| **Update frequency** | **Monthly** |
| **Updated by** | Internal team adds the month's videos to the sheet |
| **Fetch call** | `POST fetch-youtube-data` |

## Data flow

1. Each month the internal team adds that month's videos (long videos and Shorts) to the brand's Google Sheet.
2. When a user opens the page, `fetch-youtube-data` reads the sheet and returns the videos for the brand.
3. The page shows the summary card, the insight lines and the video grid.

## Sheet data used by the page

| Data | Shown as |
|------|----------|
| Video link / thumbnail | Card thumbnail and "Watch on YouTube" link |
| Title | Card title |
| Type (Video or Shorts) | Type badge and the Shorts count |
| Month | Month badge and month dropdown |
| Original SEO score | ORIGINAL SEO SCORE |
| Optimized SEO score | OPTIMIZED SEO SCORE |

> Exact column names in the sheet are not documented yet. Add them here once confirmed.

## Rules

- No videos in the sheet for a brand → page shows the empty state "No Videos Yet".
- New data appears only after the month's rows are added to the sheet.

## Open items

- Confirm the sheet's column names.
- The month dropdown changes the two summary numbers but not the video grid (see the UI doc, section 3.3). Decide whether this should be fixed.
