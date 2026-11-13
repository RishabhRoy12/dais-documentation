# Analytics → Prompt Ranking
Route: `/analytics/prompt-ranking`

## Purpose
Tracks a fixed set of **prompts** (questions a buyer might ask an AI) and records whether the brand appears, per engine, week after week.

## Controls
Engine toggle **Gemini / ChatGPT** · scan-date columns (weekly, 07-Nov-2026 back to 18-May-2026).

## Layout

```mermaid
flowchart TB
  V["Current AI Visibility & Readiness<br/>Gemini Visibility % · ChatGPT Visibility %"]
  SUM["AI summary (BETA)<br/>'0% ranked coverage across 22 tracked prompts as of 07-Nov-2026'"]
  RA["RECOMMENDED ACTIONS<br/>VISIBILITY / RISK / GROWTH cards"]
  G["AI Rankings grid<br/># · Prompts · one column per weekly scan date"]
  V --> SUM --> RA --> G
```

## Architecture and data flow

```mermaid
flowchart LR
  subgraph Setup["Configuration (staff/Prompt Planner)"]
    PB[("prompts_brandwise<br/>tracked prompts per brand")]
    BM[("brand_model_config<br/>which engines per brand")]
  end
  subgraph Run["Weekly scan (backend, not visible)"]
    SCAN["Run each prompt on each engine"]
    WPR[("weekly_prompt_ranking<br/>brand_name, week, rank")]
  end
  SCAN --> WPR
  PB --> SCAN
  BM --> SCAN
  P["Prompt Ranking page"]
  P -->|"GET brand_model_config"| BM
  P -->|"GET prompts_brandwise"| PB
  P -->|"rpc get_prompt_selection_access"| ACC["permission: may user edit prompt selection"]
  P -->|"GET weekly_prompt_ranking order,limit"| WPR
  P -->|"fetch-prompt-visibility"| VIS["visibility % per engine"]
  P -->|"generate-page-insights"| INS["RECOMMENDED ACTIONS"]
```

## Sequence

```mermaid
sequenceDiagram
  actor U as User
  participant P as Page
  participant DB as Supabase
  participant F as Edge functions
  U->>P: open
  P->>DB: brand_model_config (which engines are enabled)
  P->>DB: prompts_brandwise (the 22 prompts)
  P->>DB: rpc get_prompt_selection_access(_brand_name)
  P->>DB: weekly_prompt_ranking (latest N weeks)
  P->>F: fetch-prompt-visibility
  F-->>P: Gemini % and ChatGPT %
  P->>F: generate-page-insights {page, brand, source, signals}
  F-->>P: summary + action cards
  P-->>U: headline %, cards, weekly grid
  U->>P: switch engine
  P-->>U: re-render grid for that engine
```

## Metric definitions
- **Visibility %** = prompts where the brand is ranked ÷ total tracked prompts, for the latest scan.
- **Ranked coverage** and "tracked prompts" (22) come from `prompts_brandwise`.
- Perplexity is mentioned in insights ("lack tracking data entirely") but has no toggle, so only Gemini and ChatGPT are scanned.

## Current state for the test brand
0% on both engines, all 22 prompts unranked. The insight cards correspondingly recommend seeding brand entities in third-party sources, categorising branded vs non-branded prompts, and so on.
