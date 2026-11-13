# Analytics → Concept Overview
Route: `/analytics/concepts`

## Purpose
Shows **which topics ("concepts") AI answers associate with the brand** and the **sentiment** of those mentions, aggregated and per competitor brand.

## Controls
Engine (ChatGPT) · month selector (July 2026) · sentiment legend Positive / Neutral / Negative.

## Layout

```mermaid
flowchart TB
  A["Concepts Aggregated – ChatGPT (July 2026)<br/>Concept · Mentions · Positive · Neutral · Negative"]
  B["Concepts by Brand (2026-09-14)<br/>Concept × brand matrix: Baidyanath, Dabur, Himalaya, Patanjali Ayurved, herbal chakra"]
  A --> B
```

## Concept hierarchy
Concept names are **hierarchical paths joined by `__`**, e.g.

```
manufacturing services
└─ manufacturing services__contract & private-label
   ├─ ...__contract manufacturing
   └─ ...__private label
finished product categories
└─ finished product categories__supplements & nutraceuticals
   ├─ ...__herbal supplements
   └─ ...__capsules
regulatory compliance & certifications
└─ ...__gmp
   └─ ...__gmp certification
```

```mermaid
flowchart LR
  L1["Level 1<br/>finished product categories<br/>manufacturing services<br/>regulatory compliance<br/>ingredients & sourcing"] --> L2["Level 2<br/>e.g. supplements & nutraceuticals<br/>contract & private-label"] --> L3["Level 3<br/>e.g. herbal supplements<br/>private label"]
```

Parents' mention counts roll up their children (5 for "finished product categories" vs 4 for its child).

## Architecture and data flow

```mermaid
sequenceDiagram
  actor U as User
  participant P as Concept Overview
  participant A as fetch-concept-data
  participant B as fetch-concept-by-brand
  participant DB as Supabase
  U->>P: open
  P->>A: aggregate concepts for brand
  A->>DB: concept extraction results (from AI answers)
  A-->>P: concept, mentions, pos/neu/neg counts
  P->>B: per-brand concept matrix
  B-->>P: concept × brand mentions
  P-->>U: two tables
  U->>P: change month/engine
  P->>A: re-query
```

```mermaid
flowchart LR
  ANS["AI answers to tracked prompts"] --> EXT["LLM concept + sentiment extraction<br/>(offline pipeline, inferred)"] --> TAX["Concept taxonomy paths"] --> DB[("concept tables")] --> F["fetch-concept-*"] --> UI["Concept Overview"]
```

## Notes
- Two different dates: aggregated view is **July 2026** (monthly), per-brand view is a **2026-09-14** snapshot. Staleness vs. today is the same reporting-lag issue noted in [../09-observations-and-gaps.md](../09-observations-and-gaps.md).
- Use: pick concepts competitors own but the brand lacks, then target them in blogs, FAQs and schema.
- Extraction pipeline is not visible in the browser, so the diagram above is an inference from the data shape.
