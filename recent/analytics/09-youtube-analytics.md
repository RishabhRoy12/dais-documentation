# Analytics → YouTube Analytics
Route: `/analytics/youtube`

## Purpose
Performance of YouTube videos produced for the brand (views, engagement), tracked from a team-maintained **tracking sheet**.

## Current state
Empty: **"No Videos Yet. YouTube video data will appear here once videos are added to the tracking sheet."** The page only showed this empty state, so the populated layout (charts, columns) was not observed.

## Architecture and data flow

```mermaid
flowchart LR
  TS["Tracking sheet<br/>(video URLs added by team)"] --> F["fetch-youtube-data"]
  F -.->|"likely"| YT["YouTube Data API"]
  F --> P["YouTube Analytics page"]
  P --> E{"Any videos?"}
  E -- no --> EMPTY["Empty state: 'No Videos Yet'"]
  E -- yes --> VIEW["Video table / charts (not observed)"]
```

```mermaid
sequenceDiagram
  actor U as User
  participant P as Page
  participant F as fetch-youtube-data
  U->>P: open
  P->>F: brand context
  F-->>P: { videos: [] }
  P-->>U: No Videos Yet
```

## Where the videos come from
Execution → YouTube (`execution_youtube_records`) holds optimised title, description, tags, file and thumbnail names, first comment, playlist and **Video URL**. Once a Video URL is added to the tracking sheet it should appear here. This link between the two pages is an inference.

```mermaid
flowchart LR
  A["Intelligence → YouTube Intelligence<br/>(ideas / optimisation)"] --> B["Execution → YouTube<br/>(optimised metadata, Video URL)"] --> C["Tracking sheet"] --> D["Analytics → YouTube"]
```

## Related
`/admin/youtube-overview` exists (staff view, not tested).
