# Search Sources

All job board queries and discovery searches for the user's job search. Location is always **{{target_locations}}**.

---

## Search Titles

Search ALL of these title variations at each source:

{{search_title_variations}}

<!--
Example (for a senior product designer):

**Primary:**
- "staff product designer"
- "senior staff product designer"
- "principal product designer"

**Also search:**
- "head of design" OR "head of product design"
- "design director"
- "product design lead"
- "founding designer"
- "design engineer"

/onboard fills this in based on the user's target roles.
-->

---

## Phase 2: Company Discovery

Run these before searching boards to find new companies in the user's focus domain:

**Recently funded:**
```
"series C" OR "series D" OR "series E" {{focus_domain}} company {{search_year}} site:techcrunch.com
"raises" "$100M" {{focus_domain}} {{search_year}} site:techcrunch.com OR site:bloomberg.com
{{focus_domain}} startup funding {{search_year}} {{primary_location}} hiring
```

**General discovery:**
```
"{{focus_domain}} company" "[role title]" hiring {{primary_location}} {{search_year}}
"{{focus_domain}} startup" hiring {{primary_location}} {{search_year}}
```

Cross-reference against `target-companies.md` — note new promising companies for potential addition.

---

## Phase 3: Job Board Searches

### A. ATS Boards (Most Reliable — Prioritize)

```
site:greenhouse.io "[title variation]" {{focus_domain}}
site:lever.co "[title variation]" {{focus_domain}}
site:ashbyhq.com "[title variation]" {{focus_domain}}
```

Run each title variation through each ATS.

### B. Built In {{primary_location}}

If the user's primary location has a Built In regional site:

```
site:builtin{{primary_location_slug}}.com "[title variation]" {{focus_domain}}
```

### C. LinkedIn Jobs

Note: Unreliable due to crawl blocking. Supplement only.

```
site:linkedin.com/jobs "[title variation]" {{primary_location}} {{focus_domain}}
```

### D. Hacker News "Who's Hiring" (Monthly)

Check the most recent thread (goes up 1st of each month):
```
site:news.ycombinator.com "who is hiring" [current month] [current year]
```

Also search `hn.algolia.com` filtered to "Who's Hiring" threads for the user's target role titles.

### E. Y Combinator Jobs

```
site:workatastartup.com "[title variation]" {{focus_domain}}
site:ycombinator.com/companies "[title variation]"
```

### F. Domain-Specific Boards

Fill in based on the user's `{{focus_domain}}`. Examples:

- AI: `aijobs.ai`, `wellfound.com` (filter "AI")
- Fintech: `workinfintech.com`
- Climate: `climatebase.org`
- Remote: `weworkremotely.com`, `remotive.com`

### G. Role-Specific Boards

Boards specialized for the user's target roles. These are discovered during `/onboard` via a web search for "[role type] job boards" and confirmed with the user.

<!--
Examples by role type (onboard discovers these dynamically and fills in the actual list):
- Product management: producthunt.com/jobs, mindtheproduct.com/jobs, pmjobs.xyz
- Product design: dribbble.com/jobs, aiga.org/jobs, cofolios.com/jobs, uxjobsboard.com
- Engineering: stackoverflow.com/jobs, triplebyte.com, hired.com
- Data science: kaggle.com/jobs, datajobs.com
- Finance/accounting: efinancialcareers.com, accountingfly.com, ihireaccounting.com
- Legal: lawjobs.com, idealist.org, attorneyjobs.com
- Marketing: marketinghire.com, wearemarketers.com
- Sales: repvue.com, bravado.co
- Healthcare: healthcarejobsite.com
- Education: higheredjobs.com, k12jobspot.com
-->

{{role_specific_boards}}

### H. Location-Specific

For NYC: `garysguide.com`
For SF: `workatastartup.com`, local SF job boards
For Remote: `weworkremotely.com`, `remotive.com`

Replace with the user's location-specific boards.

### I. VC Portfolio Boards

**Searchable (prioritize):**
```
site:jobs.sequoiacap.com "[title variation]"
site:jobs.a16z.com "[title variation]"
```

**Other VCs via Google:**
```
"[VC name] portfolio" "[title variation]" hiring {{search_year}}
```

Key VCs (adjust for the user's domain): Greylock, Accel, General Catalyst, Thrive Capital, Bessemer, Founders Fund, Lightspeed, Index Ventures, Insight Partners, Kleiner Perkins.

### J. Company Career Pages

Check career pages of Tier 1 and Tier 2 companies from `target-companies.md`.

### K. General Web Search

```
"[title variation]" {{focus_domain}} {{primary_location}} {{search_year}}
"[title variation]" {{focus_domain}} company hiring {{search_year}}
```

---

## Search Cadence

| Source | Frequency |
|--------|-----------|
| ATS boards, regional Built In, YC Jobs, domain boards, remote boards | Every search |
| Company career pages (Tier 1 + Tier 2) | Every search |
| HN "Who's Hiring" | Monthly (1st of month) |
| VC portfolio boards, role-specific boards | Every 2 weeks |
| Recently funded discovery | Every 2 weeks |

---

## Research Searches (For Top Candidates)

**Company credibility / thesis fit:**
```
"[Company]" "[user's thesis keywords]" site:techcrunch.com OR site:theinformation.com
```

**Liquidity:**
```
"[Company] IPO" {{search_year}}
"[Company] Series [D/E/F]" funding
"[Company]" site:nasdaq.com OR site:nyse.com
```

**{{primary_location}} presence:**
```
"[Company] {{primary_location}} office"
```

**Recently funded (discovery):**
```
{{focus_domain}} startup funding round {{search_year}} {{primary_location}}
site:crunchbase.com {{focus_domain}} company funding {{search_year}}
```

---

## L. User-Specified Custom Boards

Additional boards the user asked to include during `/onboard` or added later. These are searched alongside the standard sources above.

{{custom_boards}}

<!--
If empty, the user didn't add any custom boards. They can add boards here at any time,
or ask Claude to add them. Format:

- [Board Name](https://example.com) — Brief description
  ```
  site:example.com "[title variation]"
  ```
-->
