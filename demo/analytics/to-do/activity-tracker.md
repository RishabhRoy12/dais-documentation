# Activity Tracker

UI reference: [../UI/12-activity-tracker.md](../UI/12-activity-tracker.md)

| | |
|---|---|
| **Data source** | Google Sheet (the team's activity log) |
| **Update frequency** | **Once every 4 days** |
| **Updated by** | Internal team adds the activities completed since the last update |
| **Fetch call** | `POST fetch-activity-data` |

## Data flow

1. Every 4 days the internal team adds the recent activities (work done for the brand) to the Google Sheet.
2. When a user opens the page, `fetch-activity-data` reads the sheet and returns the activity list for the brand.
3. The page shows "Data as of {date}" and the list, newest first.

## Sheet data used by the page

| Data | Shown as |
|------|----------|
| Activity text | The sentence on each row |
| Date | Right-aligned date on each row |

The banner date is the date of the **latest activity row**, not today's date.

> Exact column names in the sheet are not documented yet. Add them here once confirmed.

## Rules

- Because updates come every 4 days, the banner date can be up to about 4 days behind today.
- Rows are shown newest first; several rows can share a date.
- The page is read-only.

## Open items

- Confirm the sheet's column names.
- Confirm what the page should show when a brand has no activity rows (no empty state was captured).
