# Monthly Reports – Workflow

The Monthly Reports page shows each brand its monthly performance report, and behind the scenes works as an internal approval desk: an uploader adds the report, an approver reviews it, and the uploader then publishes it to the brand with Notify Client.

## Main workflow

```mermaid
flowchart TD
  subgraph UP["Uploader (or Admin for review and notify)"]
    U1["Select brand, click Upload Report"]
    U2["Pick Brand and Report Month<br/>paste Google Slides, PPT or PDF link"]
    U3{"Link starts with https://?"}
    U4{"Report already exists<br/>for this brand and month?"}
    U5["Tick Replace the existing report<br/>and send it back for approval"]
    U6["Save report"]
    U7["Read remarks on card, click Update Report<br/>paste new link, Submit for Approval"]
    U8["Click Notify Client"]
    U9["Review recipients: remove people, add emails<br/>correct WhatsApp numbers<br/>choose Email and/or WhatsApp, confirm"]
    U10["Click Retry Email or Retry WhatsApp<br/>for the failed channel only"]
    U1 --> U2
    U2 --> U3
    U3 -->|"No"| U2
    U3 -->|"Yes"| U4
    U4 -->|"Yes"| U5
    U4 -->|"No"| U6
    U5 --> U6
    U8 --> U9
  end

  subgraph AP["Approver (or Admin)"]
    A1["Open approval queue, click Review<br/>preview deck and activity timeline"]
    A2{"Decision"}
    A3["Approve"]
    A4["Request Changes<br/>remarks of at least 50 characters"]
    A1 --> A2
    A2 -->|"Approve"| A3
    A2 -->|"Request Changes"| A4
  end

  subgraph SY["System / Emails"]
    S1["Status: Pending Approval"]
    S2["Internal email to approver<br/>in-app needs-approval alert to admins and team leads"]
    S3["Status: Approved - Ready to Notify<br/>internal email to uploader"]
    S4["Status: Changes Required<br/>internal email to uploader with remarks"]
    S5["Report published to the brand immediately<br/>Edit and Delete locked"]
    S6["Email and WhatsApp sent<br/>people who already got that exact email are skipped"]
    S7{"Delivery result"}
    S8["Status: Client Notified"]
    S9["Notification Partially Failed or Failed<br/>status stays Approved, error shown on card"]
    S1 --> S2
    S5 --> S6
    S6 --> S7
    S7 -->|"All delivered"| S8
    S7 -->|"One or all channels failed"| S9
  end

  subgraph BR["Brand User"]
    B1["Report card appears on Monthly Reports page<br/>no status, remarks or buttons shown"]
    B2["Click View Report<br/>deck opens full-screen"]
    B1 --> B2
  end

  U6 --> S1
  S2 --> A1
  A3 --> S3
  A4 --> S4
  S3 --> U8
  S4 --> U7
  U7 --> S1
  U9 --> S5
  S5 --> B1
  S9 --> U10
  U10 --> S6
```

## Status changes

```mermaid
stateDiagram-v2
  state "Pending Approval" as PendingApproval
  state "Changes Required" as ChangesRequired
  state "Approved - Ready to Notify" as Approved
  state "Client Notified" as ClientNotified
  [*] --> PendingApproval : Uploader saves the report link
  PendingApproval --> Approved : Approver or Admin clicks Approve
  PendingApproval --> ChangesRequired : Approver or Admin requests changes with remarks
  ChangesRequired --> PendingApproval : Uploader submits the new link for approval
  Approved --> ClientNotified : Uploader or Admin clicks Notify Client and all messages are delivered
  Approved --> Approved : Partly or fully failed notification, uploader retries the failed channel
  ClientNotified --> [*]
```

## Which report a card shows

```mermaid
flowchart LR
  P["Platform upload for the month<br/>(approval flow)"]
  G["Master Google Sheet link for the month<br/>or built-in backup list"]
  Q{"Both exist<br/>for the same month?"}
  W["Card shows the platform-uploaded report"]
  X["Card shows whichever source has the report"]
  C["Cards sorted newest month first<br/>Year selector filters them"]
  P --> Q
  G --> Q
  Q -->|"Yes"| W
  Q -->|"No"| X
  W --> C
  X --> C
```

## Key rules

- Only the approver or an admin can approve or request changes, and nobody can approve their own upload.
- Request Changes always needs remarks of at least 50 characters.
- A report cannot be sent to the brand before it is approved.
- The report becomes visible to the brand the moment Notify Client is clicked, even if a message later fails. A retry resends only the failed channel.
- After publishing, Edit and Delete are locked.
- Brand users see only published reports. The Deployment rules (CSV upload, Approval Pending / Approved / Disapproved / Live on Website, brand dashboard Notify) do not apply to this page.
