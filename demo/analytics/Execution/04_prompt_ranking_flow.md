# Prompt Ranking Flow

**Notation:** X1 = prompt limit of the client's subscription package. A **scan date** = the week the rankings belong to. **Visibility** = how often the brand appears in an AI model's answers to the client's prompts, shown for each AI model enabled for the brand (for example ChatGPT, Gemini, Perplexity).

**Roles:** the **Client**, the **Assigned SEO team member**, the **Admin**, the **System**, and **Semrush**.

**Starting point:** this flow begins when prompt selection is **Completed**, meaning the client has approved exactly X1 unique prompts and they are locked. How the prompts are selected is in `../../prompt selections.md`.

**Goal:** the assigned SEO team member or the Admin gives the final approved prompts to **Semrush manually**. The platform has asked Semrush to fetch the rankings **every Saturday**, so the data in the Prompt Ranking section is **updated automatically every week** following Semrush's Saturday fetch, and the client sees their visibility on each AI model enabled for the brand. Nobody has to fetch or type in the data.

## Purpose and Access

Prompt ranking (`/analytics/prompt-ranking`, Analytics sidebar group, 4th item) shows the client how their brand appears when AI models enabled for the brand answer the client's approved prompts. The page has three parts:

1. **Current AI Visibility & Readiness:** one Visibility % card per enabled AI model.
2. **AI insight line and RECOMMENDED ACTIONS** (both marked BETA): generated from the latest scan.
3. **AI Rankings:** a "{n} prompts" count, a model toggle (one tab per enabled model) and a rank grid with one row per tracked prompt and one column per weekly scan date. Each cell is the brand's rank position (1 is best) or **-** (not ranked).

- The client sees Prompt Ranking data only after payment and after prompt selection is completed and the prompts are given to Semrush.
- The client can only view the page. The client cannot add or change any ranking data. The page has no date filter, compare toggle, search, pagination or export.

## In short

1. **Receive:** the final approved prompts (X1, locked) come from the prompt selection flow.
2. **Give to Semrush:** the assigned SEO team member or the Admin gives those approved prompts to Semrush **manually**, once. They are not imported automatically and the client does not type them in.
3. **Automatic weekly update:** the data in Prompt Ranking is updated automatically every week, following Semrush's fetch on Saturdays (as the platform requested). The team member or Admin does **not** fetch or type in any data.
4. **See:** the client sees visibility cards for each enabled AI model, a week-wise rank grid (model toggle, sortable date columns), and the AI insight and recommended actions on the Prompt Ranking page.

## System rules

- Prompts are given to Semrush only after **X1** prompts are approved. Rejected prompts are never given to Semrush.
- The **assigned SEO team member or the Admin** gives the approved prompts to Semrush **manually**. They are not imported automatically and the client cannot give or type them.
- The prompts are given to Semrush once, and the same prompts are used every week.
- The data in Prompt Ranking is **updated automatically every week** following Semrush's fetch. The platform asked Semrush to fetch every Saturday, and the scan dates seen in the live app are Saturdays.
- **There is no role for the team member or the Admin in fetching, typing in or uploading the ranking data.** Their only action is giving the prompts to Semrush.
- The page shows visibility for **each AI model enabled for the brand** (set in `brand_model_config`). If no value is available for a model, the page shows `0.00%` for it.
- The client cannot add or change any ranking data.
- **Model toggle:** switching tabs changes only the rank values in the grid (filtered by the `model` field of `weekly_prompt_ranking`). The visibility cards and the generated text do not change. The first enabled model is active by default.
- **Cell values:** a number is the brand's rank position in that model's answer for that prompt on that date (1 is best); **-** means not ranked. A column that is **-** in every cell means no ranking for any prompt in that scan.
- **Sorting:** clicking a date header offers Sort Ascending (1→10) or Sort Descending (10→1). It is done in the browser, one column at a time, unranked rows (-) always stay at the bottom, and row numbers move with their rows.
- **Insight and actions:** the insight line and the action cards (category RISK or VISIBILITY, priority HIGH or MEDIUM) are generated again on every load, so wording, number of cards, categories and priorities can differ for the same data. They are read-only. "Ranked coverage" = ranked prompts divided by tracked prompts for the latest scan date.

## Roles and Scope

| Role | What they can do | What they cannot do |
|------|------------------|---------------------|
| **Client** | View the Prompt Ranking page | Cannot give prompts to Semrush. Cannot add or change ranking data. |
| **Assigned SEO team member** | Give the final approved prompts to Semrush manually | Does not fetch or type in ranking data. |
| **Admin** | Same as the assigned SEO team member for any client | Same limits |
| **System** | Show the automatically updated rankings on the page, build the insight and actions on each page load | – |
| **Semrush** | Holds the prompts given to it, fetches their rankings every Saturday (as the platform requested), and the rankings are updated automatically in the Prompt Ranking section | – |

## Data and Storage

| Data | Stored where | Notes |
|------|--------------|-------|
| Approved prompts (input) | `prompts_brandwise` in the page docs | From the prompt selection flow, X1 unique prompts, locked |
| Prompts at the source | Semrush | Given manually by the assigned SEO member or Admin |
| Prompt rankings | Platform store (`weekly_prompt_ranking`: `model`, `date`, `ranking`; `monthly_percentage` is named as an insight source in the page docs) | Updated automatically, per prompt, per enabled AI model, per scan date |
| Model availability | `brand_model_config` | Which AI models are enabled for the brand |
| Visibility % cards | `fetch-prompt-visibility` | Brand taken from the session |
| Insight and actions | Not stored (`generate-page-insights`) | Generated again on every page load from the latest scan figures |

## Checked in the live app

The Prompt Ranking page was opened for one brand (Pro User view) and its calls were recorded. This confirms these points:

| Finding | What it shows |
|---------|---------------|
| Scan dates are **Saturdays**, seven days apart (for example 14-Nov-2026, 07-Nov-2026, 31-Oct-2026, back to 23-May-2026) | The weekly cadence. The very first date seen, 18-May-2026, is a Monday. |
| The page shows the models switched on for the brand in `brand_model_config`. For this brand: ChatGPT on, Gemini on, Perplexity off, AI Overview off (one example; other brands can have Perplexity or others on) | The models shown depend on the brand's setup. |
| `get_prompt_selection_access` returns `max_prompts` (X1, **75** for this brand), `is_paid`, `questionnaire_completed`, `has_proposal_rows`, `has_ranking_rows`, `eligible` and `prompts_finalized` | The prompt limit, the payment rule, and whether prompt selection is completed. |
| The tracked prompt list comes from `prompts_brandwise` (22 prompts for this brand) | The approved prompts are what the page tracks. |
| `weekly_prompt_ranking` (`model`, `date`, `ranking`) supplies the grid values: a rank number such as 1 to 5, or empty (shown as -), for each prompt on each scan date | The page shows a grid with a value for each prompt on each scan date. |
| `fetch-prompt-visibility` supplies the "Visibility %" cards for each enabled model | The percentage shown on the cards. |
| `generate-page-insights` (page `PromptRanking`) supplies the insight line and action cards; `user_page_sessions` records page usage | Generated content and usage tracking. |
| The page has **no button or screen** for adding or uploading ranking data, and **Semrush is not mentioned** in the page or its calls | Consistent with the rankings being updated automatically in the background, with no action by the client. Admin screens were not visible to this account, so they were not checked. |

## Runbook: Assigned SEO Team Member (and Admin)

1. Wait until prompt selection is **Completed** (X1 unique approved prompts).
2. Give the final approved prompts to Semrush manually, once.
3. That is the last manual step. The rankings are then updated automatically every week in the Prompt Ranking section. **Do not fetch or type in any ranking data.**

## Runbook: Client

1. Finish prompt selection (see `../../prompt selections.md`).
2. Open **Analytics → Prompt Ranking** to see your visibility on each enabled AI model.
3. Use the model tabs to switch the grid between models, and click a date header to sort by rank.
4. The page updates automatically every week. A new scan date appears as a new column in the grid.

## Troubleshooting

| Situation | What to check |
|-----------|---------------|
| Nothing to give to Semrush | The client may not have approved X1 prompts yet. Finish prompt selection. |
| No rankings show on the Prompt Ranking page | Check that the approved prompts were given to Semrush. If they were, the update is automatic and there is nothing for the team to fetch. |
| A model shows `0.00%` visibility | No value is available for that model, or the value is really 0. |
| Insight or actions read differently after a refresh | By design. They are AI-generated on every load. |
| Every cell in a date column is - | No ranking for any prompt in that scan. |
| Someone wants to type in or upload rankings | Not needed and not done. Rankings are updated automatically. |
| The client cannot add data | By design. The client cannot add or change ranking data. |
