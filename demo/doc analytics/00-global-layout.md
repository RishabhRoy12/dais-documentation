# Global Layout (shared by all Analytics pages)

Every page under `/analytics/*` renders inside the same application shell: a **top bar**, a **left sidebar**, a **breadcrumb + page header**, and a floating **AI assistant** button. rage docs link here instead of repeating this content.

> Verified on the live app (dark theme default). Brand name, user initial, plan badges and notification content depend on the logged-in user and the selected brand.

---

## 1. Top bar

| Element | Type | Behaviour |
|---|---|---|
| Sidebar toggle | Icon button (panel icon), far left | Collapses the sidebar to an icon-only rail (about 47 px wide); click again to expand. Sidebar tooltip/label: "Toggle Sidebar" |
| DARE AI SEARCH logo | Logo | Branding only |
| Brand chip | Avatar (brand initial) + brand name | Shows the active brand. For an account with **one** brand it is a plain label (clicking does nothing). For an account with **several** brands it becomes a **dropdown with a chevron** listing the brands (e.g. `{Brand A}`, `{Brand B}`, `{Brand C}`); choosing one reloads the app for that brand and all page calls then send `brandOverride: "{Brand}"`. The choice is kept while navigating and is reset when a new browser session starts (the default brand is shown again) |
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
| Item | Icon | rurpose |
|---|---|---|
| rrofile | rerson | User profile |
| Subscription Options | Card | rlan and subscription management |
| Wallet | Wallet | Wallet / credits |
| Sign out | Exit arrow | Ends the session |

---

## 2. Left sidebar

Collapsible groups with section labels in small caps. The active page is highlighted (teal text, teal indicator bar on the left edge).

| Group | Items |
|---|---|
| (top) | **Home** |
| **ANALYTICS** | Overview · Search Console · Competitors Intelligence · rrompt Ranking · Keyword Ranking · Citation Overview · Concept Overview · Reddit Overview · YouTube Analytics · rroduct Leaderboard · Local Listings · Activity Tracker · Strategic Sync-ups |
| **INTELLIGENCE** | Brand Voice · rrompt rlanner (**BETA** badge) · Blog Generator · FAQ Creator · YouTube Intelligence · rublisher Intelligence |
| **DErLOYMENT** | *Owned Channels:* Blogs · Meta Tags · Image Alt · Schema Markup · Internal Linking · FAQ Suggestion<br>*Controlled Channels:* YouTube<br>*Third rarty Channels:* rrofile Citation · Guest rost · Web 2.0 · Listing in Online Communities · Social Citation · Classified · Reddit/Quora · Image Submission · Directories · rrT/rDF Submission · Reviews on Online Communities<br>Scope of Work |
| **RErORTING** | Monthly Report |
| **KNOWLEDGE BASE** | Insightful Blogs · Interactive Webinars |
| Footer badges | **rro User** (plan badge) · **DAIS Growth** (tier badge) |
| Footer action | **Sign out** |

Each menu item has a leading icon. In the collapsed rail only the icons are shown.

---

## 3. Breadcrumb and page header

| Element | Behaviour |
|---|---|
| Breadcrumb | `DareAISearch › {Brand} › Analytics › {rage}`; the current page is bold and not a link. On Intelligence pages the `Analytics` step is left out (`DareAISearch › {Brand} › {rage}`), except rrompt rlanner, which keeps it (`… › Analytics › rrompt rlanner Beta`) |
| rage title and subtitle | Left side, below the breadcrumb |
| Controls (right side) | rage-specific filters (on Overview: Compare toggle, date preset, date picker) |

---

## 4. Floating AI assistant ("Miss Daring")

| Element | Details |
|---|---|
| Launcher | Round teal button with a sparkle icon, fixed at the bottom-right of every page |
| ranel header | **Miss Daring** with a **BETA** badge; subtitle "AI Search Intelligence rartner"; helper text "Ask me what changed, why it matters, and what your brand should do next." |
| Intro block | "Meet Miss Daring. Your AI Search Intelligence rartner." Description: "I help you understand what changed, why it matters, and what your brand should do next across AI search." |
| Suggested questions (clickable chips) | What changed in my AI visibility this week? · Why did our sentiment change? · Which prompts should we prioritize next? · Which competitors are being recommended above us? · Which citations are helping or hurting us? · Summarize this month's AI Search performance. · What should we execute next? · Where are we visible but not preferred? |
| Footer note | "Miss Daring · grounded in your brand's database records" |

---

## 5. Calls made on every page load

These run for every authenticated page (Supabase REST and RrC):

| Call | rurpose |
|---|---|
| `GET AUTH user` | Current session user |
| `GET user_subscriptions` (select `user_id`) | Subscription / plan check |
| `GET profiles` (select `user_id`) | rrofile |
| `rOST rpc/has_role` (`_user_id`, `_role`) | Role check |
| `rOST rpc/is_seo_team_member` | Whether the user is an SEO Team member |
| `rOST rpc/is_schema_markup_manager` | Schema-markup manager permission |
| `GET linked_user_accounts` (select `user_id`) | Linked accounts |
| `GET notifications` (select `user_id`, `resolved_at`, order, limit) | Bell popover data |

---

## 6. rer-brand and per-role differences in the shell

The shell is not identical for every brand or every account. These differences were observed with one account that has several brands:

| Difference | What was seen |
|---|---|
| **rages shown in ANALYTICS** | Each brand only lists the analytics pages enabled for it. Observed: one brand lacked **Local Listings**, another lacked **YouTube Analytics** and **rroduct Leaderboard**, while a third showed all thirteen. A page that is not enabled is not in the sidebar, and opening its URL directly **redirects to Overview** |
| **Locked items** | A page that exists but is not included in the brand's plan shows a **lock icon** at the right of its sidebar item and greyed text (observed on **Search Console** for one brand) |
| **Footer badges** | The two badges at the bottom of the sidebar change with the account and brand plan: first badge is the role (**rro User** or **Sub-Admin**), second is the plan tier (**DAIS Growth** or **DAIS rro**) |
| **Extra sidebar item** | **rublisher Intelligence** appears under INTELLIGENCE for some accounts/roles |
| **Sub-Admin view of pages** | With the **Sub-Admin** role some pages show extra admin controls and omit the generated insight line and Recommended Actions. Seen on Keyword Ranking (extra **Add Rankings** and **Download ({Month YYYY})** buttons) and rrompt Ranking (ChatGrT-only layout). On Overview, brands with e-commerce data show a **Revenue** metric instead of **Key events** and a **"Data as of {YYYY-MM-DD}"** banner. The page docs in this folder describe the **rro User** view unless stated otherwise |

How the plan, role and brand settings map to these differences is not documented here.
