# Schema Markup – Workflow

The Schema Markup page plans, reviews and tracks structured data (JSON-LD) for pages of a brand's website, per brand and per month.

## Main workflow

```mermaid
flowchart TD
  subgraph IT["Internal Team"]
    A["Select brand and month"]
    B{"Add rows how?"}
    C{"File valid?"}
    C1["Whole upload rejected with reason"]
    D["Enter URL, Missing Schema, Recommended Schema"]
    E{"Same URL under same schema<br/>and valid JSON-LD?"}
    E1["Duplicate error"]
    E2["Rejected"]
    F["Row added as Approval Pending"]
    G["Click send email button"]
    H["Read comment and edit entry"]
    I["Resubmit"]
    L["Confirm schema is on website"]
    M["Mark Live on Website"]
    A --> B
    B -->|"Upload CSV"| C
    C -->|"No"| C1
    B -->|"Add Manually"| D
    C -->|"Yes"| E
    D --> E
    E -->|"Duplicate"| E1
    E -->|"Invalid JSON-LD"| E2
    E -->|"OK"| F
    F --> G
    H --> I
    L --> M
  end

  subgraph SE["System / Emails"]
    G1["Brand gets update on new rows and edits<br/>since last click"]
    Z1["Plain-text disapproval summary<br/>to assigned team lead"]
    P["Live on Website"]
  end

  subgraph BU["Brand User"]
    J["Review Recommended Schema"]
    K{"Decision"}
    N["Approved"]
    O["Disapproved"]
    Z["Click Notify on dashboard"]
    J --> K
    K -->|"Approve"| N
    K -->|"Disapprove with comment"| O
  end

  G --> G1
  G1 --> J
  Z --> Z1
  O --> H
  I --> F
  N --> L
  M --> P
  N -.->|"Brand may also mark Live"| P
  P --> G
```

## Status changes

```mermaid
stateDiagram-v2
  [*] --> ApprovalPending: System sets on upload or manual add
  ApprovalPending --> Approved: Brand approves
  ApprovalPending --> Disapproved: Brand disapproves with comment
  Disapproved --> ApprovalPending: Team edits entry and resubmits
  Approved --> ApprovalPending: Team edits row
  Approved --> LiveOnWebsite: Team or brand marks Live
  LiveOnWebsite --> ApprovalPending: Team edits row
```

## Key rules

- Each URL and Missing Schema pair is its own row with its own status; one URL can have several schemas.
- No emails are sent automatically; the team must click the send email button.
- Recommended Schema must be valid JSON-LD for both CSV and manual entries.
- Team Leads, Team Members and Admins cannot approve or disapprove; only the brand can.
- Any edit resets the row to Approval Pending, and only Approved rows can be marked Live.
- A row can hold several comments, and brand users can comment only when disapproving.
