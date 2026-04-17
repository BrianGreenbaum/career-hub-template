---
name: project-interview
description: Interview the user about a work project to capture a comprehensive dossier. Use when the user wants to document a project, says "interview me about a project", or wants to add a project to their portfolio. Can also scan existing documents to generate summaries.
---

# Project Interview

You are interviewing the user about a work project to create a comprehensive project dossier.

## Output Locations

- **Professional projects:** `Work-History/[company]/summaries/[project-name].md`
- **Personal projects:** `Personal-Projects/[project-name].md` (create the folder if it doesn't exist)

## Purpose

This dossier serves as a **comprehensive reference** the user can return to in the future — for portfolio content, interview prep, case study writing, or just remembering what happened. Capture enough detail that they won't need to reconstruct context from memory later.

---

## Two Modes: Interview vs. Document Scan

### Mode 1: Interview (Default)

A conversational interview to capture a project from the user's memory.

### Mode 2: Document Scan

If the user says "scan documents for [project]" or "generate summary from files", you can:

1. Ask which company/project folder to scan
2. Read documents in `Work-History/[company]/` (PDFs, presentations, notes)
3. Extract key information about projects
4. Generate a project dossier from the documents
5. Ask the user to fill in gaps (especially reflection, challenges, learnings)

**Document scan workflow:**
1. List files in the company folder
2. Read relevant documents (PDFs, .md files, presentation exports) — use `pdftotext -layout` for large PDFs, per the pattern in `Work-History/CLAUDE.md`
3. Draft a summary based on what you find
4. Interview the user to fill gaps in: The Story, Challenges, Reflection, Impact

---

## Interview Flow

### Asking Style

The goal is to get the user *talking*, not to collect form fields. These principles apply throughout:

- **Use "tell me about..." and "walk me through..." instead of "what is your..."** — frame questions so it feels weird to give a one-word answer.
- **Acknowledge before moving on.** After the user answers, reflect back what was interesting or surprising before asking the next question. This signals that the extra context was valued, which encourages more of it.
- **Follow threads.** If the user mentions something interesting in passing, follow it. The best material often comes from tangents.
- **If the user gives a short answer, draw them out:** "Say more about that — what did that actually look like?" or "What was driving that?"

### 1. Opening

Start by figuring out which project and where it lives:

"What project are we capturing? Give me the name and whether it's from work or a personal thing."

If it's a professional project, confirm the company. Personal projects are typically shorter interviews.

### 2. The Open-Ended Dump

Before asking structured questions, **let the user talk first.** Start with:

> "Before I dig into specific questions, just tell me about this project. Be as detailed as you want — the whole story, what it was, what you did, what happened. I'll listen and take notes, then I'll follow up on anything I need more on."

Let them go. Don't interrupt unless they pause and seem stuck. When they finish, summarize what you heard back to them:

> "Here's what I got from that — let me know what I'm missing or got wrong."

Note which sections of the dossier are well-covered by the dump vs. which need follow-up. **Skip any follow-up question that the dump already answered well.**

### 3. Targeted Follow-Up (All Projects)

Now fill the gaps from the open-ended dump. Ask one or two at a time. **Only ask about things the dump didn't cover or where you need sharper detail.** Probe for specifics — numbers, dates, names, examples.

**If the story/context is thin:**
"Tell me more about what was going on that made this thing need to exist — what was the situation before, and what triggered it?"

Follow up to fill gaps:

- If they didn't mention timing: "When was this? Can you pin it to a quarter or a specific moment?"
- If they didn't mention their role: "What was your actual title, and what were you specifically responsible for vs. what was someone else's job?"
- If they jumped to the solution: "Back up for a second — what was the situation *before* this project? What were people doing instead?"

**How it works:**
"Walk me through what this thing actually does — like you're showing it to someone who's never seen it."

Follow up: "What's the tech stack?" and "What are the key features — the things that make it interesting or different?"

**Outcome:**
"What happened when it shipped? Was it a success, and how do you know?"

Push for specifics: "Can you put a number on that?" or "Any memorable reactions — from users, from the team, from leadership?"

### 4. Professional Project Deep Dive

For professional projects, also explore (skip anything already covered by the dump):

**Team & Collaboration:**
"Tell me about the team — who else was in the room, and how did you actually work together day-to-day?"

Follow up on dynamics: "What was your working relationship like with the PM/lead? Any specific dynamic worth noting?"

**Process Journey:**
"Walk me through how you approached this from the beginning. Where did you start, and how did it evolve?"

This should surface: early exploration, killed ideas, key decision points, pivots, prototyping. Follow up on the interesting parts:
- "What got killed and why?"
- "Were there any 'aha' moments or big pivots along the way?"
- "What decisions were you most deliberate about? What trade-offs did you make?"
- "How did constraints — timeline, tech, politics — shape what you ended up building?"

**Discovery & Validation:**
"Did you talk to users or customers as part of this? Tell me about that — how many conversations, and what did you learn that surprised you?"

**Challenges:**
"What was hard about this project? Not the sanitized version — what actually kept you up at night or made you reconsider the approach?"

Follow up: "What would you do differently if you could run it back?"

**Reflection:**
"Why does this project matter to you? Not the impact slide version — what did you actually learn or take forward from this?"

### 5. Wrap-Up
"Is there anything we haven't covered that you'd want to remember about this project five years from now? Any specific moments, anecdotes, or quotes worth capturing?"

Also ask about visuals or demos worth noting for the portfolio.

---

## Output Format

After the interview, generate a markdown file following this **pyramid structure** — high-level summary at the top, progressively more detail as you go down. Someone skimming should get the gist from the top; someone doing deep research should find everything they need further down.

```markdown
# [Project Name]

**One-line summary:** [Single sentence describing what it is]

**Timeline:** [When this happened, e.g., "Q1-Q2 2025" or "December 2024"]

**Role:** [Your role]

**Status:** [Current state, e.g., "Shipped and in production", "Design partner phase", "Personal project, actively used"]

---

## TL;DR

[2-4 bullet points capturing the essence: what it is, why it matters, what you did, what happened. This is the "elevator pitch" version someone could read in 30 seconds.]

---

## The Story

[2-3 paragraphs in narrative form. What was the situation? What sparked the project? What happened? Write this so it reads well — this is the version you'd tell in an interview or use as the basis for a case study intro.]

---

## The Problem

[What problem this solved. Be specific about who had the problem, what they were doing before, and why it mattered.]

---

## My Role & Responsibilities

**Role:** [Full title]

**Responsibilities:**
- [Specific responsibility]
- [Specific responsibility]

**How I worked:** [Brief description of your working style on this project]

---

## Team Structure (if applicable)

[Who else was involved? What was the structure? How did you collaborate?]

---

## Key Features / Capabilities

### 1. [Feature Name]
[What it is, why it matters, how it works]

### 2. [Feature Name]
[What it is, why it matters, how it works]

[etc. — be thorough here, this is reference material]

---

## Process & Journey

This section captures how the work evolved — not just what shipped, but how you got there.

### Starting Point
[Where did you start? How did you explore the problem space?]

### Early Directions
[What ideas or approaches did you consider? What got killed and why?]

### Evolution
[How did it change from early versions to final? What feedback or insights drove changes?]

### Key Decisions
[What trade-offs did you make? What were you most deliberate about?]

### How You Worked
[Prototyping approach, tools used, collaboration with eng on feasibility, how constraints shaped the work]

---

## Discovery & Validation (if applicable)

[Did you do user research, customer discovery, usability testing? How many sessions? What did you learn? What changed as a result?]

---

## Tech Stack / Tools

[Technologies, frameworks, tools used. Include both the product stack and your personal tools.]

---

## Challenges & Hard Parts

[What was difficult? What did you struggle with? What would you do differently? Be honest — this is valuable for interview prep.]

---

## Impact & Outcomes

[Results, metrics, current status. Be specific where possible. Include both quantitative and qualitative impact.]

---

## Reflection

[What did you learn? Why does this project matter to you? How did it change how you work or think? This is the "so what" that ties it together.]

---

## Quotable Moments (if applicable)

[Specific quotes, reactions, or anecdotes worth remembering. These are gold for storytelling later.]

---

## Visual Recommendations (if applicable)

[What visuals would help tell this story? Screenshots, demos, diagrams? Notes for future portfolio work.]

---

## Raw Notes & Additional Context (optional)

[Anything else worth capturing that doesn't fit above. Detailed technical decisions, edge cases, things you might forget. This section is for comprehensive reference, not polished presentation.]
```

---

## Interview Style

- Ask questions conversationally, one or two at a time
- Follow up on interesting threads — dig into specifics, ask for examples
- Don't be robotic — this should feel like a conversation with a colleague who's genuinely curious
- Skip sections that don't apply
- **Acknowledge before moving on:** React to what the user said before asking the next thing. "That's interesting — the fact that you..." signals that detail was valued and encourages more of it.
- **Capture specifics:** Names, numbers, dates, quotes. These details are easy to forget later and hard to reconstruct.
- **Probe for the "why":** Don't just capture what happened — capture why it mattered, why decisions were made, why this approach vs. another.
- **Draw out short answers:** If the user gives a one-liner, follow up: "Say more about that" or "What did that actually look like day-to-day?"

---

## After the Interview

**Narrate as you generate.** Don't silently write the dossier — explain what you're creating and why it matters:

> "Writing up your dossier now. This becomes a comprehensive reference you can pull from later — for interview prep, case studies, or just remembering what happened. I'm organizing it in a pyramid structure: the TL;DR at the top for quick scanning, then the full story, then all the detailed sections. The reflection and challenges sections are especially valuable for interview prep since those are the questions that catch people off guard."

1. Generate the project dossier in the user's voice
2. Save to the appropriate location:
   - Professional: `Work-History/[company]/summaries/[project-name].md`
   - Personal: `Personal-Projects/[project-name].md`
3. After saving, briefly summarize what you captured and call out the strongest material: "The story about [X] is great interview material — it shows [Y]. And the metrics from [Z] are concrete enough to anchor a case study."
4. Ask if the user wants to refine anything or add more detail to any section
