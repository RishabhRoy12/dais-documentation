# Local Listings

UI reference: [../UI/11-local-listings.md](../UI/11-local-listings.md)

| | |
|---|---|
| **Data source** | Google Sheet (the team's local listing tracking sheet) |
| **Update frequency** | **Monthly** |
| **Updated by** | Internal team adds the month's figures to the sheet |
| **Fetch call** | `POST fetch-local-listings` |

## Data flow

1. Each month the internal team adds the brand's local listing figures (posts, reviews, impressions) to the Google Sheet.
2. When a user opens the page, `fetch-local-listings` reads the sheet and returns the monthly data for the brand.
3. The page calculates the summary card and the insight sentence from it.

## Sheet data used by the page

| Data | Shown as |
|------|----------|
| Month | Month dropdown and MONTHS TRACKED |
| Posts | TOTAL POSTS |
| Reviews | TOTAL REVIEWS and AVERAGE REVIEWS |
| Impressions | IMPRESSIONS |

> Exact column names in the sheet are not documented yet. Add them here once confirmed.

## Rules

- No data in the sheet for a brand → page shows the empty state "No Listings Yet".
- The month dropdown lists months by name only (no year).

## Open items

- Confirm the sheet's column names.
- The layout for individual posts was not visible in testing (the sampled brand had 0 posts). Confirm whether the page should list posts.
