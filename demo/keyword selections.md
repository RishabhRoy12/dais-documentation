# Keyword Selection Process

**Notation:** X = keyword limit of the client's subscription package. Z = number of keyword suggestions the SEO team gives in one batch.

**Roles:** the **Client**, the **SEO team member** assigned to the client, and the **System**.

**Goal:** the process is complete only when exactly X unique keywords are approved for the client's Client ID and Subscription ID.

The process is shown in three diagrams: the overall journey, how a batch of keywords is reviewed, and how the system validates and counts approved keywords.

## 1. Overall journey

```mermaid
flowchart TD
    START([Start]) --> P1["Client selects a subscription package"]
    P1 --> P2["System assigns keyword limit X"]
    P2 --> S1["STAGE 1<br/>Assigned SEO member gives Z keyword suggestions"]
    S1 --> R1["Client reviews the suggestions<br/>(see diagram 2)"]
    R1 --> S2["STAGE 2<br/>Client may submit own keywords<br/>after ANY Stage 1 outcome"]
    S2 --> R2["SEO team reviews the client keywords<br/>(see diagram 2)"]
    R2 --> S3["STAGE 3<br/>System validates and counts approved keywords<br/>(see diagram 3)"]
    S3 --> Q{"Unique approved<br/>keywords = X ?"}
    Q -->|"Yes"| DONE([Keyword selection COMPLETED])
    Q -->|"No, fewer than X"| MORE{"Who adds more<br/>keywords?"}
    MORE -->|"Client suggests more"| S2
    MORE -->|"SEO member gives another set"| S1

    classDef stage fill:#eef6ff,stroke:#2b6cb0,color:#1a365d
    classDef decision fill:#fdf2f8,stroke:#b83280,color:#521b41
    classDef done fill:#e6ffed,stroke:#2f855a,color:#22543d
    class S1,S2,S3 stage
    class Q,MORE decision
    class DONE done
```

## 2. How a batch of keywords is reviewed (Stage 1 and Stage 2)

The same three outcomes apply in both stages. Only the reviewer changes.

| Stage | Keywords come from | Reviewer |
|---|---|---|
| Stage 1 | Assigned SEO team member | **Client** |
| Stage 2 | Client | **SEO team** |

```mermaid
flowchart TD
    B["A batch of suggested keywords"] --> RV{"Reviewer decides<br/>(Client in Stage 1,<br/>SEO team in Stage 2)"}

    RV -->|"Case 1: reject ALL"| C1["Reviewer gives ONE common remark"]
    RV -->|"Case 2: approve some,<br/>reject the rest"| C2["Reviewer gives ONE common remark<br/>for the rejected keywords"]
    RV -->|"Case 3: approve ALL"| C3["No remark needed"]

    C1 --> REJ[("REJECTED KEYWORDS<br/>stored with the common remark<br/>no limit, not counted")]
    C2 --> REJ
    C2 --> VAL["Approved keywords go to<br/>system validation (diagram 3)"]
    C3 --> VAL

    classDef store fill:#fff7e6,stroke:#d69e2e,color:#744210
    classDef decision fill:#fdf2f8,stroke:#b83280,color:#521b41
    class REJ store
    class RV decision
```

Notes:
- Case 1 ends with nothing approved, so the count stays the same.
- Stage 1 and Stage 2 have the same cases, but in Stage 2 the order is approve all, approve and reject in bulk, reject all. The logic is identical.

## 3. Validation and count check (Stage 3)

This runs every time keywords are approved.

```mermaid
flowchart TD
    A["Approved keywords arrive"] --> V1["1. Check for duplicates"]
    V1 --> V2["2. Check free slots<br/>under package limit X"]
    V2 --> V3["3. Save ONLY unique approved keywords<br/>that fit in the remaining slots"]
    V3 --> APP[("APPROVED KEYWORDS<br/>unique only, maximum X<br/>per Client ID + Subscription ID")]
    APP --> F["System fetches the approved keywords"]
    F --> CNT["System counts unique approved keywords<br/>for this Client ID + Subscription ID"]
    CNT --> CMP{"Count compared<br/>with X"}
    CMP -->|"count = X"| DONE([Keyword selection COMPLETED])
    CMP -->|"count < X"| MORE["Slots still free.<br/>Repeat suggestions:<br/>Option A: client submits more keywords (SEO team reviews)<br/>Option B: SEO member gives another set (client reviews)"]
    MORE --> LOOP(["Back to review (diagram 2)"])

    classDef store fill:#fff7e6,stroke:#d69e2e,color:#744210
    classDef decision fill:#fdf2f8,stroke:#b83280,color:#521b41
    classDef done fill:#e6ffed,stroke:#2f855a,color:#22543d
    class APP store
    class CMP decision
    class DONE done
```

## Keyword storage

| Storage section | Data stored | Storage limit |
|---|---|---|
| Approved Keywords | Unique approved keywords | Maximum X keywords |
| Rejected Keywords | Rejected keywords with their common rejection remark | No limit |

## System rules

- Approved keywords are stored against the respective **Client ID** and **Subscription ID**.
- Duplicate keywords are never counted twice.
- Rejected keywords are stored separately, with their remarks, and do not count towards the approved total.
- The system checks the available slots before saving approved keywords.
- The client can submit their own suggestions after the initial SEO suggestions, whether they approved or rejected the initial ones.
- The assigned SEO team member keeps providing suggestions whenever required.
- The process ends only when X unique keywords have been approved.
