# Verification Guide

How to verify job postings are active and maintain the database.

---

## Verifying Active Pipeline

For each role in `DASHBOARD.md` Active Pipeline:

1. Check the company's careers page or ATS link
2. Confirm the specific role is still listed
3. Flag roles with no movement in 2+ weeks for the user's review
4. Note any stage changes or new information

## Verifying Prospect Links

**High Interest (verify all):**
1. WebFetch the application link
2. If it returns error, "job not found", or redirects to generic careers page → mark for Closed
3. If it loads successfully → update status to "✅ Verified Open" and set "Last Checked" to today
4. Note any comp or location changes from previous check

**Medium Interest (spot-check ⚠️ Unverified):**
1. WebFetch links marked ⚠️
2. Update status accordingly
3. Move to Closed if dead

**Watch List companies:**
1. Visit the career page URL listed in the Watch List
2. Search for relevant roles at the user's target level
3. If new relevant role found → note details for promotion to High/Medium Interest
4. Update "Last Checked" date

---

## Link Verification Standards

**Verified statuses:**
- ✅ Verified Open — Link loads, job posting is visible and accepting applications
- ✅ Likely Open — Link loads but couldn't confirm apply button (JS-rendered, etc.)
- ⚠️ Unverified — Haven't been able to check or link is on aggregator only
- ⚠️ Verify on careers site — Aggregator link works but no direct ATS link found
- ⚠️ May be closed — Posting looks old or has warning signs

**Warning signs that a posting is closed:**
- Link redirects to generic careers page (not the specific job)
- Page shows "This job is no longer available"
- Posting date is 6+ months old with no updates
- Aggregator link works but original ATS link is gone
- Role title on page doesn't match what was listed

**Link preference order:**
1. ATS link (Greenhouse, Ashby, Lever) — most reliable
2. Company career page — second best
3. Aggregator link (Built In, LinkedIn, Indeed) — least reliable, verify first

---

## When Links Break

1. Check the company's main careers page for the role
2. Search for the role title + company name to find alternative listings
3. If an ATS link is found, use that instead
4. If no working link found → add to "Needs Verification" section with note to check careers page directly
5. Never silently include broken links — flag them clearly

---

## Verification Report Format

After verification, produce a structured summary:

```
Pipeline roles: X/Y confirmed still active
- [Company] [Role]: [status] [notes]
- ...

High Interest: X verified open, Y to close
- [Company] [Role]: [status] [date]
- ...

Medium Interest: X verified, Y to close
- [Company] [Role]: [status]
- ...

Watch List: X companies checked, Y new roles found
- [Company]: [new role details or "no changes"]
- ...
```
