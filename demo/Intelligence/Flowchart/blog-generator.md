# Blog Generator – Workflow

The Blog Generator takes a blog from an idea to a published article for a brand: a request becomes topics, the brand decides on each topic, a writer drafts the blog, the brand reviews it, and a team lead publishes it.

## Request and topics

```mermaid
flowchart TD
  subgraph BR["Brand User"]
    BR1{"Try a Blog!<br/>choose one"}
    BR2["Suggest keywords for the team"]
    BR3["Write own topic"]
    BR5["Open shared topic in side panel<br/>or tick several for bulk action"]
    BR6{"Brand decision"}
    BR7["Approve"]
    BR8["Reject<br/>comment required"]
    BR9["Request changes<br/>comment required"]
    BR1 -->|"Suggest keywords"| BR2
    BR1 -->|"Own topic"| BR3
    BR5 --> BR6
    BR6 -->|"Approve"| BR7
    BR6 -->|"Reject"| BR8
    BR6 -->|"Request changes"| BR9
  end

  subgraph TL["Internal Team (Team Lead, Admin, handed team member)"]
    T1["New request: Primary keyword required<br/>Secondary keywords and Prompt optional"]
    T1b["Bulk upload CSV or Excel<br/>up to 200 rows, each row is a request"]
    T2["Open side panel to review brand idea"]
    T3{"Team Lead or Admin decision"}
    T4["Approve"]
    T5["Reject<br/>note required"]
    T6["Hand research to a team member"]
    T7{"How to create topics?"}
    T8["Generate topics: fill brief, Save, Generate<br/>up to 5 ideas per round, save chosen as Draft"]
    T9["Add topic yourself<br/>one per line"]
    T10["Drafts saved<br/>internal only"]
    T11["Tick drafts and click Notify brand"]
    T12["Edit topic text with pencil icon<br/>goes back to Draft"]
    T13["All topics rejected:<br/>Regenerate or Add topic yourself"]
    T3 -->|"Approve"| T4
    T3 -->|"Reject"| T5
    T2 --> T3
    T4 --> T7
    T4 -.->|"Optional"| T6
    T7 -->|"Generate topics"| T8
    T7 -->|"Add topic yourself"| T9
    T8 --> T10
    T9 -->|"Save as drafts"| T10
    T10 --> T11
    T12 --> T10
    T13 --> T7
  end

  subgraph SY["System / Emails"]
    S1["Request approved automatically<br/>status Not started"]
    S2["Status: Awaiting internal review<br/>in-app alert to team leads and admins"]
    S3["Email and in-app alert to brand:<br/>idea approved"]
    S4["Email and in-app alert to brand:<br/>idea rejected, shows Rejected internally"]
    S5["In-app alert:<br/>Topic research assigned to you"]
    S6["Topics become Awaiting brand<br/>one combined email, in-app alert per topic"]
    S7["Brand's own topic accepted immediately"]
    S8["In-app alert to team leads, admins<br/>and assigned writer with decision and comment"]
    S9["Topic Accepted<br/>continues to blog flow"]
    S10["Topic Changes requested"]
    S11["Topic Rejected"]
    S7 --> S9
  end

  T1 --> S1
  T1b --> S1
  BR2 --> S2
  BR3 --> S7
  S1 --> T7
  S2 --> T2
  T4 --> S3
  T5 --> S4
  T6 --> S5
  S5 --> T7
  T9 -->|"Share straight away"| S6
  T11 --> S6
  S6 --> BR5
  BR6 --> S8
  BR7 --> S9
  BR8 --> S11
  BR9 --> S10
  S10 --> T12
  S11 --> T13
```

## Blog drafting and publishing

```mermaid
flowchart TD
  subgraph TL["Team Lead or Admin"]
    A0["Topic Accepted"]
    A1["Assign topic to a Content team writer"]
    A2["Paste Live link and click Publish<br/>needs accepted blog and live link"]
    A0 --> A1
  end

  subgraph WR["Content Team Writer"]
    W1["Start work once assigned"]
    W2["Add Content deck link<br/>optional image link, click Save"]
    W3["Status: Ready to share"]
    W4["Click Notify brand<br/>single or bulk"]
    W5["Update the deck<br/>click Re-share revision"]
    W1 --> W2
    W2 --> W3
    W3 --> W4
  end

  subgraph SY["System / Emails"]
    Y1["In-app alert to the writer"]
    Y2{"Topic accepted and<br/>deck link exists?"}
    Y3["Status: Awaiting brand<br/>one combined email with titles, in-app alert<br/>deck can now be opened"]
    Y4["In-app alert to team leads, admins and writer<br/>with the brand decision"]
    Y5["Status: Published<br/>in-app alert to team leads, admins, content team and brand<br/>no email"]
    Y6["Brand's Blog column links to live article"]
    Y5 --> Y6
  end

  subgraph BR["Brand User"]
    B1["Open the draft"]
    B2{"Brand decision"}
    B3["Accept"]
    B4["Request changes<br/>comment required"]
    B5["Reject<br/>comment required"]
    B6["Open published blog"]
    B1 --> B2
    B2 -->|"Accept"| B3
    B2 -->|"Request changes"| B4
    B2 -->|"Reject"| B5
  end

  A1 --> Y1
  Y1 --> W1
  W4 --> Y2
  Y2 -->|"No, cannot share yet"| W2
  Y2 -->|"Yes"| Y3
  Y3 --> B1
  B2 --> Y4
  B3 --> A2
  B4 --> W5
  B5 --> W5
  W5 --> Y3
  A2 --> Y5
  Y6 --> B6
```

## Status changes

Request status:

```mermaid
stateDiagram-v2
  state "Awaiting internal review" as AwaitingReview
  state "Rejected internally" as RejectedInternally
  state "Not started" as NotStarted
  [*] --> AwaitingReview : Brand suggests keywords
  [*] --> NotStarted : Internal request, approved automatically
  AwaitingReview --> NotStarted : Team Lead or Admin approves
  AwaitingReview --> RejectedInternally : Team Lead or Admin rejects with note
```

Topic status:

```mermaid
stateDiagram-v2
  state "Awaiting brand" as AwaitingBrand
  state "Changes requested" as ChangesRequested
  [*] --> Draft : Team creates topic
  [*] --> Accepted : Brand's own topic, accepted automatically
  Draft --> AwaitingBrand : Internal user clicks Notify brand
  AwaitingBrand --> Accepted : Brand approves
  AwaitingBrand --> Rejected : Brand rejects with comment
  AwaitingBrand --> ChangesRequested : Brand requests changes with comment
  ChangesRequested --> Draft : Team edits topic text
```

Blog status:

```mermaid
stateDiagram-v2
  state "Being written" as BeingWritten
  state "Ready to share" as ReadyToShare
  state "Awaiting brand" as AwaitingBrand
  state "Changes requested" as ChangesRequested
  [*] --> BeingWritten : Writer assigned and starts
  BeingWritten --> ReadyToShare : Writer saves the Content deck link
  ReadyToShare --> AwaitingBrand : Notify brand
  AwaitingBrand --> Accepted : Brand accepts
  AwaitingBrand --> ChangesRequested : Brand requests changes with comment
  AwaitingBrand --> Rejected : Brand rejects with comment
  ChangesRequested --> AwaitingBrand : Writer clicks Re-share revision
  Rejected --> AwaitingBrand : Writer clicks Re-share revision
  Accepted --> Published : Team Lead or Admin pastes Live link and publishes
```

## Key rules

- Internally raised requests are approved automatically. A brand keyword idea waits for internal review, and rejecting needs a note.
- Drafts are internal only. The brand sees a topic only after Notify brand.
- A brand's own topic is accepted immediately. A brand comment is required to reject or request changes.
- A blog cannot be shared until its topic is accepted and a content deck link exists. Publishing needs an accepted blog and a live link.
- Team members see only requests handed to them and topics assigned to them. Writers come only from the Content team.
- Publishing alerts the brand in-app but sends no email. The Deployment status rules do not apply to this page.
