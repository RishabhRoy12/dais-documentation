# Global Layout (shared by all Analytics pages)

Every page under `/analytics/*` renders inside the same application shell: a **top bar**, a **left sidebar**, a **breadcrumb + page header**, and a floating **AI assistant** button. Page docs link here instead of repeating this content.

> Verified on the live app (dark theme default). Brand name, user initial, plan badges and notification content depend on the logged-in user and the selected brand.

---

## 1. Top bar

| Element | Type | Behaviour |
|---|---|---|
| Sidebar toggle | Icon button (panel icon), far left | Collapses the sidebar to an icon-only rail (about 47 px wide); click again to expand. Sidebar tooltip/label: "Toggle Sidebar" |
| DARE AI SEARCH logo | Logo | Branding only |
| Brand chip | Avatar (brand initial) + brand name | Shows the active brand. Clicking it does not open a menu for this account |
| Theme switch | Toggle switch with sun and moon icons (`aria-label` "Toggle theme") | Switches between dark (default) and light theme; applies the `light` class on the root element |
| Notifications | Bell icon button | Opens a popover (see 1.1) |
| User avatar | Round button with user initial | Opens the user menu (see 1.2) |

### 1.1 Notifications popover
| Element | Text / behaviour |
|---|---|
| Title | Notifications |
| Action link | Mark all read |
| Empty state | "You're all caught up." |
| Footer link | View all notifications |

The page loads the user's unresolved notifications on start (`notifications` table, filtered by `user_id` and `resolved_at`, ordered, limited).

### 1.2 User menu
| Item | Icon | Purpose |
|---|---|---|
| Profile | Person | User profile |
| Subscription Options | Card | Plan and subscription management |
| Wallet | Wallet | Wallet / credits |
| Sign out | Exit arrow | Ends the session |

---

## 2. Left sidebar

Collapsible groups with section labels in small caps. The active page is highlighted (teal text, teal indicator bar on the left edge).

| Group | Items |
|---|---|
| (top) | **Home** |
| **ANALYTICS** | Overview · Search Console · Competitors Intelligence · Prompt Ranking · Keyword Ranking · Citation Overview · Concept Overview · Reddit Overview · YouTube Analytics · Product Leaderboard · Local Listings · Activity Tracker · Strategic Sync-ups |
| **INTELLIGENCE** | Brand Voice · Prompt Planner (**BETA** badge) · Blog Generator · FAQ Creator · YouTube Intelligence · Publisher Intelligence |
| **DEPLOYMENT** | *Owned Channels:* Blogs · Meta Tags · Image Alt · Schema Markup · Internal Linking · FAQ Suggestion<br>*Controlled Channels:* YouTube<br>*Third Party Channels:* Profile Citation · Guest Post · Web 2.0 · Listing in Online Communities · Social Citation · Classified · Reddit/Quora · Image Submission · Directories · PPT/PDF Submission · Reviews on Online Communities<br>Scope of Work |
| **REPORTING** | Monthly Report |
| **KNOWLEDGE BASE** | Insightful Blogs · Interactive Webinars |
| Footer badges | **Pro User** (plan badge) · **DAIS Growth** (tier badge) |
| Footer action | **Sign out** |

Each menu item has a leading icon. In the collapsed rail only the icons are shown.

---

## 3. Breadcrumb and page header

| Element | Behaviour |
|---|---|
| Breadcrumb | `DareAISearch › {Brand} › Analytics › {Page}`; the current page is bold and not a link |
| Page title and subtitle | Left side, below the breadcrumb |
| Controls (right side) | Page-specific filters (on Overview: Compare toggle, date preset, date picker) |

---

## 4. Floating AI assistant ("Miss Daring")

| Element | Details |
|---|---|
| Launcher | Round teal button with a sparkle icon, fixed at the bottom-right of every page |
| Panel header | **Miss Daring** with a **BETA** badge; subtitle "AI Search Intelligence Partner"; helper text "Ask me what changed, why it matters, and what your brand should do next." |
| Intro block | "Meet Miss Daring. Your AI Search Intelligence Partner." Description: "I help you understand what changed, why it matters, and what your brand should do next across AI search." |
| Suggested questions (clickable chips) | What changed in my AI visibility this week? · Why did our sentiment change? · Which prompts should we prioritize next? · Which competitors are being recommended above us? · Which citations are helping or hurting us? · Summarize this month's AI Search performance. · What should we execute next? · Where are we visible but not preferred? |
| Footer note | "Miss Daring · grounded in your brand's database records" |

---

## 5. Calls made on every page load

These run for every authenticated page (Supabase REST and RPC):

| Call | Purpose |
|---|---|
| `GET AUTH user` | Current session user |
| `GET user_subscriptions` (select `user_id`) | Subscription / plan check |
| `GET profiles` (select `user_id`) | Profile |
| `POST rpc/has_role` (`_user_id`, `_role`) | Role check |
| `POST rpc/is_seo_team_member` | Whether the user is an SEO Team member |
| `POST rpc/is_schema_markup_manager` | Schema-markup manager permission |
| `GET linked_user_accounts` (select `user_id`) | Linked accounts |
| `GET notifications` (select `user_id`, `resolved_at`, order, limit) | Bell popover data |
