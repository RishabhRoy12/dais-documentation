# Reddit/Quora – Workflow

Records answers posted on Reddit and Quora threads for a brand, per brand and per month. There is no approval step: the team adds entries and notifies the brand, who only views them.

## Main workflow

```mermaid
flowchart TD
  subgraph Team["Internal Team (Team Lead / Team Member)"]
    A1["Select brand and month"] --> A2{"Add entries how?"}
    A2 -->|"Download Sample CSV, Upload CSV"| A3{"CSV valid? Question and Answer filled, https links"}
    A2 -->|"Add Manually"| A4{"Question and Answer filled, links valid?"}
    A3 -->|"No"| A5["Upload rejected with reason"]
    A3 -->|"Yes"| A6["Entries appear in table"]
    A4 -->|"No"| A7["Error shown"]
    A4 -->|"Yes"| A6
    A6 --> A8["Check rows"]
    A8 --> A9{"Change needed?"}
    A9 -->|"Edit with pencil"| A8
    A9 -->|"Delete with bin, permanent"| A8
    A9 -->|"All rows added"| A10["Click Notify at bottom bar"]
  end
  subgraph Sys["System / Emails"]
    S1["One email to brand: entries are ready"]
  end
  subgraph Brand["Brand User"]
    B1["View entries, open links, copy answers"]
  end
  A10 --> S1 --> B1
```

## Notify flow

No status, comments or approval exist on this page. Notify is the only email step.

```mermaid
flowchart LR
  N1["Add all rows first"] --> N2["Click Notify, no counter"]
  N2 --> N3["Brand gets one email"]
  N3 --> N4["Brand views only, no approve or comment"]
  N5["Later changes: Notify again sends everything changed since last click"] -.-> N2
```

## Key rules

- Fields: Question (thread link, required), Answer (required), Live Link (optional, shows a dash when empty). CSV headers are Question, Answer and Live Link.
- Links must be valid https URLs; no duplicate check is described.
- Editing a row changes nothing else, because there is no status.
- No automatic emails. Click Notify only after all rows are added, since the page is built to send one email per brand.
- Brand users cannot add, edit, delete, comment or mark Live, and have no Notify button here.
