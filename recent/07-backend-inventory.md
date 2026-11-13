# 07 · Backend Inventory (Supabase)

Everything below was observed in network traffic or in the main JS bundle. The database schema itself was not inspected, so columns are not listed.

## Edge functions (`/functions/v1/…`)

| Group | Function | Request keys | Used by |
|---|---|---|---|
| Analytics | `fetch-ga4-analytics` | startDate, endDate, dateRange, brandOverride | Overview, Brand Pulse |
| | `fetch-search-console-data` | brand, startDate, endDate, rowLimit | Overview, Search Console |
| | `classify-branded-queries` | brand, queries | Search Console (branded vs non-branded) |
| | `fetch-keywords-ranking` | brandOverride | Overview, Keyword Ranking, Brand Pulse |
| | `fetch-improved-keywords` / `fetch-dropped-keywords` | brandOverride | Brand Pulse |
| | `fetch-prompt-weekly-summary` | | Overview |
| | `fetch-prompt-visibility` | | Prompt Ranking, Brand Pulse |
| | `fetch-searchscore-trend` | brandName | Brand Pulse |
| | `fetch-competitor-mentions` | brandName, dateRangeDays / startDate / endDate | Competitors, Brand Pulse |
| | `fetch-semrush-competitor-data`, `fetch-traffic-share-data`, `fetch-keywords-by-domain` | | Competitors |
| | `fetch-citation-data`, `fetch-sources-data` | startDate, endDate | Citations, Brand Pulse |
| | `fetch-concept-data`, `fetch-concept-by-brand` | | Concept Overview |
| | `fetch-reddit-overview` | | Reddit Overview |
| | `fetch-youtube-data` | | YouTube Analytics |
| | `fetch-product-leaderboard` | | Product Leaderboard |
| | `fetch-local-listings` | | Local Listings |
| | `fetch-activity-data` | | Activity Tracker |
| AI | `generate-page-insights` | page, brand, source, signals | Competitors, Prompt/Keyword Ranking, Citations |
| | `analytics-chat` | | Floating chat |
| Delivery | `fetch-execution-blogs` | brandOverride | Blogs, Brand Voice |
| | `fetch-scope-of-work` (GET) | brand | Scope of Work |
| | `fetch-monthly-reports` | | Monthly Report |
| | `manage-mom` | action, brand_name | Strategic Sync-ups |
| Staff (403 for client) | `import-<type>` ×9 | brand_name | Execution Shape B pages |
| | `send-<type>-review-email` ×9 | action, brand_name, month | Execution Shape B pages |
| Account | `google-oauth-url`, `disconnect-google` | | Google connect |
| | `trigger-welcome-email`, `send-bug-report`, `send-expert-inquiry`, `send-recharge-inquiry` | | onboarding / support |

`<type>` is one of: profile-citation, guest-post, web-two, online-communities, social-citation, classified, image-submission, directories, ppt-pdf (plus community-reviews, directories and others following the same pattern).

## RPC functions (`/rest/v1/rpc/…`)

`has_role`, `is_seo_team_member`, `is_schema_markup_manager`, `is_meta_tag_internal`, `current_user_brand_name`, `get_prompt_selection_access`, `get_keyword_selection_access`, `get_share_of_voice_window`, `get_blog_v2_brand_ref`, `notify_event`, `resolve_notifications`

## Tables read directly (`/rest/v1/…`)

| Domain | Tables |
|---|---|
| Identity & access | `profiles`, `user_roles`, `user_subscriptions`, `user_subscriptions_billing`, `subscription_payments`, `linked_user_accounts`, `sub_admin_brands`, `team_members`, `google_connections`, `growth_questionnaires` |
| Brands & tracking | `brands`, `brand_model_config`, `prompts_brandwise`, `weekly_prompt_ranking`, `citation_graph_data`, `search_scores` |
| Content | `blog_topic_generation_v2`, `blog_column_layouts`, `faq_results`, `youtube_intelligence_results`, `brand_voice_settings`, `brand_voices`, `brand_voice_source_docs`, `brand_voice_blogs`, `knowledge_articles`, `publisher_websites_public` |
| Execution | `execution_image_alt_records`, `execution_schema_markup_records`, `execution_internal_linking`, `execution_faq_suggestions`, `execution_youtube_records`, `youtube_column_layouts`, `meta_tag_items`, `meta_tag_column_layouts`, `meta_tag_notify_state`, plus the eleven off-page tables in doc 05 |
| Reporting | `monthly_report_submissions` |
| Platform | `notifications`, `chat_messages`, `user_sessions`, `user_page_sessions` |

## Third-party hosts contacted by the browser

`*.supabase.co` (backend), `l.clarity.ms` (Microsoft Clarity), `app.dareaisearch.com/__l5e/trackevents` (first-party telemetry). Semrush, GA4, GSC, Reddit and YouTube are reached only from edge functions, never from the browser.
