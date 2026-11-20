# Brand Voice – Workflow

Brand Voice turns a brand's approved blogs (and brand book, if any) into a 12-section Brand Voice Document, then uses that document to review new drafts. For the written runbook, see [Execution/brand-voice.md](../Execution/brand-voice.md).

## Access by role

```mermaid
flowchart TD
  A["User opens Intelligence > Brand Voice"] --> B{"Who is signed in?"}
  B -->|"Admin"| AD["Generator tab: full control<br/>blogs, Add Blog, Generate, monthly switch, History<br/>Review tab: sees and deletes all reviews"]
  B -->|"Sub-admin / internal team"| SA["Generator tab: manager layout<br/>blog list loads empty, Generate refused 'Admin only'<br/>Review tab: sub-admin sees all reviews, others see own"]
  B -->|"Brand user (incl. Lite)"| BU["Brand Voice Document tab: read-only<br/>search, section jump, Copy, History<br/>Review tab: sees and deletes own reviews"]
```

## Flow A: building the Brand Voice Document

```mermaid
flowchart TD
  subgraph AD["Admin"]
    A1["Select brand<br/>page loads brand book, blogs,<br/>current document, monthly switch"]
    A2["Add Blog (optional)<br/>paste text or fetch URL, title, about 50 words or more"]
    A3{"Brand book<br/>or 3+ approved blogs?"}
    A4["Add N more blogs<br/>Generate stays disabled"]
    A5["Click Generate / Regenerate"]
    A6["Read, search, jump to sections, Copy<br/>open History to preview old versions"]
    A1 --> A2
    A1 --> A3
    A2 --> A3
    A3 -->|"No"| A4
    A4 --> A2
    A3 -->|"Yes"| A5
  end

  subgraph SY["System"]
    S1["Automatic sync from Deployment > Blogs"]
    S2["Keep Approved, Live on Website,<br/>Live or Published only"]
    S3["Remove link-imported blogs no longer approved<br/>pasted blogs always kept"]
    S4["Collapse duplicate titles, keep newest<br/>upgrade content-deck link to live link"]
    S5["Fetch new approved blogs<br/>message: N approved blogs auto-imported"]
    S6["AI reads brand book first, blogs second<br/>saved instructions + fixed rules:<br/>grounded, no invented traits, positively framed"]
    S7["About 30-60 seconds<br/>save new version<br/>v1 AI Generated, later AI Refreshed"]
    S8["New version becomes Active<br/>previous version kept in History"]
    S1 --> S2 --> S3 --> S4 --> S5
    S6 --> S7 --> S8
  end

  A1 --> S1
  S5 --> A3
  A5 --> S6
  S8 --> A6
```

## The 12 sections of every document

```mermaid
flowchart LR
  D["Brand Voice Document"] --> G1["1 Brand Understanding<br/>2 Target Audience<br/>3 Brand Voice Summary"]
  D --> G2["4 Writing Style<br/>5 Blog Structure<br/>6 SEO and GEO<br/>7 Language"]
  D --> G3["8 Do's and Don'ts<br/>9 CTA Guidelines<br/>10 Approved Content Patterns"]
  D --> G4["11 Content Examples<br/>12 Quality Checklist"]
```

## Flow B: reviewing a draft

```mermaid
flowchart TD
  subgraph US["Any user (admin, internal, brand)"]
    U1["Open Brand Voice Review tab"]
    U2["Add optional title<br/>paste draft or upload .txt / .md up to 1.5 MB<br/>at least 20 words"]
    U3["Click Review Content"]
    U4["Read verdict, three groups, scorecard, report<br/>Copy report"]
    U5["Open History, reload or delete a review"]
    U1 --> U2
    U2 --> U3
  end

  subgraph SY["System"]
    S1{"Active Brand Voice<br/>Document for brand?"}
    S2["Warning: generate a document first<br/>Review button disabled"]
    S3["AI reviews draft against brand book (if any)<br/>and active document, using saved review instructions"]
    S4{"Overall verdict"}
    S5["Approved"]
    S6["Needs Revision"]
    S7["Disapproved"]
    S8["Groups: Approved / Disapproved / Needs Revision<br/>each with reasons or fixes, plus scorecard"]
    S9["Review saved automatically<br/>up to 50 shown in History"]
    S1 -->|"No"| S2
    S3 --> S4
    S4 --> S5
    S4 --> S6
    S4 --> S7
    S5 --> S8
    S6 --> S8
    S7 --> S8
    S8 --> S9
  end

  U1 --> S1
  S1 -->|"Yes"| U2
  U3 --> S3
  S8 --> U4
  S9 --> U5
```

## Document versions

```mermaid
stateDiagram-v2
  [*] --> NoDocument
  NoDocument --> v1_Active: Generate (AI Generated)
  v1_Active --> v2_Active: Regenerate (AI Refreshed)
  v2_Active --> vN_Active: Regenerate again
  v1_Active --> History: replaced
  v2_Active --> History: replaced
  note right of History
    Up to 50 versions shown, newest first
    Preview only, cannot be re-activated from the page
  end note
```

## Key rules

- **Generate needs 3 approved blogs or a brand book.** The brand book wins where blogs disagree.
- **Only admins can generate or manage blogs.** Sub-admins and internal staff see the buttons but are refused.
- **Sync on page open can delete** link-imported blogs that are no longer approved in Deployment. Pasted blogs are kept.
- **Deleting a blog only affects future versions.** Regenerate to apply changes.
- **Review needs an active document** and at least 20 words of draft.
- **"Auto-refresh monthly" is a saved setting only**; nothing regenerates monthly yet.
- **No emails, WhatsApp or in-app alerts** are sent from this page.
