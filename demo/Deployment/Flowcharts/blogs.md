# Blogs – Workflow

A read-only progress board listing each brand's blogs month by month, with topic status, blog status, final status and live link. All work happens in Blog Generator.

## Main workflow

```mermaid
flowchart TD
  subgraph BG["Blog Generator (where work happens)"]
    G1["Team creates topics"] --> G2{"Topic decision"}
    G2 -->|"Approve"| G3["Blog written and reviewed"]
    G2 -->|"Disapprove or reject"| G4["Changes requested or Rejected"]
    G3 --> G5{"Blog decision"}
    G5 -->|"Approved"| G6["Mark Live on Website and or add live link"]
    G5 -->|"Disapproved"| G3
  end
  subgraph Src["Data sources"]
    D1["Blog Generator topics, month created"]
    D2["Google Sheet: earlier records, old database"]
  end
  subgraph Page["Blogs page, read-only"]
    P1["User opens page, latest statuses read on each load"] --> P2["Select brand and month"]
    P2 --> P3["Table: topic, keyword, Topic Status, Blog Status, Final Status, Live Link"]
    P3 --> P4{"User action"}
    P4 -->|"Click Topic Status or Blog Status"| P5["Opens that topic in Blog Generator"]
    P4 -->|"Click Visit"| P6["Opens live blog in new tab"]
  end
  G6 --> D1
  G1 --> D1
  D1 --> P1
  D2 --> P1
  P5 --> G2
```

## Status mapping

How Blog Generator labels and the Google Sheet show on the page.

```mermaid
flowchart LR
  subgraph TS["Topic Status, Blog Generator"]
    T1["Draft: Approval Pending, staff only"]
    T2["Awaiting brand: Approval Pending"]
    T3["Changes requested: Disapproved"]
    T4["Accepted: Approved"]
    T5["Rejected: Disapproved, hidden"]
  end
  subgraph BS["Blog Status, Blog Generator"]
    B1["Not started: Approval Pending"]
    B2["Changes requested: Disapproved"]
    B3["Accepted: Approved"]
    B4["Rejected: Disapproved, row still shown"]
    B5["Published: Live on Website"]
  end
  subgraph FS["Final Status"]
    F1["Live on Website"]
    F2["In progress"]
  end
  B5 --> F1
  LK{"Any live link present?"}
  LK -->|"Yes, link not checked"| F1
  LK -->|"No"| F2
  SH["Sheet status says Live on Website"] --> F1
  SH2["Sheet row: status text shown as Topic Status, Blog Status blank"] --> LK
```

## Key rules

- No upload, add, edit, delete, approval, comments, Notify buttons or emails on this page, for any role.
- Statuses refresh only on the next page load. Topics are placed in the month they were created.
- Draft topics are hidden from brand users; rejected topics are hidden from everyone.
- Earlier sheet records load only for Paid or Lite plans, admins and sub-admins, or the listed allowed brands. The same blog can appear twice because the sources are not merged.
- Any live link, unchecked, is enough to show Live on Website.
- Brand users see only their own brand; internal staff see assigned brands; admins see any brand.
