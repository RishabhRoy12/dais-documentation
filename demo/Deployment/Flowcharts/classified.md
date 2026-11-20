# Classified – Workflow

Plans and tracks classified-ad listings posted for a brand on third-party classified-ad sites, per brand and per month, one Link per row.

## Main workflow

```mermaid
flowchart TD
  subgraph TEAM["Internal Team (Team Lead / Team Member)"]
    T1["Select brand and month<br/>(confirm month first)"]
    T2{"Add links how?"}
    T3["Download Sample CSV<br/>(columns: Links and optional Comment)<br/>then Upload CSV"]
    T4["Add Manually<br/>enter link and save"]
    T5{"Valid https URL,<br/>valid file, not a duplicate<br/>for this brand and month?"}
    T6["Rejected with reason or error<br/>(whole upload rejected if file invalid)"]
    T7["Click Notify new rows"]
    T8["Read comment, edit or replace link<br/>(pencil) and save"]
    T9["Click Notify changes"]
    T10["Mark Live on Website<br/>(dropdown, row must be Approved)"]
  end
  subgraph SYS["System / Emails"]
    S1["Rows added as Approval Pending"]
    S2["Email to brand: new links"]
    S3["Row reset to Approval Pending"]
    S4["Email to brand: updates"]
    S5["Plain-text email to assigned team lead<br/>approved and disapproved counts"]
  end
  subgraph BRAND["Brand User"]
    B1["Open link and review classified listing"]
    B2{"Decision"}
    B3["Approve"]
    B4["Disapprove and add comment"]
    B5["Row is Live on Website"]
    B6["Click dashboard Notify<br/>when review is finished"]
  end
  T1 --> T2
  T2 -->|"CSV"| T3
  T2 -->|"Manual"| T4
  T3 --> T5
  T4 --> T5
  T5 -->|"No"| T6
  T6 --> T2
  T5 -->|"Yes"| S1
  S1 --> T7
  T7 --> S2
  S2 --> B1
  B1 --> B2
  B2 -->|"Approve"| B3
  B2 -->|"Disapprove"| B4
  B4 --> T8
  T8 --> S3
  S3 --> T9
  T9 --> S4
  S4 --> B1
  B3 --> T10
  T10 --> B5
  B3 -.->|"Brand may also mark Live"| B5
  B5 --> B6
  B6 --> S5
```

## Status changes

```mermaid
stateDiagram-v2
  state "Approval Pending" as ApprovalPending
  state "Live on Website" as LiveOnWebsite
  [*] --> ApprovalPending : System - row added by upload or manual add
  ApprovalPending --> Approved : Brand user approves
  ApprovalPending --> Disapproved : Brand user disapproves with comment
  Approved --> LiveOnWebsite : Team or Brand marks Live after classified listing published
  Approved --> ApprovalPending : System - link edited or replaced
  Disapproved --> ApprovalPending : System - link edited or replaced
  LiveOnWebsite --> ApprovalPending : System - link edited or replaced
  ApprovalPending --> ApprovalPending : Team sets Pending via dropdown or link edited
```

## Key rules

- Only the brand user can set Approved or Disapproved. Team and Admin cannot, even on the brand's behalf.
- The team's status dropdown offers only Approval Pending and Live on Website. Using it does not reset the row; editing or replacing the link does. A row can be marked Live on Website only if it is Approved.
- No emails are automatic. One click of a Notify button sends everything changed since the last click for the selected brand and month; a counter at (0) means nothing is pending.
- The same link cannot be added twice for a brand in the same month, but is allowed in different months.
- The CSV has two columns, Links and an optional Comment. The comment is saved on the row as written by the uploader and never changes the status.
- Team and Admin can add comments at any time; brands only when disapproving. Adding a comment never changes status. Deleting a row is permanent, allowed in any status, and not counted under Notify changes.
