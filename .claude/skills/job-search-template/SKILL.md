---
name: job-search
description: |
  Exhaustive job search for {{target_roles}} at {{focus_domain}}. Use when the user asks to "run a job search", "find new jobs", "search for roles", or "what's out there". Searches multiple job boards, filters against the user's specific criteria, researches company fit, and outputs qualified opportunities.
---

# Job Search Skill

Run an exhaustive search for roles matching the user's criteria. Location is always **{{target_locations}}**.

## Reference Files

Read these skill references for detailed instructions:

- [Search Sources](./references/search-sources.md) — All job board queries and discovery searches
- [Scoring & Fit](./references/scoring-and-fit.md) — Search criteria, scoring rubrics, fit signals, user background
- [Verification Guide](./references/verification-guide.md) — How to verify links and maintain the database
- [Output Format](./references/output-format.md) — Templates for search results and file updates
- [Target Companies](./references/target-companies.md) — Tiered company list and skip list

## Context Files (Load Before Starting)

1. `Search/{{search_year}}/CLAUDE.md` — Search criteria, preferences, workflow rules
2. `Search/{{search_year}}/DASHBOARD.md` — Active pipeline (what's already being pursued)
3. `Search/{{search_year}}/companies/prospects.md` — Full prospects database
4. `Search/{{search_year}}/searches/overview.md` — Past search history
5. `.claude/skills/job-search/references/target-companies.md` — Target companies and skip list

---

## Step 0: First-Run Detection

After loading context files, check whether this is the first time the skill has been run:

1. Read `Search/{{search_year}}/searches/overview.md`
2. If the search history table is empty (no rows, or contains "_No searches run yet_"), this is a **first run**.

**On first run, present this overview before starting the search:**

> **First time running `/job-search` — here's how it works.**
>
> This skill searches across multiple job boards, scores every role against your criteria, and maintains a ranked pipeline. Here's what happens:
>
> **What it searches:**
> [List all sources from `references/search-sources.md` — present them as a clean bulleted list organized by category: ATS boards, aggregators, domain-specific boards, location boards, VC portfolios, company career pages, discovery searches]
>
> **How it works:**
> 1. Three parallel agents search different source categories simultaneously
> 2. Results are consolidated, deduplicated, and scored against your criteria
> 3. Roles are tiered (Tier 1 = strong match, Tier 2 = good match, Tier 3 = watch list)
> 4. Your prospects database and dashboard are updated automatically
> 5. A single dated search results file captures everything found
>
> **Your criteria:** [summarize from Search CLAUDE.md — target roles, locations, comp range, must-haves]
>
> **Your custom boards:** [list any role-specific or user-added boards from search-sources.md Section L]
>
> Each search run builds on previous ones — verified roles are tracked, closed postings are noted, and your pipeline grows over time. Run it weekly for best results.
>
> **Does this look right?** Before I start searching, let me know:
> - Are these criteria still accurate? (roles, location, comp, must-haves)
> - Any job boards you want me to add or skip?
> - Any companies you want to add to the Watch List or Skip list?
> - Good to go?

**Wait for the user to confirm before proceeding.** If they request changes:
- **Criteria changes** → update `Search/{{search_year}}/CLAUDE.md` and `references/scoring-and-fit.md`
- **Board changes** → update `references/search-sources.md` (Section G for role-specific, Section L for custom)
- **Company changes** → update `references/target-companies.md`

After confirmation (or on subsequent runs where this overview is skipped), proceed to Step 1.

---

## Execution: Parallel Agents

This skill spawns 3 parallel agents, then consolidates results.

### Step 1: Load Context

Read all context files listed above to understand current state.

### Step 2: Spawn Three Parallel Agents

Launch ALL three agents simultaneously using the Task tool:

---

**CRITICAL: Agents must NOT create or modify any files.** Each agent returns a structured report only. All file creation and updates happen in Step 3 (consolidation), performed by the main skill runner. This prevents duplicate files and ensures a single consolidated output.

---

**Agent A — "Verify Existing Data"**

Spawn a Task subagent (subagent_type: "general-purpose") with this prompt:

> **IMPORTANT: Do NOT create, write, or modify any files. Only return your findings as a structured report.**
>
> You are verifying the user's job search database. Read these files:
> - `Search/{{search_year}}/DASHBOARD.md` (active pipeline)
> - `Search/{{search_year}}/companies/prospects.md` (prospects database)
> - `.claude/skills/job-search/references/verification-guide.md` (verification procedures)
> - `.claude/skills/job-search/references/target-companies.md` (skip list)
>
> Do the following:
> 1. **Verify Active Pipeline**: For each role in the Active Pipeline table, WebFetch the company careers page or ATS link. Confirm the role is still open. Flag any that have gone stale (no movement in 2+ weeks).
> 2. **Verify High Interest Prospects**: For every role in prospects.md → High Interest, WebFetch the application link. If dead → note for Closed. If live → note as "Verified Open" with today's date.
> 3. **Spot-Check Medium Interest**: Verify roles marked ⚠️ Unverified.
> 4. **Check Watch List Companies**: Visit career pages of Watch List companies. Note any new relevant roles.
> 5. **Report**: Return a structured summary:
>    - Pipeline roles: X/Y confirmed still active, list any concerns
>    - High Interest: X verified open, Y to close, any comp/location changes
>    - Medium Interest: X verified, Y to close
>    - Watch List: Any new roles found at watched companies
>    - Full details for each role checked (status, date, notes)

---

**Agent B — "Search ATS Boards + Target Company Careers"**

These are the highest-value, most reliable sources. Spawn a Task subagent (subagent_type: "general-purpose") with this prompt:

> **IMPORTANT: Do NOT create, write, or modify any files. Only return your findings as a structured report.**
>
> You are searching for new job opportunities for the user on ATS boards and target company career pages. Read these files:
> - `.claude/skills/job-search/references/search-sources.md` (search queries — focus on sections A, J, K)
> - `.claude/skills/job-search/references/scoring-and-fit.md` (criteria and scoring)
> - `.claude/skills/job-search/references/target-companies.md` (target companies + skip list)
> - `Search/{{search_year}}/DASHBOARD.md` (active pipeline — don't duplicate these)
> - `Search/{{search_year}}/companies/prospects.md` (existing prospects — don't duplicate these)
>
> **Your scope — ATS boards + target company career pages:**
> 1. **Search ATS boards** (Section A in search-sources.md): Greenhouse, Lever, Ashby — use ALL title variations from the Search Titles list.
> 2. **Check Tier 1 + Tier 2 company career pages** (Section J): Visit career pages for every Tier 1 and Tier 2 company in target-companies.md.
> 3. **Check VC portfolio boards** (Section I).
> 4. **Extract data**: For every role found, capture: Company, Title, Salary, Location/In-Office, Link, relevance notes, Source.
> 5. **Filter**: Apply disqualifiers from scoring-and-fit.md. Deduplicate.
> 6. **Score**: Rate remaining roles 1-5 on each dimension in the scoring rubric.
> 7. **Research top candidates** (4+ average): Company fit, liquidity, location, product reception.
> 8. **Verify Tier 1 links**: WebFetch every link for strong-match roles.
> 9. **Report**: Return results organized as Tier 1 / Tier 2 / Tier 3 / Needs Verification / Confirmed Closed / Disqualified.

---

**Agent C — "Search Aggregators, Discovery & Specialty Boards"**

Broader net across aggregators and niche sources. Spawn a Task subagent (subagent_type: "general-purpose") with this prompt:

> **IMPORTANT: Do NOT create, write, or modify any files. Only return your findings as a structured report.**
>
> You are searching for new job opportunities for the user across aggregator boards and specialty sources. Read these files:
> - `.claude/skills/job-search/references/search-sources.md` (search queries — focus on sections B through H, K, and Phase 2 discovery)
> - `.claude/skills/job-search/references/scoring-and-fit.md` (criteria and scoring)
> - `.claude/skills/job-search/references/target-companies.md` (skip list)
> - `Search/{{search_year}}/DASHBOARD.md` (active pipeline — don't duplicate these)
> - `Search/{{search_year}}/companies/prospects.md` (existing prospects — don't duplicate these)
>
> **Your scope — aggregators, discovery, and specialty boards:**
> 1. **Discover new companies** (Phase 2 in search-sources.md): Search for recently funded companies in the user's focus domain. Cross-reference against target-companies.md.
> 2. **Search Built In {{primary_location}}** (Section B): All title variations.
> 3. **Search LinkedIn Jobs** (Section C): Supplement only, unreliable.
> 4. **Search HN "Who's Hiring"** (Section D): Most recent thread.
> 5. **Search YC Jobs** (Section E).
> 6. **Search domain-specific boards** (Section F).
> 7. **Search remote + design boards** (Section G).
> 8. **Search location-specific boards** (Section H).
> 9. **General web search** (Section K): Broad title searches.
> 10. **Extract, filter, score**: Same process as other agent — extract data, apply disqualifiers, deduplicate, score.
> 11. **Note new companies discovered**: List any companies not in target-companies.md that look promising.
> 12. **Report**: Return results organized as Tier 1 / Tier 2 / Tier 3 / New Companies Discovered / Confirmed Closed / Disqualified.

---

### Step 3: Consolidate & Re-Tier (Single File Output)

Once all three agents return, **you** (the main skill runner) consolidate everything into **one** search results file. The agents should not have created any files — if they did, merge their content and remove duplicates.

1. **Apply verification results** from Agent A to update the current database picture
2. **Merge new finds** from Agents B and C:
   - Deduplicate across agents (same role found by both → keep best link)
   - Cross-reference against existing data (don't duplicate active pipeline or existing prospects)
3. **Re-tier the full opportunity set** — look at ALL open roles and produce a fresh ranking:
   - Consider: fit score, verification status, time sensitivity, comp, team/culture signals
   - Flag roles that moved UP or DOWN in tier since last search (and why)
   - Note newly discovered roles
4. **Call out the user's top 3-5 opportunities** across everything — what should they spend energy on right now?

### Step 4: Update Files

Follow the update procedures in [Output Format](./references/output-format.md):

1. Save search results to `Search/{{search_year}}/searches/YYYY-MM-DD.md`
2. Update `Search/{{search_year}}/companies/prospects.md` (add new, close dead, update dates)
3. Update "Last job search" in `Search/{{search_year}}/CLAUDE.md`
4. Update "Last updated" in `Search/{{search_year}}/DASHBOARD.md`
5. Add summary row to `Search/{{search_year}}/searches/overview.md`

### Step 5: Present Results

Summarize in conversation:
- Verification results (what closed, what's still active)
- New finds worth noting
- The re-tiered top opportunities
- Recommended next actions
