# Scoring & Fit Criteria

Search criteria, scoring rubrics, fit signals, and user background for role assessment.

---

## Hard Requirements

- **Role:** {{target_roles}}
- **Comp:** {{target_comp_range}}
- **Location:** {{target_locations}}
- **Industries to EXCLUDE:** {{industries_to_avoid}}

## Location Rules (STRICT — Non-Negotiable)

- Fully remote US roles: ALWAYS qualify (unless user specified otherwise)
- Hybrid/in-office roles: MUST have a {{primary_location}} office
- Any other city (unless explicitly in `{{target_locations}}`) = **immediate disqualifier**
- When a posting lists multiple offices, verify {{primary_location}} is a real option
- A company having a {{primary_location}} office doesn't mean this specific role is available there — check the posting itself
- If location is ambiguous, check the company's office locations before including

## Immediate Disqualifiers

- Company in an excluded industry: {{industries_to_avoid}}
- Comp below the user's floor
- No US/remote option (unless user allows international)
- Hybrid/in-office NOT in a target location
- Company is on the "Companies to SKIP" list in `target-companies.md`
- Company is on the "Not Interested" list in `prospects.md`
- Role level below the user's minimum (see `{{target_roles}}`)

---

## Scoring Rubric (1-5 Each)

| Dimension | 1 (Low) | 3 (Mid) | 5 (High) |
|-----------|---------|---------|----------|
| **Domain fit** | Outside the user's focus domain | Adjacent to focus domain | Core to `{{focus_domain}}` |
| **Leadership signal** | No public direction on this domain | Some engagement | Leadership actively evangelizing the domain |
| **Liquidity** | Early stage, no path | Late stage, possible IPO | Public company or imminent IPO |
| **Product reception** | Nothing shipped, or poorly received | Product exists, mixed reception | Product well-received, growing |
| **Role fit** | Title/level mismatch | Reasonable match | Perfect match for user's experience + growth |

**Tier thresholds:**
- **Tier 1 (Strong Match):** Average 4+ across all dimensions
- **Tier 2 (Good Match):** Average 3+ with no dimension below 2
- **Tier 3 (Watch List):** Interesting company, score below Tier 2 OR no current opening

---

## Fit Signals

Beyond the scoring rubric, reflect on what the user actually wants. Track these as they emerge from interviews, and update `.claude/skills/learnings.md` or a `learnings.md` file next to interview notes when new patterns appear.

**Energizers (look for these):**
- [User-specific energizers — filled in during `/onboard` and updated as patterns emerge]

**Yellow flags (watch for these):**
- [User-specific yellow flags — filled in during `/onboard` and updated as patterns emerge]

---

## User Background (For Fit Assessment)

{{user_background_summary}}

---

## Deduplication Rules

When the same role appears on multiple boards:
- Keep one entry with the best link
- Priority: ATS link (Greenhouse/Ashby/Lever) > company career page > aggregator (Built In, LinkedIn)
- Note "Also found on: [other sources]" if helpful
