# YouTube – Workflow

The YouTube page prepares the YouTube details (title, description, tags, file name, thumbnail name, first comment, playlist) for each brand video, per brand and per month.

## Main workflow

```mermaid
flowchart TD
  subgraph IT["Internal Team"]
    A["Select brand and month"]
    B{"Add rows how?"}
    C{"File valid, columns present,<br/>Video URL valid if filled?"}
    C1["Whole upload rejected with reason"]
    D["Fill form, only Keyword mandatory"]
    E["Rows added as Approval Pending<br/>no duplicate check"]
    F["Click Notify new rows"]
    H["Read comment and Edit row"]
    I["Save, row resets to Approval Pending"]
    J["Click Notify changes"]
    L["Publish video on YouTube"]
    M["Add Video URL"]
    M1["Mark Live on Website"]
    A --> B
    B -->|"Download Sample CSV then Upload CSV"| C
    C -->|"No"| C1
    B -->|"Add Manually"| D
    C -->|"Yes"| E
    D --> E
    E --> F
    H --> I
    I --> J
    L --> M
    M --> M1
  end

  subgraph SE["System / Emails"]
    F1["Email to brand: details ready"]
    J1["Email to brand: edited rows to review"]
    Z1["Plain-text disapproval summary<br/>to assigned team lead"]
    Q["Live on Website"]
  end

  subgraph BU["Brand User"]
    K["Review row details"]
    N{"Decision"}
    O["Approved"]
    P["Disapproved"]
    Z["Click Notify on dashboard"]
    K --> N
    N -->|"Approve"| O
    N -->|"Disapprove with comment"| P
  end

  F --> F1
  J --> J1
  F1 --> K
  J1 --> K
  Z --> Z1
  P --> H
  I --> K
  O --> L
  M1 --> Q
  O -.->|"Brand may also mark Live"| Q
```

## Status changes

```mermaid
stateDiagram-v2
  [*] --> ApprovalPending: System sets on upload or manual add
  ApprovalPending --> Approved: Brand approves
  ApprovalPending --> Disapproved: Brand disapproves with comment
  Disapproved --> ApprovalPending: Team edits row
  Approved --> ApprovalPending: Team edits row
  Approved --> LiveOnWebsite: Team or brand marks Live, needs Video URL
  LiveOnWebsite --> ApprovalPending: Team edits other fields
  Approved --> Approved: Video URL added or changed, no reset
  LiveOnWebsite --> LiveOnWebsite: Video URL changed, no reset
```

## Key rules

- Exception to the reset rule: adding or changing the Video URL, or marking the row Live on Website, keeps the current status.
- Live on Website needs the row to be Approved and the Video URL filled with a valid YouTube link.
- Only Keyword is mandatory; there is no duplicate check for now.
- No emails are sent automatically; Notify new rows counts added rows and Notify changes counts edited rows, never deleted rows.
- Admin, Team Lead and Team Member cannot approve or disapprove; only the brand can. Team Leads and Members see assigned brands only.
- Delete needs confirmation, works in any status including Live on Website, and cannot be undone.
