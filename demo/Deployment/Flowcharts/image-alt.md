# Image Alt – Workflow

The Image Alt page improves the ALT text of images on a brand's website pages, per brand and per month.

## Main workflow

```mermaid
flowchart TD
  subgraph IT["Internal Team"]
    A["Select brand and month"]
    B{"Add rows how?"}
    C{"File valid?"}
    C1["Whole upload rejected with reason"]
    C2["Error shown"]
    C3{"Same Website Page URL and Image URL<br/>already in this brand and month?"}
    D["Row added"]
    E["Row starts as Approval Pending"]
    H["Read comment and edit Suggested ALT"]
    I["Resubmit"]
    L["Confirm ALT updated on website"]
    M["Mark Live on Website"]
    N["Click send email button below table"]
    A --> B
    B -->|"CSV upload"| C
    C -->|"No"| C1
    C3 -->|"Yes"| C2
    B -->|"Manual add"| C3
    C -->|"Yes"| C3
    C3 -->|"No"| D
    D --> E
    H --> I
    I --> E
    L --> M
  end

  subgraph BU["Brand User"]
    F["Compare Current ALT with Suggested ALT"]
    G{"Decision"}
    J["Approved"]
    K["Disapproved"]
    Z["Click Notify on dashboard"]
    F --> G
    G -->|"Approve"| J
    G -->|"Disapprove with comment"| K
  end

  subgraph SE["System / Emails"]
    O["Brand receives update on team edits<br/>since last click"]
    P["Plain-text disapproval summary<br/>to assigned team lead"]
    Q["Live on Website"]
  end

  E --> F
  N --> O
  Z --> P
  K --> H
  J --> L
  M --> Q
  J -.->|"Brand may also mark Live"| Q
  Q --> N
```

## Status changes

```mermaid
stateDiagram-v2
  [*] --> ApprovalPending: System sets on upload or manual add
  ApprovalPending --> Approved: Brand approves
  ApprovalPending --> Disapproved: Brand disapproves with comment
  Disapproved --> ApprovalPending: Team edits Suggested ALT and resubmits
  Approved --> ApprovalPending: Team edits row
  Approved --> LiveOnWebsite: Team or brand marks Live
  LiveOnWebsite --> ApprovalPending: Team edits row
```

## Key rules

- Team Leads, Team Members and Admins cannot approve or disapprove; only the brand can.
- A disapproval needs a comment, and brand users can comment only when disapproving.
- Any edit resets the row to Approval Pending, whatever its status.
- Only an Approved row can be marked Live on Website.
- One send email button sends everything changed since the last click for that brand and month.
- The disapproval summary to the team lead comes from the brand's dashboard Notify button, not from the page button.
- The duplicate check applies to both CSV upload and manual add. A row is a duplicate when the same Website Page URL and Image URL already exist in the same brand and month.
