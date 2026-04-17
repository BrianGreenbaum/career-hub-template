# Career Hub — Instructions for Claude

## Overview

This is **{{user_name}}**'s career management hub. It contains job search materials, work history, portfolio assets, and professional relationships.

> If this file still contains double-brace placeholder tokens, run `/onboard` to fill in your details and generate a customized job-search skill. After onboarding, `/onboard` should be re-run if your role or goals change significantly.

---

## About the User

- **Name:** {{user_name}}
- **Location:** {{user_location}}
- **Current role:** {{current_role}} at {{current_company}}
- **Years of experience:** {{years_experience}}
- **Areas of focus:** {{areas_of_focus}}
- **Domain / industry:** {{focus_domain}}

### Current context

{{current_role_context}}

### Active job search

{{active_search_summary}}

---

## Writing Style

Default to: conversational, first-person, direct, grounded in specific examples, no filler or corporate-speak, short paragraphs, bullets for lists.

---

## Task Management

All action items live on a single Kanban board: [TODOS.md](./TODOS.md)

**Default tags:** `#search`, `#networking`, `#work` (customize in `TODOS.md` as needed)
**Priority:** 🔴 High, 🟡 Medium, 🟢 Low (optional prefix)
**Due dates:** `@{YYYY-MM-DD}` (optional, Kanban plugin date picker format)
**Columns:** Not Started → Started → Waiting → Done → Archive

Manage from the CLI with `/todo` — add, done, move, list, clean.

The board renders as a drag-and-drop Kanban in Obsidian (requires the Kanban community plugin by mgmeyers). Without the plugin it's still readable as plain markdown.

**What goes on the board:** Action items — things the user needs to do or is waiting on.
**What doesn't:** Job pipeline stages (those stay in `Search/{{current_search_year}}/DASHBOARD.md`), recurring reminders (those stay in CLAUDE.md files).

---

## Folder Structure

```
CareerHub/
├── CLAUDE.md                    # This file — root instructions
├── README.md                    # Nav hub for humans reading the repo
├── TODOS.md                     # Unified Kanban board (all action items)
│
├── Search/{{current_search_year}}/               # Active job search (created by /onboard if user opted in)
│   ├── CLAUDE.md                # Job search workflow instructions
│   ├── DASHBOARD.md             # Job pipeline, next actions
│   └── ...
│
├── Weekly/                      # Weekly professional recaps (optional, gated by onboarding)
│   ├── README.md                # Log index
│   └── {YYYY}-W{NN}.md          # Per-week entries
│
├── Networking/                  # Professional relationships
│   ├── README.md                # People index
│   └── [person].md              # Individual contact notes
│
├── Work-History/                # Past work by company
│   ├── CLAUDE.md                # Processing instructions
│   └── [company]/               # One folder per employer
│
├── Portfolio/                   # Case studies and portfolio assets
│   └── case-studies/
│
└── .claude/
    └── skills/                  # Reusable skills
```

---

## Running Claude from Different Locations

| Run from | Context loaded | Best for |
|----------|----------------|----------|
| Hub root | Root CLAUDE.md | Broad career work, switching between areas |
| `Search/{{current_search_year}}/` | Root + Search CLAUDE.md | Focused job search sessions |

---

## File Linking (Obsidian Compatible)

The user views these files in Obsidian. Use proper markdown links (not backtick code formatting) so links are clickable.

### Link Format
```markdown
[Link Text](./path/to/file.md)
```

### Rules
1. **Always link to files, not folders** — Obsidian doesn't handle folder links well
2. **Add back-links** — Include navigation back to parent hubs
3. **Use clickable links for key assets** — Don't use backtick formatting for paths that should be navigable

---

## Formatting Rules

### Timelines
Always sort timelines with **most recent date at the top**:
```markdown
| Date | Event |
|------|-------|
| 2026-01-25 | Most recent event |
| 2026-01-20 | Earlier event |
```

---

## Inbound Updates (Recruiter Outreach, Interview Updates, etc.)

When the user shares job search updates conversationally — recruiter messages, interview scheduling, offer details, rejections, or status changes — treat them as record updates. Automatically:

1. **Create or update the contact file** in the company folder (`Search/{{current_search_year}}/companies/[company]/`) or `Search/{{current_search_year}}/networking/` for non-company contacts
2. **Create or update the job overview** in `Search/{{current_search_year}}/companies/[company]/overview.md`
3. **Move the opportunity through the pipeline** in `Search/{{current_search_year}}/DASHBOARD.md`
4. **Update or create relevant todos** in `TODOS.md`
5. **Clean up prospects** if the company was previously tracked there

Don't wait to be asked — if the information implies a record change, make it.

---

## Weekly Professional Updates

{{weekly_updates_section}}

<!--
If the user opted into weekly journaling during /onboard, the above placeholder is replaced with:

The user captures professional updates via `/update`. Prompt them to run it if 7+ days have passed since the last entry.

**Latest entry:** [Weekly/README.md](./Weekly/README.md)

If the user opted out, the placeholder is replaced with:

The user did not opt into weekly journaling. The `/update` skill is still available if they want to capture an entry ad-hoc.
-->
