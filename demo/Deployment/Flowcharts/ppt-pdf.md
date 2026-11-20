# PPT/PDF Submission – Workflow

Plans and tracks presentations (PPT) and documents (PDF) submitted for a brand to third-party document-sharing sites, per brand and per month.

## Main workflow

```mermaid
flowchart TD
  subgraph Team["Internal Team (Team Lead / Team Member)"]
    A1["Select brand and month"] --> A2{"Add links how?"}
    A2 -->|"Download Sample CSV, Upload CSV"| A3{"CSV valid?"}
    A2 -->|"Add Manually"| A4{"Valid https link and not a duplicate this month?"}
    A3 -->|"No"| A5["Whole upload rejected with reason"]
    A3 -->|"Yes, duplicates checked per brand and month"| A6["Rows added as Approval Pending"]
    A4 -->|"No"| A7["Error shown"]
    A4 -->|"Yes"| A6
    A6 --> A8["Click Notify new rows"]
    D1["Read brand comment"] --> D2["Edit or replace link with pencil, save"]
    D2 --> D3["Click Notify changes"]
    L1["PPT or PDF published on sharing site"] --> L2["Set Live on Website"]
  end
  subgraph Brand["Brand User"]
    B1["Open link and review PPT or PDF"] --> B2{"Decision"}
    B2 -->|"Approve"| B3["Status Approved"]
    B2 -->|"Disapprove with comment"| B4["Status Disapproved"]
    B5["Click dashboard Notify"]
  end
  subgraph Sys["System / Emails"]
    S1["Email to brand"]
    S2["Edit resets row to Approval Pending"]
    S3["Plain-text approved and disapproved counts emailed to assigned team lead"]
  end
  A8 --> S1 --> B1
  B4 --> D1
  D2 --> S2
  S2 --> D3
  D3 --> S1
  B3 --> L1
  L2 --> B5
  B5 --> S3
```

## Status changes

```mermaid
stateDiagram-v2
  state "Approval Pending" as AP
  state "Approved" as AG
  state "Disapproved" as DG
  state "Live on Website" as LV
  [*] --> AP: System, on upload or manual add
  AP --> AG: Brand approves
  AP --> DG: Brand disapproves with comment
  AG --> LV: Team or Brand marks Live
  AG --> AP: System, link edited
  DG --> AP: System, link edited or replaced
  LV --> AP: System, link edited
  DG --> AP: Team sets via dropdown
  AG --> AP: Team sets via dropdown
```

## Key rules

- Only the brand can set Approved or Disapproved; the team dropdown offers Approval Pending and Live on Website only.
- A row can be Live on Website only when Approved.
- Editing or replacing the link resets any status to Approval Pending; changing the dropdown or adding a comment does not.
- Same link cannot be added twice for a brand in the same month; the same link in different months is allowed. The CSV has one column, Links.
- No automatic emails. Notify new rows and Notify changes are manual; deleted rows are not counted. Deleting is permanent and allowed in any status.
- Admin cannot approve or disapprove. The brand can comment only when disapproving; the team can comment at any time.
