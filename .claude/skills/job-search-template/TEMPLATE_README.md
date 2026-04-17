# job-search-template

> **This is a template, not a working skill.** It lives here so that `/onboard` can use it as the base for generating a customized `job-search` skill tailored to the user's search criteria.

## How it's used

During `/onboard`, after the goals interview, the onboarding skill:

1. Collects the user's search criteria (target roles, comp, locations, must-haves, industries to avoid, target companies, skip list).
2. Hands off to `skill-creator` with:
   - This template folder as the base
   - The user's answers as the substitution values for `{{placeholders}}`
3. `skill-creator` generates a real `.claude/skills/job-search/` folder with the substitutions applied.

## Placeholders used

The template files reference these placeholder tokens — all must be supplied to skill-creator:

| Token | Example value |
|---|---|
| `{{target_roles}}` | "Staff+ Product Designer, Design Leadership" |
| `{{target_locations}}` | "NYC + Remote US" |
| `{{primary_location}}` | "NYC" |
| `{{target_comp_range}}` | "$250K+ base" |
| `{{must_haves}}` | "AI-native company, senior IC impact, strong comp" |
| `{{industries_to_avoid}}` | "Crypto/Web3, Adtech, Defense/Gov" |
| `{{skip_list_companies}}` | "Coinbase, Palantir, ..." |
| `{{focus_domain}}` | "AI / AI-native companies" |
| `{{user_background_summary}}` | Short paragraph describing the user's experience and strengths |
| `{{search_year}}` | "2026" (current search cycle) |

## Files in this template

- `SKILL.md` — Main skill entry
- `references/scoring-and-fit.md` — Scoring rubric and disqualifiers
- `references/search-sources.md` — Job board queries
- `references/target-companies.md` — Starter target-companies template (mostly empty, user fills in)
- `references/output-format.md` — Templates for search result files
- `references/verification-guide.md` — Link verification procedures (mostly generic)

## Manual invocation

If you want to customize the job-search skill yourself without going through `/onboard`:

1. Copy this folder to `.claude/skills/job-search/`
2. Replace all `{{placeholder}}` tokens with your values
3. Fill in `references/target-companies.md` with your target companies
4. Remove this `TEMPLATE_README.md` from the copy
