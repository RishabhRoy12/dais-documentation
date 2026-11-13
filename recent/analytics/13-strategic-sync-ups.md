# Analytics → Strategic Sync-ups
Route: `/analytics/brand-mom` · Subtitle: "AI-powered Minutes of Meeting. Extract tasks, decisions & summaries automatically"

## Purpose
Meeting notes (Minutes of Meeting, "MoM") for the brand, where AI turns a transcript or notes into **summary, decisions and tasks**.

## Current state
"No meetings yet. Create your first AI-powered meeting notes to get started." with a **New Meeting** button. The New Meeting form and a populated list were not opened (write action, so not exercised).

## Architecture and data flow

```mermaid
flowchart LR
  P["Strategic Sync-ups page"]
  P -->|"GET sub_admin_brands (brand_name)"| SB[("sub_admin_brands")]
  P -->|"POST {action, brand_name}"| M["manage-mom edge function"]
  M --> DB[("meeting records")]
  M -. "AI extraction" .-> LLM["LLM: summary, decisions, tasks"]
```

```mermaid
sequenceDiagram
  actor U as User
  participant P as Page
  participant M as manage-mom
  U->>P: open
  P->>M: {action: "list", brand_name} (action name inferred)
  M-->>P: []
  P-->>U: empty state
  U->>P: New Meeting
  P->>M: {action: "create", notes/transcript} (inferred)
  M->>M: AI extracts summary, decisions, tasks
  M-->>P: saved meeting
  P-->>U: meeting card with extracted items
```

## Meeting lifecycle (inferred)

```mermaid
stateDiagram-v2
  [*] --> Empty
  Empty --> Draft: New Meeting
  Draft --> Processed: AI extraction
  Processed --> Reviewed: user edits
  Reviewed --> Shared: visible to brand
  Shared --> [*]
```

## Notes
- `sub_admin_brands` is read here, so sub-admins likely see meetings across the brands they manage.
- A separate staff page `/admin/internal-mom` exists in the router for internal meetings.
- Action names (`list`, `create`) and states above are inferred, since only the page-load call `manage-mom {action, brand_name}` was captured.
