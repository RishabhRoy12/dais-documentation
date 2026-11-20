# Strategic Sync-ups

UI reference: [../../UI/13-strategic-sync-ups.md](../../UI/13-strategic-sync-ups.md)

| | |
|---|---|
| **Data source** | Entered manually in the app (not from a Google Sheet) |
| **Update frequency** | No fixed schedule: whenever the internal team holds and records a meeting |
| **Updated by** | **Internal team, manually** |
| **API** | `POST manage-mom` |

## Data flow

1. After a meeting, the internal team opens **New Meeting** and pastes the raw meeting notes.
2. **Process with AI** saves the meeting and extracts the summary, DAIS tasks, brand-side tasks and decisions.
3. The team can edit the summary, tasks and decisions, add tasks and decisions, regenerate the AI output or delete items.
4. Saved meetings appear in the list for the brand, newest first, and can be searched.

## Rules

- Only the raw notes are required; title, date, brand and attendees are optional or pre-filled.
- Add Task and delete actions save immediately, with no confirmation.
- This is the only analytics page that **writes** data.

## Open items

- Decide who may create or edit meetings (the page checks admin, sub-admin and internal-team roles).
- Decide whether brand users may see the page or only the internal team.
