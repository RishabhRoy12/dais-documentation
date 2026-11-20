# Reviews on Online Communities – Workflow

Prepares and tracks reviews written about a brand for posting on third-party community and business-listing sites, per brand and per month.

## Main workflow

```mermaid
flowchart TD
  subgraph Team["Internal Team (Team Lead / Team Member)"]
    A1["Select brand and month"] --> A2{"Add reviews how?"}
    A2 -->|"Download Sample CSV, Upload CSV"| A3{"CSV valid? Review and Link filled, https link"}
    A2 -->|"Add Manually: Review and Link"| A4{"Fields filled, valid link, not a duplicate this month?"}
    A3 -->|"No"| A5["Whole upload rejected with reason"]
    A3 -->|"Yes, same review and link not already in month"| A6["Rows added as Approval Pending, CSV comment saved as comment"]
    A4 -->|"No"| A7["Error shown"]
    A4 -->|"Yes"| A6
    A6 --> A8["Click Notify new rows"]
    D1["Read brand comment"] --> D2["Edit review text or link with pencil, save"]
    D2 --> D3["Click Notify changes"]
    L1["Review posted on online community"] --> L2["Set Live on Website"]
  end
  subgraph Brand["Brand User"]
    B1["Read review, open link, check it is right to post"] --> B2{"Decision"}
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
  [*] --> AP: System, on upload or manual add, CSV comment does not change this
  AP --> AG: Brand approves
  AP --> DG: Brand disapproves with comment
  AG --> LV: Team or Brand marks Live
  AG --> AP: System, review text or link edited
  DG --> AP: System, review text or link edited
  LV --> AP: System, review text or link edited
  DG --> AP: Team sets via dropdown
  AG --> AP: Team sets via dropdown
```

## Key rules

- Each row has two mandatory fields, Review and Link. The CSV has three columns: Review, Link and optional Comment.
- A CSV comment is saved as a comment by the uploader and never changes the status.
- Duplicate means the same review with the same link in the same brand and month; allowed across months.
- Only the brand can set Approved or Disapproved; a row can be Live on Website only when Approved.
- Editing the review text or link resets to Approval Pending; the dropdown and comments do not.
- No automatic emails; brand comments only when disapproving; deleting is permanent and not counted in Notify changes.
