# Competitors Intelligence Flow

## 1. Overall journey

```mermaid
flowchart TD
    P(["Brand is linked to its<br/>property ID"])
    P --> S["Semrush API<br/>data fetched as per the property ID"]
    S --> GA[("GA4<br/>holds the data that came from Semrush")]

    TM["Admin or assigned SEO team member<br/>provides and updates the Sheet<br/>every month"] --> SH[("Sheet (one per brand)<br/>competitor domain data")]

    GA --> PG["Competitors Intelligence page"]
    SH -->|"read directly"| PG
    SH -.->|"no Sheet for the brand"| ND["Sheet blocks + AI insight<br/>show No data available"]

    PG --> B1["Share of Voice<br/>AI models (per brand)<br/>(from GA4 / Semrush)"]
    PG --> B2["Brand's Mention in AI Indexed Sources<br/>AI models (per brand)<br/>(from GA4 / Semrush)"]
    PG --> B3["Authority Score<br/>(from Sheet)"]
    PG --> B4["Domain by Traffic share<br/>(from Sheet)"]
    PG --> B5["Branded and Non-branded Keywords by Domain<br/>(from Sheet)"]

    B1 --> AI["System generates<br/>AI insight line + RECOMMENDED ACTIONS"]
    B2 --> AI
    B3 --> AI
    B4 --> AI
    AI --> PG

    PG --> NEXT["Semrush blocks: updated automatically<br/>Semrush → GA4 → page"]
    NEXT --> S

    N["No fetching, typing or uploading of<br/>Semrush data"] -.-> GA

    classDef ext fill:#fff7e6,stroke:#d69e2e,color:#744210
    classDef stage fill:#eef6ff,stroke:#2b6cb0,color:#1a365d
    classDef done fill:#e6ffed,stroke:#2f855a,color:#22543d
    classDef ai fill:#f3e8ff,stroke:#7c3aed,color:#44337a
    classDef note fill:#f7fafc,stroke:#a0aec0,color:#2d3748
    class S,GA,SH ext
    class PG stage
    class P done
    class AI ai
    class N,TM,ND note
```

## 2. Where each block comes from

```mermaid
flowchart LR
    subgraph SEM["Semrush → GA4"]
        direction TB
        X1["Share of Voice<br/>AI models (per brand)"]
        X2["Brand's Mention in AI Indexed Sources<br/>AI models (per brand)"]
    end
    subgraph SHT["Brand's Sheet (Admin or assigned SEO, monthly, read directly)"]
        direction TB
        Y1["Authority Score"]
        Y2["Domain by Traffic share"]
        Y3["Branded Keywords and<br/>Non-branded Keywords by Domain"]
    end
    subgraph GEN["System (AI)"]
        direction TB
        Z1["AI insight line"]
        Z2["RECOMMENDED ACTIONS"]
    end
    SEM --> PAGE["Competitors Intelligence page"]
    SHT --> PAGE
    SEM --> GEN
    SHT --> GEN
    GEN --> PAGE
```

