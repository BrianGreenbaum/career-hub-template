# Work History

Past and current roles, organized by company. Source documents (resumes, reviews, presentation PDFs, old project docs) go in per-company subfolders; AI-generated summaries go in `{company}/summaries/`.

## How it works

```
Work-History/
├── CLAUDE.md                  # Processing instructions
├── README.md                  # This file
└── {company}/
    ├── summaries/             # Git-tracked markdown outputs
    │   ├── {company}-overview.md
    │   ├── SOURCE_TRACKER.md
    │   └── {project}.md
    └── [source files]         # Resumes, reviews, PDFs — git-ignored
```

Only the `summaries/` folders are committed to git. The rest is local reference material.

## Getting started

Run `/process-work-history`. It will:

1. Ask which folder your source files are in (or prompt you to drop them into one).
2. Scan PDFs, LinkedIn exports, resume docs, old project writeups.
3. Extract a timeline of companies, roles, and projects.
4. Identify gaps (missing years, companies mentioned but not detailed, projects with no narrative).
5. Offer to run `/project-interview` for each gap to fill it in.

You can re-run `/process-work-history` any time you drop new files in or want to do a gap check.
