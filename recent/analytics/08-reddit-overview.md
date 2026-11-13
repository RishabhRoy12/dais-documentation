# Analytics → Reddit Overview
Route: `/analytics/reddit-overview` · Subtitle: "Subreddit impact and trending Reddit threads for your brand"

## Purpose
Reddit threads and subreddits that AI engines draw on for the tracked prompts, so the team knows where to participate.

## Controls
Engine (ChatGPT) · date/snapshot selector (2026-09-21).

## Layout

```mermaid
flowchart TB
  SI["Subreddit Impact<br/>Subreddit · Link · Prompts · Visibility · Threads · Citations"]
  TH["Threads<br/>Thread · Thread URL (click to open) · Subreddit · Prompts"]
  SI --> TH
```

Sample rows: `r/ayurvedabeauty` (1 prompt, 50% visibility, 1 thread, 1 citation) and `r/u_ayurvedic1223`.

## Architecture and data flow

```mermaid
sequenceDiagram
  actor U as User
  participant P as Reddit Overview
  participant F as fetch-reddit-overview
  participant DB as Supabase
  U->>P: open
  P->>F: brand + engine + date
  F->>DB: Reddit citations extracted from AI answers
  F-->>P: subreddit aggregates + thread list
  P-->>U: two tables
  U->>P: click thread link
  P-->>U: opens reddit.com in new tab
```

```mermaid
flowchart LR
  PR["Tracked prompts"] --> AI["AI engine answers"] --> URL["Cited URLs"] --> FILT["Filter reddit.com"] --> AGG["Group by subreddit / thread"] --> UI["Reddit Overview"]
  UI -. "opportunity" .-> EX["Execution: Reddit/Quora"]
```

## Definitions
- **Prompts**: number of tracked prompts whose answers cited that subreddit.
- **Visibility**: share of those prompts where the brand was also mentioned (50% = 1 of 2).
- **Threads / Citations**: distinct threads and total times they were cited.

## Notes
- The listed threads are old (2022-era IDs) and not about the brand's category specifically, so this feeds target selection, not brand mentions.
- Links to the Execution → Reddit/Quora page (Question, Answer, Live Link) where answers are written.
