# Profile Citation – Workflow

The Profile Citation page plans and tracks profile pages created for a brand on third-party websites, one Link per row, per brand and per month.

## Main workflow

```mermaid
flowchart TD
  subgraph IT["Internal Team"]
    A["Select brand and month"]
    B{"Add links how?"}
    C{"File valid?"}
    C1["Whole upload rejected with reason"]
    D["Enter Link"]
    E{"Valid https URL and<br/>not already added for brand?"}
    E1["Error shown, duplicate checked<br/>across months"]
    F["Row added as Approval Pending"]
    G["Click Notify new rows"]
    H["Read comment, update link or reply"]
    I["Editing link resets<br/>row to Approval Pending"]
    J["Click Notify changes"]
    L["Create the profile citation"]
    M["Publish and set Live on Website<br/>via status dropdown"]
    A --> B
    B -->|"Download Sample CSV then Upload CSV"| C
    C -->|"No"| C1
    B -->|"Add Manually"| D
    C -->|"Yes"| E
    D --> E
    E -->|"No"| E1
    E -->|"Yes"| F
    F --> G
    H --> I
    I --> J
    L --> M
  end

  subgraph SE["System / Emails"]
    G1["Email to brand: new links added"]
    J1["Email to brand: updates after feedback"]
    Z1["Plain-text disapproval summary<br/>to assigned team lead"]
    Q["Live on Website"]
  end

  subgraph BU["Brand User"]
    K["Open each Link and review"]
    N{"Decision"}
    O["Approved"]
    P["Disapproved"]
    Z["Click Notify on dashboard"]
    K --> N
    N -->|"Approve"| O
    N -->|"Disapprove with comment"| P
  end

  G --> G1
  J --> J1
  G1 --> K
  J1 --> K
  Z --> Z1
  P --> H
  I --> K
  O --> L
  M --> Q
  O -.->|"Brand may also mark Live"| Q
```

## Status changes

```mermaid
stateDiagram-v2
  [*] --> ApprovalPending: System sets on upload or manual add
  ApprovalPending --> Approved: Brand approves link
  ApprovalPending --> Disapproved: Brand disapproves with comment
  Disapproved --> ApprovalPending: Team edits or replaces link
  Approved --> ApprovalPending: Team edits or replaces link
  Approved --> LiveOnWebsite: Team or brand marks Live
  LiveOnWebsite --> ApprovalPending: Team edits or replaces link
  Approved --> ApprovalPending: Team sets via dropdown, not an edit
  LiveOnWebsite --> ApprovalPending: Team sets via dropdown, not an edit
```

## Key rules

- Team Leads and Members can set only Approval Pending or Live on Website with the dropdown; Approved and Disapproved are brand-only. Admins cannot approve or disapprove either.
- Using the status dropdown does not reset the row; editing or replacing the link does.
- The same link cannot be added twice for a brand, even across different months.
- Each row has one field only: the Link, which must be a valid https URL.
- No emails are sent automatically; deleted rows are not counted under Notify changes, and delete works in any status.
- Admins, Team Leads and Team Members can add comments; brands can comment only when disapproving.
