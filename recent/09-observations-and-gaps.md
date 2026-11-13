# 09 · Observations, Risks & Gaps

Findings from the crawl, kept separate from the architecture docs so facts and judgement don't mix.

## Confirmed in the live app

1. **Empty states** for the test brand (Herbal Chakra): YouTube Analytics ("No Videos Yet"), Product Leaderboard, Local Listings, Strategic Sync-ups ("No meetings yet"). Overview shows a banner "No data collected yet: Website analytics / Keyword ranking: Not collected" even though GA4 numbers render below it. The banner and data disagree.
2. **HTTP 500** from `GET execution_social_citation_records` on `/execution/social-citation`. That page showed no table.
3. **HTTP 403** from every `import-*` and `send-*-review-email` function when called as a client. If the client UI is meant never to call them, they should be skipped for client roles; today each page load fires them and fails.
4. **Stale data labels:** Competitors "Authority Score Last updated: July 2026" while the data is November 2026. Concepts shows "Mentions (July 2026)" and "Concepts by Brand (2026-09-14)". Reporting shows "July 2026", so months have gaps.
5. **Duplicate calls:** Competitors calls `fetch-competitor-mentions` three times with different parameters, and `fetch-keywords-ranking` and `fetch-prompt-visibility` are called from several pages with no shared cache.
6. **Mixed route naming:** `/analytics/citations` is in the sidebar while `/analytics/citation-overview` also exists. Two blog generators (`/blog-generator`, `/blog-generator-v2`) and two meta-tag pages (`meta-tags`, `meta-tags-new`) coexist.
7. **`/analytics/prompt-research`** (Prompt Planner) made no calls on load, so its data path is unknown until a user runs a search.

## Not covered (be aware)

- Only the **client** role was tested. Admin and internal pages were not visited, and the permission matrix in doc 03 is inferred from RPC and route names.
- Lazy-loaded JS chunks were not parsed, so some tables and functions used only on interaction are missing from doc 07.
- No write actions were performed (no approvals, comments, imports or generation), so row status values and generation request/response shapes are unobserved.
- Database column definitions and RLS policies were not read, only what the REST layer exposes.

## Suggested follow-ups

| Priority | Action |
|---|---|
| High | Fix the 500 on `execution_social_citation_records` |
| High | Gate `import-*` / `send-*-review-email` by role on the client so they are not called as clients |
| Medium | Reconcile the "No data collected yet" banner with live GA4 data |
| Medium | Share fetches (React Query cache key by brand + range) so Brand Pulse and the analytics pages don't repeat them |
| Low | Retire the legacy duplicate routes or redirect them |
| Next | Repeat the crawl with an admin account to document `/admin/*`, `/hdie`, and `/intelligence/dais-crawler*` |
