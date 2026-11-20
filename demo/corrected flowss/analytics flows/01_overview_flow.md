# Overview Flow

> Written for the **Overview** page (`/analytics/overview`, `doc analytics/01-overview.md`).

**Notation:** **AI Search traffic** = website sessions that come from AI platforms (ChatGPT, Perplexity, Gemini and similar). **Organic traffic** = sessions from traditional search engines (Google, Bing, Yahoo and others). A **scan date** = the week a ranking belongs to. The **property ID** = the ID that links the brand to its data in GA4.

**Goal:** the Overview page is a one-screen summary of the brand's performance. Most of its data is taken from **GA4**. A few tables (the landing-page tables) also show **Search Console (GSC)** data: Clicks, Impressions, CTR and Position. The two week-wise ranking tables are not taken from GA4: they read the **same stored data** as the **Prompt Ranking** and **Keyword Ranking** pages (not fetched again). Nobody types in or uploads data on the Overview page, and it keeps updating automatically.

| Data on the page | Source |
|------------------|--------|
| KPI card, AI Search traffic, Organic traffic, AI Search Decision Table, AI Search Discovery Table | **GA4**, using the **property ID** |
| GSC columns (Clicks, Impressions, CTR, Position) in the landing-page tables | **Search Console (GSC)** |
| Prompt Ranking Performance Week Wise (AI models per brand) | **Prompt Ranking** page data (see `../../flows/analytics flows/04_prompt_ranking_flow.md`) |
| Keyword Ranking Performance Week Wise | **Keyword Ranking** page data (see `../../flows/analytics flows/05_keyword_ranking_flow.md`) |

## Purpose and Access

The page shows:

1. **KPI card:** Active users, New users, Sessions, Key events, Revenue.
2. **AI insight line (BETA):** one sentence on the top AI platform's share of AI Search traffic.
3. **Analytics (AI Search):** line chart, bar chart by platform, session-source table, landing-page table and a BETA summary line.
4. **Analytics (Organic Traffic):** line chart, bar chart by source, session-source table, landing-page table and a BETA summary line.
5. **Prompt Ranking Performance Week Wise:** number of ranked prompts per week, with one toggle option per enabled AI model.
6. **Keyword Ranking Performance Week Wise:** number of keywords in Top 5, 10, 20, 50 and 100 per week.
7. **AI Search Decision Table** and **AI Search Discovery Table:** which AI platforms drive sessions and how users first discovered the brand.

The client can only view the page. The client can change the date preset and range, switch **Compare** on, search the landing pages, and pick the engine and dates in the prompt table. The client cannot add or change any data.

## In short

1. The brand is linked to its GA4 property ID (once).
2. The traffic blocks take their data from GA4.
3. The prompt table takes its data from the Prompt Ranking page data.
4. The keyword table takes its data from the Keyword Ranking page data.
5. The page updates automatically. The client picks the date range, and can compare it with the previous period.

## 1. Overall journey

```mermaid
flowchart TD
    P(["Brand is linked to its<br/>property ID"])
    P --> GA[("GA4<br/>website traffic data<br/>as per the property ID")]

    GSC[("Search Console (GSC)<br/>Clicks, Impressions, CTR, Position<br/>(landing-page tables only)")]
    PR[("Prompt Ranking page data<br/>weekly, AI models (per brand)<br/>(04_prompt_ranking_flow.md)")]
    KR[("Keyword Ranking page data<br/>weekly, by tier<br/>(05_keyword_ranking_flow.md)")]

    GA --> PG["Overview page"]
    GSC --> PG
    PR --> PG
    KR --> PG

    PG --> B1["KPI card<br/>users, sessions, key events, revenue<br/>(from GA4)"]
    PG --> B2["Analytics (AI Search)<br/>charts and tables<br/>(from GA4, GSC columns in landing-page table)"]
    PG --> B3["Analytics (Organic Traffic)<br/>charts and tables<br/>(from GA4, GSC columns in landing-page table)"]
    PG --> B4["AI Search Decision and Discovery tables<br/>(from GA4)"]
    PG --> B5["Prompt Ranking Performance Week Wise<br/>(from Prompt Ranking data)"]
    PG --> B6["Keyword Ranking Performance Week Wise<br/>(from Keyword Ranking data)"]

    B1 --> AI["System builds the AI insight line<br/>and the summary lines (BETA)"]
    B2 --> AI
    B3 --> AI
    AI --> PG

    PG --> M["Client picks date preset or range<br/>(Last 30 Days by default)<br/>and can turn Compare on"]
    M --> GA
    M --> GSC

    N["No fetching, typing or uploading"] -.-> PG

    classDef ext fill:#fff7e6,stroke:#d69e2e,color:#744210
    classDef stage fill:#eef6ff,stroke:#2b6cb0,color:#1a365d
    classDef done fill:#e6ffed,stroke:#2f855a,color:#22543d
    classDef ai fill:#f3e8ff,stroke:#7c3aed,color:#44337a
    classDef note fill:#f7fafc,stroke:#a0aec0,color:#2d3748
    class GA,GSC,PR,KR ext
    class PG stage
    class P done
    class AI ai
    class N note
```

## 2. Where each block comes from

```mermaid
flowchart LR
    subgraph G["GA4"]
        direction TB
        X1["KPI card"]
        X2["Analytics (AI Search)"]
        X3["Analytics (Organic Traffic)"]
        X4["AI Search Decision Table"]
        X5["AI Search Discovery Table"]
    end
    subgraph GS["Search Console (GSC)"]
        direction TB
        W1["GSC columns in the landing-page tables"]
    end
    subgraph PRP["Prompt Ranking page data"]
        direction TB
        Y1["Prompt Ranking Performance Week Wise"]
    end
    subgraph KRP["Keyword Ranking page data"]
        direction TB
        Z1["Keyword Ranking Performance Week Wise"]
    end
    G --> PAGE["Overview page"]
    GS --> PAGE
    PRP --> PAGE
    KRP --> PAGE
```

## System rules

- The **KPI card**, **AI Search**, **Organic Traffic**, **AI Search Decision Table** and **AI Search Discovery Table** are taken from **GA4**, using the brand's **property ID**.
- The landing-page tables also show **GSC** columns (Clicks, Impressions, CTR, Position), taken from Search Console. Only these tables have GSC columns; all other numbers are from GA4.
- The **Prompt Ranking Performance Week Wise** table reads the same stored data as the **Prompt Ranking** page (not fetched again): the number of ranked prompts per week, for the selected AI model (one of those enabled for the brand).
- The **Keyword Ranking Performance Week Wise** table reads the same stored data as the **Keyword Ranking** page (not fetched again): the number of keywords in Top 5, 10, 20, 50 and 100 per week. The tiers add up, so Top 100 is never lower than Top 5.
- GA4 sessions whose source is an AI platform (for example chatgpt.com, perplexity.ai, gemini.google.com) are shown as **AI Search**. Sessions from search engines are shown as **Organic**.
- The **date preset / range** (Last 7 Days, Last 15 Days, Last 30 Days, All Time, or a custom range) and **Compare** change the GA4 and GSC blocks only. The prompt and keyword tables are not compared and do not follow the date range.
- The **AI insight line** and the **summary lines** are generated by the System (BETA) from the GA4 data.
- If GA4 or the keyword data has not been collected yet, the page shows the banner **"No data collected yet"** with the status of Website analytics and Keyword ranking.
- The **NEW** tag in a landing-page table = the page got traffic in this period but not in the previous period of equal length.
- The data updates **automatically**. There is no manual add or upload on this page.
- The client cannot add or change any data.
- The data is **brand scoped**.

## Data and Storage

| Data | Source | Stored where | Notes |
|------|--------|--------------|-------|
| Brand ↔ property ID | Brand setup | Brand setup | Set once per brand |
| KPI card, AI Search, Organic, Decision and Discovery tables | GA4 | GA4 | Follows the date range and Compare |
| GSC columns in the landing-page tables | Search Console (GSC) | GSC | Clicks, Impressions, CTR, Position. Follows the date range |
| Prompt Ranking Performance Week Wise | Prompt Ranking page data | Same stored data as the Prompt Ranking page, as per `../../flows/analytics flows/04_prompt_ranking_flow.md` | Weekly, per enabled AI model. Does not follow the date range |
| Keyword Ranking Performance Week Wise | Keyword Ranking page data | Same stored data as the Keyword Ranking page, as per `../../flows/analytics flows/05_keyword_ranking_flow.md` | Weekly, by tier. Does not follow the date range |
| AI insight line and summary lines | System (generated) | Not stored | Built from the GA4 data |

Page details: `doc analytics/01-overview.md`.

## Runbook: Client

1. Open **Analytics → Overview**.
2. Pick the date preset or range. Turn **Compare** on to see the previous period.
3. Read the KPI card, then the AI Search and Organic blocks. Use the landing-page search to find a page.
4. Read the Prompt Ranking table (pick an enabled AI model, and the dates) and the Keyword Ranking table.
5. Read the Decision and Discovery tables to see which AI platforms drive and start the visits.

## Troubleshooting

| Situation | What to check |
|-----------|---------------|
| "No data collected yet" banner | See which chip says "Not collected": Website analytics (GA4) or Keyword ranking. |
| Traffic blocks are empty or zero | Check the brand's GA4 property ID and the date range. Key events and Revenue stay 0 if GA4 has no conversion or revenue event set up. |
| Prompt table is empty | The prompts may not have been given to Semrush yet, or no weekly data has come in. See `../../flows/analytics flows/04_prompt_ranking_flow.md`. |
| Keyword table is empty or old | Rankings are added on the Keyword Ranking page. See `../../flows/analytics flows/05_keyword_ranking_flow.md`. |
| Prompt or keyword numbers differ from the date range | Expected. These two tables follow weekly scan dates, not the date range. |
| Someone wants to upload data | Not needed and not done. |
