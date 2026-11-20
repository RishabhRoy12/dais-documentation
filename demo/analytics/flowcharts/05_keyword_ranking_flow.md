# Keywords Ranking Flow

## 1. Overall journey

```mermaid
flowchart TD
    START([Start]) --> Q1{"Is the client new<br/>or already set up?"}

    Q1 -->|"New client"| KS["Keyword selection process<br/>client approves keywords<br/>(see keyword selections.md)"]
    Q1 -->|"Existing client"| CHK{"Has the client already<br/>approved X keywords?"}

    KS --> CHK
    CHK -->|"No, fewer than X"| KS
    CHK -->|"Yes, exactly X"| ADD["Add button (above the date selector) becomes available<br/>to the assigned SEO member or Admin"]

    ADD --> M{"How are the rankings added<br/>(every Monday)?"}
    M -->|"Method A"| MA["Add rankings manually<br/>keyword by keyword<br/>(see diagram 2)"]
    M -->|"Method B"| MB["Upload a CSV file<br/>(see diagram 2)"]

    MA --> SAVE["System saves the rankings"]
    MB --> SAVE
    SAVE --> UPD["Keyword Ranking page is updated<br/>(see diagram 3)"]
    UPD --> END([End])

    classDef stage fill:#eef6ff,stroke:#2b6cb0,color:#1a365d
    classDef decision fill:#fdf2f8,stroke:#b83280,color:#521b41
    classDef done fill:#e6ffed,stroke:#2f855a,color:#22543d
    class KS,ADD,MA,MB,SAVE,UPD stage
    class Q1,CHK,M decision
    class END done
```

Plain reading:

- **A new client** always starts with keyword selection. Keywords must be approved first, and the process repeats until exactly X are approved.
- **An existing client** who has already approved X keywords skips keyword selection and goes straight to adding rankings.
- **Only the assigned SEO team member or the Admin adds the rankings.** The client cannot add rankings. The client only sees the result on their Keyword Ranking page.
- **Rankings are updated every Monday**, by either method, by the assigned SEO member or the Admin.
- Rankings are added only once X keywords are approved, because the rankings belong to those approved keywords.

## 2. The two ways of adding rankings

```mermaid
flowchart TD
    BTN["Every Monday: assigned SEO member or Admin<br/>clicks the Add button (above the date selector)<br/>hidden or disabled until X keywords are approved"] --> CH{"Choose a method"}

    CH -->|"Method A: manual"| A1["Pick the scan date<br/>(the Monday of the update)"]
    A1 --> A2["Enter the rank of each approved keyword<br/>one by one"]
    A2 --> A3["Keyword not ranking?<br/>leave it as Not in Rank"]
    A3 --> A4["Save"]

    CH -->|"Method B: CSV upload"| B1["Prepare the CSV file<br/>keywords and their ranks for ONE scan date<br/>(one file per date)"]
    B1 --> B2["Upload the CSV file"]
    B2 --> B3{"System checks the file"}
    B3 -->|"File is valid"| B4["Rows are read and matched to the approved keywords<br/>rows for keywords NOT approved are skipped"]
    B3 -->|"File has problems"| B5["Upload is refused<br/>user corrects the file and uploads again"]
    B5 --> B1

    A4 --> SAVE["System saves the rankings<br/>per brand, per keyword, per scan date<br/>(a rank for an existing scan date is overwritten)"]
    B4 --> SAVE

    classDef decision fill:#fdf2f8,stroke:#b83280,color:#521b41
    classDef store fill:#fff7e6,stroke:#d69e2e,color:#744210
    class CH,B3 decision
    class SAVE store
```

| | Method A: Manual | Method B: CSV upload |
|---|---|---|
| Best for | A few keywords, or a quick correction | Many keywords at once |
| How | Enter the rank of each keyword in the page | Upload one file with all the ranks for one scan date (one file per date); rows for non-approved keywords are skipped |
| Result | Same: the rankings are saved for the scan date | Same: the rankings are saved for the scan date |
| Done by | The assigned SEO member or Admin | The assigned SEO member or Admin |
| When | Every Monday | Every Monday |

## 3. After the rankings are saved

```mermaid
flowchart TD
    S["Rankings saved<br/>per keyword and scan date"] --> R1[("Ranking store")]
    R1 --> P1["Client's Keyword Ranking page reads the data<br/>the next time it opens or reloads"]

    P1 --> U1["Five tier cards<br/>Top 5 / 10 / 20 / 50 / 100<br/>for the chosen scan date (default latest)"]
    P1 --> U2["Keyword Performance Week Wise table<br/>new scan date appears as a column"]
    P1 --> U3["AI insight line and RECOMMENDED ACTIONS (BETA)<br/>always latest scan vs previous scan"]

    classDef store fill:#fff7e6,stroke:#d69e2e,color:#744210
    class R1 store
```

- The new scan date is added to the top-right scan-date dropdown (newest first) and becomes a column in the week-wise table. The latest date is the default for the five cards and the default sort column (ascending, unranked **-** last).
- The scan-date dropdown changes **only the five cards**. The table columns are chosen with the "{n} of {total} dates" multi-select (default all; Clear keeps the latest). The insight and actions never follow the dropdown.
- Tier values are cumulative (Top 5 <= Top 10 <= ... <= Top 100 <= total tracked keywords). Unranked keywords count in no tier.
- The insight and actions come from `generate-page-insights` and are regenerated on each load (wording, number of cards, category VISIBILITY / GROWTH / RISK and priority HIGH / MEDIUM can differ). They are read-only.
- Data is read through `POST fetch-keywords-ranking` (empty body, brand from the session). The page has no search, pagination or export.
- A keyword with no rank for a scan date shows **-**. (The stored value `Not in Rank` is not stated in the page doc.)

