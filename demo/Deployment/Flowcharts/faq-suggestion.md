# FAQ Suggestion – Workflow

The FAQ Suggestion page is used to suggest FAQ questions and answers for pages of a brand's website, per brand and per month.

## Main workflow

```mermaid
flowchart TD
  subgraph IT["Internal Team"]
    A["Select brand and month"]
    B{"Add rows how?"}
    C{"File valid?"}
    C1["Whole upload rejected with reason"]
    D["Enter Page URL, Question, Answer"]
    E{"Same Page URL and<br/>same Suggested Question?"}
    E1["Duplicate error"]
    F["Row added as Approval Pending"]
    G["Click send email button"]
    H["Read comment, edit with pencil icon"]
    I["Resubmit"]
    L["Confirm FAQ is on website"]
    M["Mark Live on Website"]
    A --> B
    B -->|"Download Sample CSV then Upload CSV"| C
    C -->|"No"| C1
    B -->|"Add Manually"| D
    C -->|"Yes"| E
    D --> E
    E -->|"Yes"| E1
    E -->|"No"| F
    F --> G
    H --> I
    L --> M
  end

  subgraph SE["System / Emails"]
    G1["Brand gets everything changed<br/>since last click"]
    Z1["Plain-text disapproval summary<br/>to assigned team lead"]
    P["Live on Website"]
  end

  subgraph BU["Brand User"]
    J["Read Suggested Question and Answer"]
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
  Disapproved --> ApprovalPending: Team edits and resubmits
  Approved --> ApprovalPending: Team edits row
  Approved --> LiveOnWebsite: Team or brand marks Live
  LiveOnWebsite --> ApprovalPending: Team edits row
```

## Key rules

- No emails are sent automatically; the team must click the send email button.
- Several questions for one URL are allowed; a duplicate is the same Page URL with the same Suggested Question.
- Internal users can delete a row in any status, including Live on Website, after confirmation; it cannot be recovered.
- Team Leads, Team Members and Admins cannot approve or disapprove; only the brand can.
- Any edit resets the row to Approval Pending, and only Approved rows can be marked Live.
- A row can hold several comments, and brand users can comment only when disapproving.
