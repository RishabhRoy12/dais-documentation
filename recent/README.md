# DareAISearch Dashboard: Workflow & Architecture Pack

Source: live read-only crawl of `https://app.dareaisearch.com` (logged in as a client user, brand *Herbal Chakra*, Pro User), plus the app's JS bundle. Crawled 2026-11-12. No credentials are stored in this folder.

| # | File | What it shows |
|---|---|---|
| 01 | [system-architecture](01-system-architecture.md) | Component diagram: React PWA, Supabase, external sources, telemetry. Request patterns and brand scoping. |
| 02 | [sitemap-and-navigation](02-sitemap-and-navigation.md) | Sidebar mindmap, full route table including hidden routes, navigation flow. |
| 03 | [auth-and-user-flow](03-auth-and-user-flow.md) | Login sequence, roles, onboarding and subscription journey. |
| 04 | [analytics-data-flow](04-analytics-data-flow.md) | Page → edge function → source map, Overview and Brand Pulse flows, metric glossary. |
| 05 | [execution-workflow](05-execution-workflow.md) | The 17 execution pages, row lifecycle, blog pipeline, insight-to-execution loop. |
| 06 | [intelligence-and-content-workflows](06-intelligence-and-content-workflows.md) | Brand Voice, Prompt Planner, Blog/FAQ/YouTube tools, Publisher marketplace. |
| 07 | [backend-inventory](07-backend-inventory.md) | Every edge function, RPC and table observed. |
| 08 | [page-catalog](08-page-catalog.md) | Per-page headings, tabs, columns, calls, with screenshots. |
| 09 | [observations-and-gaps](09-observations-and-gaps.md) | Bugs, inconsistencies, coverage limits, follow-ups. |
| – | `screenshots/` | 42 full-viewport screenshots, one per page. |
| – | `data/crawl-raw.json` | Raw crawl output the catalog was generated from. |

Diagrams are Mermaid, so they render in GitHub, VS Code (Markdown Preview Mermaid Support extension) and most Markdown viewers.

## One-paragraph summary

DareAISearch is a React single-page app on Supabase. Clients land on an analytics suite that tracks how AI engines (ChatGPT, Gemini) mention and cite their brand, combined with GA4, Search Console and Semrush data. "Recommended Actions" panels turn that data into tasks. The DareAISearch team then executes those tasks in the Execution section (on-page fixes, content, and off-page citations), the client reviews and comments on each row, and results roll up into Scope of Work, the Activity Tracker and the Monthly Report.
