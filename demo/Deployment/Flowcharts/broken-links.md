# Broken Links – Workflow

Plans and tracks broken links found for a brand and the fix for each one (for example a 301 redirect), per brand and per month. Each row is one broken link.

## Main workflow

```mermaid
flowchart TD
  subgraph Team["Internal Team (Team Lead / Team Member)"]
    A1["Select brand and month"] --> A2{"Add entries how?"}
    A2 -->|"Sample CSV, Upload CSV"| A3{"CSV valid? Page URL, Broken Link, Action filled, https links"}
    A2 -->|"Add row"| A4{"Fields valid and not a duplicate this month?"}
    A3 -->|"No"| A5["Upload rejected with reason"]
    A3 -->|"Yes, Page URL plus Broken Link not already in month"| A6["Rows added as Approval Pending"]
    A4 -->|"No"| A7["Error shown"]
    A4 -->|"Yes"| A6
    A6 --> A8["Click Notify new rows"]
    D1["Read Client Comments"] --> D2["Update action or redirect URL with pencil, save"]
    D2 --> D3["Reply in DIAS Comments"]
    D3 --> D4["Click Notify changes"]
    L1["Fix done on website, for example 301 in place"] --> L2["Set Live on Website"]
  end
  subgraph Brand["Brand User"]
    B1["Review broken link and proposed fix"] --> B2{"Decision"}
    B2 -->|"Approve"| B3["Status Approved"]
    B2 -->|"Disapprove, write Client Comment"| B4["Status Disapproved"]
    B5["Click dashboard Notify"]
  end
  subgraph Sys["System / Emails"]
    S1["Email to brand"]
    S2["Edit resets row to Approval Pending, Last Updated refreshed"]
    S3["Plain-text approved and disapproved counts emailed to assigned team lead"]
  end
  A8 --> S1 --> B1
  B4 --> D1
  D2 --> S2
  D4 --> S1
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
  [*] --> AP: System, on upload or Add row
  AP --> AG: Brand approves
  AP --> DG: Brand disapproves with Client Comment
  AG --> LV: Team or Brand marks Live
  AG --> AP: System, row edited
  DG --> AP: System, action or redirect URL edited
  LV --> AP: System, row edited
  DG --> AP: Team sets via dropdown
  AG --> AP: Team sets via dropdown
```

## Key rules

- Fields: Page URL, Broken Link and Action To be Taken are required; Reference Screenshot and URL for Redirection are optional.
- Duplicate means the same Page URL with the same Broken Link in the same brand and month; allowed across months.
- DIAS Comments are the team's and can be added at any time; Client Comments are the brand's and only when disapproving. Comments never change status.
- Only the brand sets Approved or Disapproved; Live on Website needs Approved first. Any edit resets to Approval Pending.
- Last Updated fills in automatically on every add or change and cannot be edited.
- No automatic emails; deleting is permanent, allowed in any status, and not counted in Notify changes.
