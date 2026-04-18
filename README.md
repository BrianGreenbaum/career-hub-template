# Career Hub Template

A Claude Code–powered career management starter. Clone it, run `/onboard`, and you've got a personalized hub for job search, work history, content, and professional relationships — all as plain markdown on your disk.

> **New here?** Open [`overview.html`](./overview.html) in a browser for a visual walkthrough of how the whole system works.

---

## Install

### Prerequisites

- **[Claude Code](https://code.claude.com/docs/en/overview)** installed and working
- **[pdftotext](https://www.xpdfreader.com/pdftotext-man.html)** — for reading PDF resumes:
  ```bash
  brew install poppler
  ```
- **(Optional) [Obsidian](https://obsidian.md/)** with the Kanban community plugin — the TODOs board renders as a drag-and-drop Kanban

### Setup

```bash
git clone https://github.com/BrianGreenbaum/career-hub-template ~/CareerHub
cd ~/CareerHub
claude
```

Then inside Claude Code:

```
/onboard
```

That's it. The onboarding interview (~10–15 min) asks about your background, role, and goals, fills in the template with your details, and generates a customized `/job-search` skill tailored to your target roles and criteria.

---

## Skills

All skills live under `.claude/skills/` and are invoked with a `/` prefix inside Claude Code. Open any `SKILL.md` file to see or edit how it works — they're just markdown.

| Skill | What it does |
|---|---|
| `/onboard` | Entry point for a new install. Interviews you, populates `CLAUDE.md`, generates a customized `/job-search` skill, and seeds starter content. Re-run if your role or goals change significantly. |
| `/process-work-history` | Scans resumes, LinkedIn exports, performance reviews, and old project docs into structured per-company summaries. Flags gaps and offers to fill them via `/project-interview`. Re-runnable whenever you drop new files in. |
| `/project-interview` | Interviews you about a specific project to capture a comprehensive dossier (context, role, decisions, outcomes, metrics). Output feeds `/case-study`. |
| `/case-study` | Builds an interview-ready case study presentation outline plus a companion dossier, from an existing project dossier or a fresh interview. |
| `/job-search` | Generated during `/onboard`, tailored to your target roles, locations, comp, and industries. Runs an exhaustive multi-source search, filters against your criteria, and produces a qualified opportunity list. |
| `/todo` | CLI Kanban board management — add, done, move, list, clean. Backed by `TODOS.md`, which renders as a drag-and-drop board in Obsidian. |
| `/update` | Weekly professional journal. Scans recent activity across the hub and drafts a recap entry in `Weekly/`. |

---

## Folder layout

```
.
├── CLAUDE.md              # Root instructions (populated by /onboard)
├── README.md              # This file
├── TODOS.md               # Kanban board (manage via /todo)
├── overview.html          # Visual overview of the system
│
├── Search/
│   └── {year}/            # Active job search cycle
│       ├── CLAUDE.md      # Workflow instructions
│       ├── DASHBOARD.md   # Pipeline status
│       ├── companies/     # Per-company folders
│       ├── searches/      # Search run logs
│       └── networking/    # Non-company contacts
│
├── Weekly/                # Weekly journal entries
├── Networking/            # Professional relationships
├── Work-History/          # Past and current roles per company
├── Portfolio/             # Case studies and portfolio assets
├── Content/               # Drafts, posts, writing
│
└── .claude/
    └── skills/            # The skills listed above
```

---

## Daily use

Once set up, the most common commands:

- `/todo add [task]` — add something to your task board
- `/todo list #search` — see your active job search tasks
- `/update` — journal a weekly entry
- `/job-search` — run an exhaustive search for new roles
- `/project-interview` — capture a new project dossier
- `/case-study [project]` — build an interview case study outline

---

## Customizing

Everything here is designed to be edited.

- **`CLAUDE.md` is yours.** Edit it to add context Claude should always know about you. Update whenever your situation changes.
- **Skills are just markdown.** Open any `.claude/skills/*/SKILL.md` and modify it. Claude re-reads it on every invocation.
- **Add your own.** Use the `skill-creator` skill to build new ones; use the existing skills as examples of shape.
- **Delete what you don't need.** Not journaling? Delete `Weekly/`. Not publishing? Delete `Content/`. The hub shouldn't have folders you don't use.

---

## What this is *not*

- **Not a web app** — it's files on your disk that Claude Code operates on
- **Not a CRM or ATS** — it's a personal knowledge base, not a sales tool
- **Not automated** — skills run when you invoke them; nothing happens in the background

---

## Troubleshooting

**`/onboard` isn't available.**
Make sure you're running `claude` from inside the hub directory. Skills are discovered from `.claude/skills/` relative to where you start Claude Code.

**PDFs aren't getting read during `/process-work-history`.**
Install `pdftotext`: `brew install poppler`, then re-run the skill.

**The Kanban board renders as plain markdown.**
Install [Obsidian](https://obsidian.md/) and the Kanban community plugin by mgmeyers. Point Obsidian at the hub as a vault. `TODOS.md` will render as a drag-and-drop board.

**`/job-search` references files that don't exist yet.**
That's normal on first run — the skill creates `Search/{year}/DASHBOARD.md`, `companies/prospects.md`, and `searches/overview.md` as it goes. If onboarding didn't seed them, re-run `/onboard` or create them by hand.

---

## Credits

Built by [Brian Greenbaum](https://briangreenbaum.com) while running his own career search and documenting the process. Shared as a starter because the system worked well enough that it seemed worth letting other people use it too.

If you find bugs or have suggestions, open an issue or PR.
