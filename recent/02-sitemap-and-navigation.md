# 02 · Sitemap & Navigation

## Sidebar as seen by the logged-in Pro user

```mermaid
mindmap
  root((DareAISearch))
    Home
      Brand Pulse
    Analytics
      Overview
      Search Console
      Competitors Intelligence
      Prompt Ranking
      Keyword Ranking
      Citation Overview
      Concept Overview
      Reddit Overview
      YouTube Analytics
      Product Leaderboard
      Local Listings
      Activity Tracker
      Strategic Sync-ups
    Intelligence
      Brand Voice
      Prompt Planner (BETA)
      Blog Generator
      FAQ Creator
      YouTube Intelligence
      Publisher Intelligence
    Execution
      Content
        Blogs
        Meta Tags
        Image Alt
        Schema Markup
        Internal Linking
        FAQ Suggestion
        YouTube
      Off-page / Citations
        Profile Citation
        Guest Post
        Web 2.0
        Listing in Online Communities
        Social Citation
        Classified
        Reddit/Quora
        Image Submission
        Directories
        PPT/PDF Submission
        Reviews on Online Communities
    Deliverables
      Scope of Work
    Reporting
      Monthly Report
    Learn
      Insightful Blogs
      Interactive Webinars
```

Header bar: brand switcher (Herbal Chakra), light/dark toggle, notifications bell, avatar. Footer: plan badges (*Pro User*, *DAIS Growth*), **Sign out**. A floating sparkle button opens the AI chat (`analytics-chat`).

## Full route table (from the JS router)

Routes marked **hidden** exist in the router but were not in this user's sidebar. They are probably role-gated or legacy. This is an inference, not confirmed.

| Group | Routes |
|---|---|
| Public / auth | `/`, `/auth`, `/reset-password`, `*` (404) |
| Onboarding & billing | `/questionnaire`, `/growth/questionnaire`, `/growth/plan`, `/growth/checkout`, `/growth/thank-you`, `/subscription`, `/subscription/checkout`, `/subscription/success`, `/trial-dashboard` |
| Home | `/dashboard`, `/brand-pulse` |
| Analytics (visible) | `/analytics/overview`, `console-insights`, `competitors`, `prompt-ranking`, `keyword-ranking`, `citations`, `concepts`, `reddit-overview`, `youtube`, `product-leaderboard`, `local-listings`, `activity`, `brand-mom`, `prompt-research` |
| Analytics (**hidden**) | `/analytics/citation-overview`, `/analytics/citation-leaderboard`, `/analytics/overall-performance` |
| Intelligence (visible) | `/intelligence/brand-voice`, `/blog-generator-v2`, `/faq-generator`, `/youtube-intelligence`, `/intelligence` (Publisher) |
| Intelligence (**hidden**) | `/blog-generator` (v1), `/prompt-generator`, `/intelligence/competitor-research`, `/intelligence/dais-crawler`, `/intelligence/dais-crawler-v2`, `/intelligence/dais-crawler/report/:jobId`, `/intelligence/recommendations`, `/intelligence/visibility-overview`, `/hdie`, `/hdie/backfill`, `/hdie/intelligence` |
| Execution (visible) | 17 pages, see doc 05 |
| Execution (**hidden**) | `/execution/broken-links`, `/execution/heading-tags`, `/execution/robots-txt`, `/execution/sitemap`, `/execution/meta-tags-new` |
| Deliverables / reporting | `/deliverables`, `/deliverables/scope-of-work`, `/scope-of-work`, `/reporting/monthly` |
| Learn | `/insightful-blogs`, `/interactive-webinars` |
| Notifications | `/notifications` |
| **Admin (hidden)** | `/admin/users`, `/admin/brand-delivery`, `/admin/task-manager`, `/admin/internal-mom`, `/admin/notifications`, `/admin/knowledge-base`, `/admin/citation-intelligence`, `/admin/data-check`, `/admin/backfill-tracker`, `/admin/semrush-integration`, `/admin/user-flow`, `/admin/youtube-overview` |

## Navigation flow

```mermaid
flowchart TD
  A["Open any URL"] --> B{"Session?"}
  B -- no --> AUTH["/auth"]
  B -- yes --> C["getDefaultLandingRoute()<br/>(role / plan based)"]
  AUTH -- "sign in" --> C
  C --> D["/analytics/overview (observed landing)"]
  D --> H["Home: /brand-pulse"]
  D --> AN["Analytics group"]
  D --> IN["Intelligence group"]
  D --> EX["Execution group"]
  D --> DL["Deliverables / Reporting"]
  D --> LN["Learn"]
  H -- "Where to Focus Next" --> AN
  AN -- "RECOMMENDED ACTIONS" --> EX
```
