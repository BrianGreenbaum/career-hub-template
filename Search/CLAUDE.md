# Job Search Hub — Instructions for Claude

## Overview

This folder contains the user's job search work, organized by year. Each year gets its own subfolder (e.g., `2026/`) containing that cycle's pipeline, applications, interview notes, and related materials.

**For the user's background, see the root [CLAUDE.md](../CLAUDE.md).**

---

## Two Hubs, Different Purposes

- **`{{current_search_year}}/DASHBOARD.md`** — Pipeline status. Tracks what stage each application is in (Researching → Applied → Recruiter Screen → etc.). Updated when an application moves forward.
- **[TODOS.md](../TODOS.md)** — Action items. Tasks to do, things to follow up on, items waiting on others. Filter by `#search` for job search tasks. Managed via `/todo`.

---

## Folder Structure

```
Search/
└── {{current_search_year}}/
    ├── DASHBOARD.md       # Main hub — pipeline status, quick links
    ├── CLAUDE.md          # Per-year workflow instructions (optional — can reference this file)
    ├── companies/         # Company-specific folders + prospects
    │   ├── prospects.md   # Companies of interest not yet active
    │   └── [company]/     # Each company has overview, postings, interviews, contacts
    ├── searches/          # Job search results by date
    └── networking/        # Non-company contacts (external recruiters, general networking)
```

---

## Job Application Workflow

### When adding a new job:
1. Create a folder: `{{current_search_year}}/companies/[company-name]/`
2. Add `posting-[short-role-title].md` with full details and URL
3. Add `overview.md` as the main hub linking all related files (with `← [Back to Dashboard](../../DASHBOARD.md)` at top)
4. Add entry to `{{current_search_year}}/DASHBOARD.md` (Active Pipeline + Next Actions)

### When updating an application:
1. Update the stage and next action in `DASHBOARD.md`
2. Add timeline entry in the company's `overview.md` (most recent at top)
3. Link any new files (interview notes, cover letters, etc.)
4. **Always keep both DASHBOARD.md and the job's overview.md current**

### After an interview:
When the user shares a call summary or transcript, document it in detail:
1. Save detailed notes to `companies/[company]/interview-[type-or-name]-[date].md` — capture everything: what the user shared, what the interviewer said, notable moments, new intel, open questions
2. Create/update contact file if it's a new person: `companies/[company]/contact-[name].md`
3. Link from the company's `overview.md` (Key Files section + timeline entry)
4. Update stage in `DASHBOARD.md` if the application moved forward
5. Update `TODOS.md` with any new action items
6. Add timeline entry (most recent at top)

---

## File Organization Rules

All company-related files live in `{{current_search_year}}/companies/[company]/`. Files use prefix-based naming so they group by type when sorted alphabetically:

| Prefix | Use | Example |
|--------|-----|---------|
| `overview.md` | Company hub (always present) | `overview.md` |
| `posting-` | Job postings | `posting-staff-designer.md` |
| `interview-` | Interview notes (after the fact) | `interview-2026-02-06-hm-carl.md` |
| `prep-` | Interview/application prep | `prep-case-study-2026-02-16.md` |
| `contact-` | People at the company | `contact-carl-nelson.md` |
| `research-` | Company/role research | `research-culture.md` |

Other rules:
- **Non-company contacts** (external recruiters, general networking) go in `{{current_search_year}}/networking/`
- **`searches/`** lives at the year-folder level, not inside companies

---

## Formatting Rules

### Timelines
Always sort timelines with **most recent date at the top**:
```markdown
| Date | Event |
|------|-------|
| 2026-01-18 | Applied via Greenhouse |
| 2026-01-16 | Informational call with contact |
```

### overview.md as Source of Truth
Each job folder's `overview.md` should always reflect the latest state:
- Current status and next action
- Complete timeline of all activity
- Links to all related files (job posting, cover letter, interview notes, etc.)
- Key themes and talking points for interviews

---

## File Linking (Obsidian Compatible)

### Common Link Patterns
| From | To | Link |
|------|-----|------|
| Company overview | Dashboard | `[Back to Dashboard](../../DASHBOARD.md)` |
| Company overview | Job posting | `[Job Posting](./posting-role-title.md)` |
| Company overview | Interview notes | `[Call Notes](./interview-type-date.md)` |
| Company overview | Prep doc | `[Prep](./prep-type-date.md)` |
| Company overview | Contact | `[Name](./contact-name.md)` |
| Prospects | Dashboard | `[Back to Dashboard](../DASHBOARD.md)` |
| Dashboard | Company overview | `[Company](./companies/company-folder/overview.md)` |

---

## Key Assets

- Dashboard: `./DASHBOARD.md` — Main hub for pipeline status and next actions
- Prospects list: `./companies/prospects.md`
- Search history: `./searches/overview.md`
- Work project summaries: `../../Work-History/`

---

## Reminders

### Weekly Job Search
Remind the user to review job boards and database at least once a week. Check when the last search was done and prompt if it's been more than 7 days.

**Last job search:** (updated by `/job-search` skill)

---

## Compounding Learnings

The goal: each interview and application should make the next one easier.

### After Interviews
When the user shares interview notes or transcripts, prompt for a quick debrief before filing:
1. **What landed?** — Moments that felt strong, stories that resonated
2. **What surprised you?** — Questions you'd answer differently, gaps in prep
3. **Red/yellow flags?** — Anything concerning about the role, team, or company
4. **Shift in thinking?** — Did this change what they're looking for?

Capture insights in a `learnings.md` file alongside the interview notes, or in a shared `{{current_search_year}}/learnings.md` for cross-cutting patterns.

### Periodic Criteria Check
Every few weeks, or after a significant interview, review the Job Search Criteria below and ask if anything has shifted.

---

## Job Search Criteria

> These criteria are filled in by `/onboard` during setup. The `/job-search` skill is customized per user based on these values.

- **Target roles:** {{target_roles}}
- **Target locations:** {{target_locations}}
- **Comp range:** {{target_comp_range}}
- **Must-haves:** {{must_haves}}
- **Industries to avoid:** {{industries_to_avoid}}
- **Skip-list companies:** {{skip_list_companies}}

### Additional Preferences

{{additional_preferences}}
