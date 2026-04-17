# Work History — Inbox

Drop your source career documents into this folder, then run `/process-work-history` to scan and extract them into structured per-company summaries.

## What to drop in

- **Your resume** — PDF, .docx, or .md
- **LinkedIn export** — go to Settings → Data Privacy → Get a copy of your data → "Want something in particular?" → at least "Profile"
- **Performance reviews** from past jobs
- **Old project writeups, case studies, presentation PDFs**
- **Portfolio docs** (text-extractable formats work best)

## What gets ignored

- `.fig`, `.sketch`, `.jam` — design files
- `.mp4`, `.mov`, `.mp3` — video/audio
- Large standalone images

These are noted in `SOURCE_TRACKER.md` as Skip but not processed.

## Notes

- Files dropped here are **git-ignored** (see root `.gitignore`). They stay local.
- After processing, extracted summaries live in `Work-History/{company}/summaries/` and are git-tracked.
- You can re-run `/process-work-history` any time you drop new files.
