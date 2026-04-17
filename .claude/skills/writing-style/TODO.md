# writing-style skill — TODO

> This skill slot is intentionally empty in v1 of the career-hub-template. It's a placeholder for a future design session.

## What it should do

A standalone `/writing-style` skill that captures the user's voice and tone preferences, then applies them consistently across other skills that generate written output (`/update`, `/case-study`, `/project-interview`, drafts in `Content/`, cover letters, etc.).

## Why a dedicated skill

Voice is the most personal part of a writing system. Rather than shipping a generic `WRITING_STYLE.md` that users ignore or override, this skill interviews the user about their voice preferences and produces a living style guide they actually use. It can also be refined over time as the user sees Claude generate content and gives feedback on what sounds right vs. wrong.

## Rough design notes

- **Interview phase** — asks about voice reference points (authors they admire, their own published writing, tone they want to hit), pet peeves (words/phrases they hate), formality level, platform-specific adjustments, examples of writing they'd want Claude to match
- **Calibration phase** — generates sample text in the proposed voice, user critiques, iterates
- **Output** — a `writing-style.md` file at the root (or inside the skill folder) that other skills read and apply
- **Refinement** — can be re-run any time the user wants to tune the voice, or invoked with `/writing-style refine` to adjust based on recent feedback

## Integration points

Other skills in the template should reference `writing-style.md` (if present) when generating written output. The skills that need this are:

- `/update` — weekly journal entries
- `/project-interview` — project dossiers  
- `/case-study` — presentation outlines and dossiers
- `/job-search` — cover letter drafts, pitch language
- Any `Content/` drafting

Right now those skills fall back to generic defaults. Once `/writing-style` is built, they should prefer the user's style guide if it exists.

## Status

**To be designed with the template author in a follow-up session.**
