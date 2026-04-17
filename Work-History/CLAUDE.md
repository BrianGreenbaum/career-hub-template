# Work History — Instructions for Claude

## Overview

This folder contains source documents and AI-generated summaries for each company the user has worked at. The goal is to turn raw artifacts (resumes, performance reviews, research docs, slide decks, old project writeups) into structured, interview-ready career overviews.

---

## Folder Structure (per company)

```
Work-History/
├── CLAUDE.md              # This file — shared instructions
├── {company}/
│   ├── summaries/         # Git-tracked markdown outputs
│   │   ├── {company}-overview.md    # Main career overview
│   │   ├── SOURCE_TRACKER.md        # Which docs have been processed
│   │   └── {project}.md             # Deep-dive summaries for major projects
│   └── [source files]     # Git-ignored (PDFs, PPTX, XLSX, DOCX, etc.)
```

Only the `summaries/` folders are tracked in git. Everything else is local reference material.

---

## The Summarization Process

### Starting a new company

1. **Read the user's resume first** if one is available in `Portfolio/` or the work-history inbox. It provides the positioning language, framing, and metrics the user uses to describe each role.

2. **Create the folder structure:**
   - `Work-History/{company}/summaries/`
   - `Work-History/{company}/summaries/{company}-overview.md`
   - `Work-History/{company}/summaries/SOURCE_TRACKER.md`

3. **Inventory source documents.** List every file in the company folder in SOURCE_TRACKER.md. Categorize and mark skip/todo status using the format below.

4. **Process in batches.** Read 3-6 related documents per batch. After each batch: update the overview, mark files as Done in the tracker, commit.

### Processing a batch

1. Read the source documents
2. Extract: projects, metrics, dates, quotes, relationships, key decisions
3. Update the overview with new information — don't duplicate what's already there
4. Update SOURCE_TRACKER.md to mark files as Done
5. Commit with a message like: `Process {company} batch 2: Performance Reviews`

### Handling large PDFs

Many source documents are PDFs that are too large to read directly (>1MB). Use `pdftotext` to convert them to plain text first:

```bash
# Install pdftotext (part of poppler) if not already installed
brew install poppler

# Convert PDF to text with layout preservation
pdftotext -layout "source-file.pdf" output.txt

# Then read the text file
```

**Why this works:**
- **Massive size reduction:** A 13MB PDF can become an 11KB text file
- **Preserves content:** All text content is extracted and readable
- **Layout preservation:** The `-layout` flag maintains visual structure (columns, spacing)
- **Fast processing:** Conversion takes seconds even for large files

The text files are `.gitignore`d, so they won't clutter the repo. Use this technique for any PDF that fails to load due to size.

### What to extract from source documents

- **Projects:** What was built, the user's role, outcome, dates
- **Metrics:** Revenue, accuracy, growth %, adoption numbers — anything quantifiable
- **Quotes:** Manager/peer feedback that's useful for interviews
- **Decisions:** Strategic calls the user made (especially where they initiated something)
- **Patterns:** Evidence of recurring themes
- **Timeline facts:** Dates, team changes, org context

---

## Overview Template

Each `{company}-overview.md` should follow this structure:

```markdown
# {Company} — Career Overview

**{User Name}** | {dates}
**Title:** {title}
**Company:** {one-line company description}

## The {Company} Story
Narrative arc: what the user did, what they did well, how they grew. 2-4 paragraphs.

## Current State ({month} {year})
Only for current employer. Remove for past roles.

## Project Inventory
Quick-scan table, reverse chronological. **Link project names to their detailed sections below using Obsidian internal links.**

Use the format: `[[#Section Header\|Display Text]]`

| Project | Date | Role | One-line summary |

## Performance Review Summary
Timeline table + key themes. Only if review data exists.

## Project Details
Organized by era, reverse chronological. Each project gets:
- What it was
- The user's role
- Key decisions / contributions
- Outcome / impact
- Link to deep-dive if one exists

## Internal Tools Built
Table of tools the user built (if applicable).

## Positioning Notes for Job Search
How to talk about this role in interviews. What to lead with, what to connect to.

## Quotable Moments
Manager and peer quotes worth remembering.

## Portfolio Assets on Disk
What exists locally (videos, repos, design files).
```

Sections can be omitted if there's no data for them.

---

## SOURCE_TRACKER.md Template

```markdown
# {Company} Source Document Tracker

Tracks which documents from `Work-History/{company}/` have been processed into summaries.

← [Back to summaries](./{company}-overview.md)

---

## Summaries Created

| Summary | Source Documents |
|---------|-----------------|
| [{company}-overview.md](./{company}-overview.md) | ... |

---

## Source Documents — Status

### {Category}
| File | Status |
|------|--------|
| filename.pdf | Todo / Done / Skip — {reason} |
```

### Status values
- **Done** — processed into a summary
- **Todo** — not yet processed
- **Skip — {reason}** — not processable (video, design file, duplicate, personal, admin)

### Skip rules
- `.fig`, `.sketch`, `.jam` → Skip (design file)
- `.mp4`, `.mov`, `.mp3` → Skip (video/audio)
- `.png`, `.jpg`, `.svg` → Skip (image)
- `.pptx` when a `.pdf` version exists → Skip (duplicate)
- `.docx` when a `.pdf` version exists → Skip (duplicate)
- Personal/admin docs (offer letters, etc.) → Skip

---

## Batch Strategy

Group related documents together. Good groupings:
- By project (all docs for one initiative)
- By time period (all docs from one quarter)
- By type (all performance reviews, all presentations)

Aim for 3-6 documents per batch to keep context manageable.

---

## Writing Rules

- First person where appropriate, third person for overview sections
- Practical and direct — no filler
- Anchor claims to specific evidence (metrics, quotes, dates)
- Use the user's own language from their resume when describing positioning
- Defer voice/tone specifics to the `/writing-style` skill if the user has set one up

---

## Companies

> Filled in by `/process-work-history` as companies are added.

| Company | Status | Overview |
|---------|--------|----------|
