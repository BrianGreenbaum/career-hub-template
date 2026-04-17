# Output Format

Templates for search results files and database updates.

---

## Search Results File

Save to `Search/{{search_year}}/searches/YYYY-MM-DD.md`:

```markdown
# Job Search — YYYY-MM-DD

**Focus:** {{target_locations}}, {{focus_domain}}, {{target_roles}}
**Sources searched:** [list all sources checked]

---

## Verification Summary

- Active pipeline roles verified: X/Y still active
- High Interest prospects verified: X still open, Y closed
- Watch List companies checked: X, Y new roles found

## Tier 1: Strong Match (Apply Now)

| Company | Role | Salary | Location | Fit Score | Liquidity | Link | Verified |
|---------|------|--------|----------|-----------|-----------|------|----------|

[For each Tier 1, add a section with:]
### [Company] — [Role]
- **Domain fit:** [evidence]
- **Liquidity:** [status]
- **Why it fits:** [specific reasons]
- **Concerns:** [if any]
- **Verified active:** YYYY-MM-DD

## Tier 2: Good Match (Worth Exploring)

| Company | Role | Salary | Location | Notes | Link | Verified |
|---------|------|--------|----------|-------|------|----------|

## Tier 3: Watch List

| Company | Notes |
|---------|-------|

## Needs Verification

| Company | Role | Salary | Note | Careers Page |
|---------|------|--------|------|--------------|

## New Companies Discovered

| Company | What They Do | Funding | Why Interesting | Careers Page |
|---------|-------------|---------|-----------------|--------------|

## Confirmed Closed (This Search)

| Company | Role | Salary | Note |
|---------|------|--------|------|

## Disqualified (This Search)

| Company | Role | Reason |
|---------|------|--------|

## Top Opportunities Right Now

Across active pipeline + prospects, here's where the user should focus:
1. [Company — Role]: [why now]
2. ...
3. ...
```

---

## Prospects Update Procedures

After each search, update `Search/{{search_year}}/companies/prospects.md`:

**Add new finds:**
- Tier 1 results → High Interest (unless the user is actively pursuing → Active Pipeline)
- Tier 2 results → Medium Interest
- Companies with no current opening → Watch List

**Close dead roles:**
- Move verified-closed roles to the "Closed / No Longer Available" section
- Include: Company, Role, Reason, Date Confirmed

**Update existing entries:**
- Set "Last Checked" to today's date for all verified roles
- Update verification status (✅, ⚠️, etc.)
- Update comp or location if changed
- Update "Last updated" date at top of file

**Respect boundaries:**
- Don't resurface "Not Interested" companies
- Don't resurface "Companies to SKIP" entries
- Don't duplicate Active Pipeline roles

---

## Tracking File Updates

After every search run:

1. **`Search/{{search_year}}/CLAUDE.md`** — Update "Last job search" date
2. **`Search/{{search_year}}/DASHBOARD.md`** — Update "Last updated" date and "Last job search" in Quick Stats
3. **`Search/{{search_year}}/searches/overview.md`** — Add summary row:

```markdown
| [YYYY-MM-DD](./YYYY-MM-DD.md) | {{target_locations}}, {{focus_domain}} | X | [Brief summary of key finds and closures] |
```

4. **For roles the user wants to actively pursue:**
   - Create company folder: `Search/{{search_year}}/companies/[company]/`
   - Add `overview.md` with `← [Back to Dashboard](../../DASHBOARD.md)` at top
   - Add `posting-[role-slug].md` with full posting details and URL
   - Add to DASHBOARD.md Active Pipeline table
