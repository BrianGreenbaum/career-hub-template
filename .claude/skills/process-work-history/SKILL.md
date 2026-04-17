---
name: process-work-history
description: |
  Process the user's work history from source documents (resumes, LinkedIn exports, performance reviews, old project writeups, presentation PDFs) into structured per-company summaries. Identifies gaps and offers to fill them via /project-interview. Use when the user says "process my work history", "import my resume", "scan my work docs", or "find gaps in my work history". Re-runnable — can be invoked any time the user drops new files or wants to check for gaps.
---

# Process Work History

This skill turns raw career artifacts into structured Work-History summaries and identifies gaps to interview the user on.

It is **re-runnable** — the user can invoke it any time they drop new files into the work history folder, or months later to do a gap check.

---

## Process Overview

1. **Tell the user where to put files** (if they haven't already)
2. **Ask which folder to scan**
3. **Inventory the files**
4. **Extract company + project data in batches**
5. **Write / update summaries** following the `Work-History/CLAUDE.md` pattern
6. **Identify gaps** (missing years, companies with no summaries, projects with no narrative)
7. **Offer to fill gaps** via `/project-interview`

Read `Work-History/CLAUDE.md` first — it has the processing pattern and output templates that this skill follows.

### Narration

**This skill does a lot of file processing.** Narrate each major step so the user understands what's happening and why:

- When scanning files: "Found [N] files — [list types]. I'll start with your resume since that's the highest-value artifact for building the timeline."
- When extracting: "Reading your resume now — I'm pulling out companies, dates, titles, and key bullet points. I'll preserve your own language from the resume bullets since that's how you've already positioned this work."
- When writing summaries: "Creating a structured summary for [Company]. This organizes everything from the resume + any other docs into a format that other skills can reference — the job search skill uses this for fit assessment, and the case study skill draws from it."
- When building the timeline: "Building your canonical work timeline — this is the master reference for your career arc."
- When identifying gaps: "Now checking for gaps — missing years, companies with no detail, projects mentioned but not captured."

---

## Step 1: Where Do the Files Live?

Ask the user where their source documents are. Common patterns:

- Already in `Work-History/[company]/` — they've organized per-company already
- In a single `Work-History/inbox/` folder — dumped together, unsorted
- In an external folder they'll tell you about (e.g., `~/Downloads/career-docs/`)
- Nowhere yet — they need to gather files

If they haven't gathered anything, give them clear instructions:

> To get the most out of this skill, drop the following into `Work-History/inbox/` (I'll create the folder if it doesn't exist):
>
> - Your current resume (PDF, .docx, or .md)
> - Your LinkedIn profile export (Settings → Data Privacy → Get a copy of your data → "Want something in particular?" → pick at least "Profile")
> - Any performance reviews you have from past jobs
> - Old project writeups, case studies, or presentation PDFs
> - Portfolio docs or design files (I'll extract text where possible, otherwise note them for later)
>
> Once they're in, come back and run `/process-work-history` again and I'll scan them.

If they already have files in per-company folders, skip this and move to Step 2.

---

## Step 2: Inventory the Files

Once the user confirms files are in place:

1. **List the source folder** — use Glob or Bash `ls`
2. **Categorize each file:**
   - `.pdf` → process with `pdftotext -layout` (see `Work-History/CLAUDE.md`)
   - `.md`, `.txt` → read directly
   - `.docx` → try `pandoc` or `textutil` if available; otherwise note as "needs manual extraction"
   - Images (`.png`, `.jpg`) → optional, use vision to scan for text if the user wants
   - Design files (`.fig`, `.sketch`) → Skip, note as "design file, not processable"
   - Videos / audio → Skip
3. **Create or update `SOURCE_TRACKER.md`** in the target folder with status for each file

---

## Step 3: Extract in Batches

Process 3-6 related files at a time. For each batch:

1. Read / extract the text
2. Identify:
   - **Company name** and dates
   - **Role / title**
   - **Projects** mentioned (with dates where possible)
   - **Metrics** (revenue, adoption, growth %, anything quantifiable)
   - **Quotes / feedback** worth saving for interview stories
   - **Key decisions or turning points** the user led
3. For each company found, ensure a folder exists: `Work-History/[company]/summaries/`
4. Create or update `Work-History/[company]/summaries/[company]-overview.md` following the template in `Work-History/CLAUDE.md`
5. If a project is substantial enough to deserve a deep-dive, create `Work-History/[company]/summaries/[project].md` and link it from the overview

**Handling the resume specifically:** The resume is the highest-value artifact. Process it first in its own batch. Extract:
- Full company list with dates (this becomes the canonical timeline)
- Role / title for each
- Top 2-3 bullet points per role (these are the user's own positioning language — preserve them verbatim)
- Any quantifiable metrics

---

## Step 4: Build the Timeline

Once the first batch is processed, construct a **canonical timeline** from the resume + LinkedIn data. Save it to `Work-History/timeline.md` or display in conversation.

```markdown
# Work Timeline

| Dates | Company | Role | Notes |
|-------|---------|------|-------|
| 2024-01 – present | [Current Company] | [Current Role] | |
| 2020-03 – 2023-12 | [Previous Company] | [Previous Role] | |
| ... | ... | ... | |
```

Reverse chronological. Flag any gaps (months or years with no entry) visibly in the Notes column.

---

## Step 5: Identify Gaps

After the initial pass, do a gap analysis:

1. **Timeline gaps** — date ranges between companies with no coverage. Flag these and ask the user: sabbatical? Freelancing? Job search? Personal project?
2. **Companies with no detail** — a company appears in the resume but there's no `Work-History/[company]/summaries/[company]-overview.md` yet. Needs a summary.
3. **Projects mentioned but not detailed** — the resume says "Led redesign of onboarding, 40% activation lift" but there's no project deep-dive. Candidate for `/project-interview`.
4. **Missing metrics** — a project is described but no numbers. Ask if the user remembers any.
5. **No recent entries** — the most recent company has no current-state section or recent project details.

Present the gaps as a prioritized list:

> Here's what I found and what's missing:
>
> ✅ **Covered well:**
> - [Company A] — resume entry processed, 3 project deep-dives exist
> - [Company B] — overview exists with metrics
>
> ⚠️ **Needs a deep-dive:**
> 1. [Company C] — [Project name] — mentioned in resume ("Led X"), no dossier yet
> 2. [Company D] — [Project name] — has short description, no outcomes captured
>
> ❌ **Missing entirely:**
> 1. [Company E] — [Dates] — appears in LinkedIn but no resume bullet or docs
> 2. Timeline gap: 2019-06 to 2020-02 — no entry
>
> Want to fill any of these now? I can run `/project-interview` on each, or you can point me at more source docs.

---

## Step 6: Offer to Fill Gaps

For each gap the user wants to fill:

1. **Project gap** → invoke `/project-interview` with the company + project name as context
2. **Company gap** → start a lightweight overview interview (just the basics: dates, role, what you did, key projects). Then offer `/project-interview` for the notable projects.
3. **Timeline gap** → ask what was happening during that period and capture a short note in `timeline.md`

---

## Re-running the Skill

When the user re-runs `/process-work-history`:

1. Re-inventory the source folder — flag any new files since last run
2. Check `SOURCE_TRACKER.md` to see what's already been processed
3. Process new files only (skip Done entries)
4. Re-run gap analysis — gaps may have been filled by `/project-interview` runs since the last scan
5. Present updated gap report

---

## Interview Style for Gap Filling

When interviewing the user to fill a gap, keep it light unless they want to go deep:

- Confirm the basics (company, dates, role, 1-line description of what the company does)
- Ask for 2-3 most notable projects or outcomes
- For each, ask: "Want me to do a full `/project-interview` on this, or is a short blurb enough for now?"

Let the user decide the depth. Not every past job needs a full dossier.

---

## Output Location Summary

- Canonical timeline: `Work-History/timeline.md`
- Per-company overviews: `Work-History/[company]/summaries/[company]-overview.md`
- Source tracker per company: `Work-History/[company]/summaries/SOURCE_TRACKER.md`
- Project deep-dives: `Work-History/[company]/summaries/[project].md`
- Source files: `Work-History/inbox/` or per-company folders (git-ignored)
