# 03 · Authentication, Roles & User Journey

## Login sequence (observed)

```mermaid
sequenceDiagram
  autonumber
  actor U as User
  participant S as SPA
  participant A as Supabase Auth
  participant R as PostgREST / RPC
  U->>S: open /analytics/overview
  S->>S: no session, redirect to /auth
  U->>S: email + password, Sign In
  S->>A: POST /auth/v1/token (password grant)
  A-->>S: access + refresh token
  S->>A: GET /auth/v1/user
  par bootstrap
    S->>R: GET profiles
    S->>R: GET user_roles
    S->>R: rpc has_role
    S->>R: rpc is_seo_team_member
    S->>R: rpc is_schema_markup_manager
    S->>R: GET user_subscriptions
    S->>R: GET linked_user_accounts
    S->>R: GET notifications
  end
  S->>R: POST user_sessions (session start)
  S-->>U: land on /analytics/overview
  loop every page view
    S->>R: POST user_page_sessions
  end
```

Alternative entries: **Continue with Google**, **Create one** (sign up), **Forgot password** (`/reset-password`), and **Reset session** (clears a stuck session).

## Roles and permissions

| Role / check | Source | Effect |
|---|---|---|
| `admin` | `has_role(_role:'admin')` | Admin console (`/admin/*`) and all brands |
| `internal_team` | `has_role` | Staff tools, brand override |
| `sub_admin` | `has_role` + `sub_admin_brands` | Manages a specific set of brands |
| SEO team member | `is_seo_team_member()` | Edit rights on execution records |
| Schema markup manager | `is_schema_markup_manager()` | Schema Markup editing |
| Normal client user | default | Read access to own brand, can comment and approve on execution rows |

The roles above come from the bundle and RPC names. The mapping of role to page is inferred, and only the client view was tested.

```mermaid
flowchart TD
  L["Login"] --> R{"Role check<br/>has_role / user_roles"}
  R -- admin --> AD["Admin console + all brands"]
  R -- internal_team --> IT["Staff tools + brandOverride"]
  R -- sub_admin --> SA["Assigned brands via sub_admin_brands"]
  R -- client --> CL["Own brand only"]
  CL --> SUB{"user_subscriptions"}
  SUB -- trial --> TR["/trial-dashboard"]
  SUB -- paid --> PR["Full app (Pro User / DAIS Growth)"]
  SUB -- none --> OB["/questionnaire, /growth/plan, /subscription"]
```

## Client onboarding / subscription journey

```mermaid
flowchart LR
  A["Sign up"] --> B["/questionnaire<br/>growth_questionnaires"]
  B --> C["/growth/plan"]
  C --> D["/growth/checkout"]
  D --> E["/growth/thank-you"]
  E --> F["Dashboard"]
  F -.-> G["/subscription (upgrade)"]
  G --> H["/subscription/checkout"]
  H --> I["/subscription/success"]
  I --> F
  F -. "Connect Google" .-> J["google-oauth-url → google_connections<br/>(enables GA4 + Search Console)"]
```

Pre-auth values (`preAuthBrandName`, `preAuthName`, `preAuthWebsiteUrl`) are held in localStorage so the brand a visitor typed before signing up carries into onboarding.

## Typical daily client journey

```mermaid
journey
  title Client using the dashboard
  section Check
    Open Brand Pulse: 5: Client
    Read Key Movements: 4: Client
  section Diagnose
    Review Prompt Ranking: 4: Client
    Check Competitors and Citations: 4: Client
  section Act
    Open RECOMMENDED ACTIONS: 4: Client
    Generate blog or FAQ: 3: Client
  section Track
    Review Execution status and comment: 3: Client
    Read Monthly Report: 4: Client
```
