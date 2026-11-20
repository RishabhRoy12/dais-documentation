# Meta Tags – Workflow

The Meta Tags page improves the URL, Title, Meta Description and H1 of a brand's website pages, per brand and per month.

## Main workflow

```mermaid
flowchart TD
  subgraph IT["Internal Team"]
    A["Select brand and month"]
    B{"Add pages how?"}
    C{"Headers match sample<br/>and Current URL present?"}
    C1["Whole file rejected or<br/>rows without Current URL skipped"]
    D["Rows saved immediately<br/>matched by Current URL plus keywords"]
    E["Save row with source Manual"]
    F{"Recommendations missing?"}
    G["AI fills missing fields only<br/>or click Generate missing"]
    H["Admin or Team Lead reviews<br/>AI changes and edits"]
    I["Click Notify new rows"]
    Q["Team reads remarks and edits<br/>recommended values"]
    T["Click Notify changes"]
    U{"Published on website?"}
    V["Team clicks rocket icon<br/>Live on Website"]
    A --> B
    B -->|"Upload CSV or Excel"| C
    C -->|"No"| C1
    C -->|"Yes"| D
    B -->|"Add Item"| E
    D --> F
    E --> F
    F -->|"Yes"| G
    G --> H
    F -->|"No"| I
    H --> I
    U -->|"Yes"| V
  end

  subgraph SE["System / Emails"]
    J["Email to all external users of the brand"]
    S1["Status recalculated on every save"]
    R["Edited field answer cleared<br/>row resets to Approval Pending"]
    Z1["Plain-text disapproval summary<br/>to assigned team lead"]
  end

  subgraph BU["Brand User"]
    K["Approve or reject each recommendation<br/>remarks mandatory on rejection"]
    L{"Submit button"}
    L1["Refused"]
    M{"Row result"}
    N["Approved"]
    O["Disapproved"]
    P["Approval Pending"]
    Z["Click Notify on dashboard"]
    K --> L
    L -->|"Approve with a rejection"| L1
    L -->|"Reject with no rejection"| L1
    L -->|"Rejection without remarks"| L1
    L1 --> K
    M -->|"All approved"| N
    M -->|"Any rejected"| O
    M -->|"Any unanswered"| P
  end

  I --> J
  J --> K
  L -->|"Valid submit"| S1
  S1 --> M
  Z --> Z1
  O --> Q
  Q --> R
  R --> T
  T --> J
  N --> U
  U -->|"No"| N
```

## Status changes

```mermaid
stateDiagram-v2
  [*] --> ApprovalPending: System sets on row creation
  ApprovalPending --> Approved: Brand approves every recommendation and submits
  ApprovalPending --> Disapproved: Brand rejects at least one with remarks
  Approved --> Disapproved: Brand rejects at least one with remarks
  Disapproved --> Approved: Brand approves all after team updates
  Approved --> ApprovalPending: Team edits or answer cleared
  Disapproved --> ApprovalPending: Team edits recommended value
  Approved --> LiveOnWebsite: Team or brand marks Live
  LiveOnWebsite --> ApprovalPending: Team edits row
  ApprovalPending --> ApprovalPending: Hidden column shown again, answers cleared
```

## Key rules

- Status is never typed in; it is recalculated on every save. Live on Website is the only manual status action.
- Only recommendations that have a value and sit in a visible column count towards status.
- Any internal edit resets the row to Approval Pending; if another field is still rejected the row stays Disapproved.
- Blank Recommended cells or blank keywords on re-upload overwrite saved values; blank Current Title, Description and H1 keep them.
- Showing a hidden Recommended column again clears brand answers for that field on all rows of the brand.
- The brand-side Notify button emails the assigned team lead a plain-text count summary covering all pages.
