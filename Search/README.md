# Search

Active job search hub. Tracks companies you're pursuing, interview notes, prep docs, and pipeline status.

## How it works

Organize by year — each active job search year gets its own folder:

```
Search/
└── {year}/
    ├── CLAUDE.md             # Workflow instructions for this search cycle
    ├── DASHBOARD.md          # Pipeline status (who's at what stage)
    ├── companies/
    │   ├── prospects.md      # Companies you're watching, not yet active
    │   └── [company]/        # One folder per company you're actively pursuing
    │       ├── overview.md   # Main hub for this company
    │       ├── posting-*.md  # Job postings
    │       ├── interview-*.md # Interview notes
    │       ├── prep-*.md     # Interview prep
    │       ├── contact-*.md  # People at the company
    │       └── research-*.md # Company research
    ├── searches/             # Log of job searches run via /job-search
    └── networking/           # Recruiters and contacts not tied to a specific company
```

## Getting started

After `/onboard`, a `{current year}/` subfolder will be created with a templated `CLAUDE.md` and empty `DASHBOARD.md`. Use `/job-search` to find roles and `/todo` to track actions.

**Key skills:**
- `/job-search` — runs an exhaustive search customized to your criteria
- `/todo` — manages action items tagged `#search`
