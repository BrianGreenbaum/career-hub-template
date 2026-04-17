---
name: update
description: |
  Professional update and journaling. Captures what's been happening across work, job search,
  networking, and personal life. Use when the user says "update", "recap", "what's been
  going on", "catch me up", "journal", or "log". Also prompt the user to run this if 7+ days have
  passed since the last weekly entry (check CLAUDE.md for the latest entry date).
---

# Update Skill

Capture a professional update from the user. Can cover any time period — entries are filed by
ISO week number for easy browsing.

## Process

### 1. Determine the Period

Read `CLAUDE.md` to find the latest weekly entry pointer. Calculate which weeks need coverage.
If multiple weeks are behind, cover them in one session (one entry per week, or combined if
activity was light).

### 2. Scan Recent Activity

Before asking the user anything, gather context from what's already in the system:

- `git log --oneline --since="[last entry end date]" --reverse` — what changed
- `Search/{year}/DASHBOARD.md` (if it exists) — pipeline movement
- `TODOS.md` — completed or new items

Present a summary: "Here's what I can see happened since the last update." This
saves them from repeating what's already documented and gives them a starting point.

### 3. Open-Ended Dump First

Before asking category-by-category questions, start with an open prompt:

> "Before I ask specifics — what's been going on? Just tell me whatever's top of mind since the last update. Be as detailed as you want."

Let the user talk. When they're done, summarize what you heard and note which categories are already covered vs. need follow-up.

### 4. Fill the Gaps

Now go through categories the dump didn't cover. For each, share what the scan found and ask conversationally — don't just list categories:

- **Work** — "Anything happening at work worth noting? Projects moving, team changes, decisions you were part of?"
- **Job Search** — "How's the search feeling? Any conversations or shifts in thinking that aren't captured in the pipeline?"
- **Networking** — "Talk to anyone interesting this week? Coffees, calls, new connections?"
- **Personal / Energy** — "How are you feeling about all of it? What's taking up headspace?" (Optional — skip if they seem done.)

Skip any category the user told `/onboard` they don't care about (e.g., if they're not
job-searching, skip Job Search). **Acknowledge interesting things they say** before moving to
the next topic.

### 5. Write the Entry

**Narrate what you're writing:** "Writing up your entry for Week [N] now — capturing [brief summary of what they told you]. I'll also update the weekly log index and your CLAUDE.md pointer."

Create `Weekly/{YYYY}-W{NN}.md`. Follow the format of existing entries if any exist (read a recent
one as reference). Guidelines:

- Section headers for each category
- `← [Back to Weekly Log](./README.md)` at top
- Honest, first-person tone — the user's voice, not a report
- Content seeds clearly called out so they're findable later
- Skip empty sections rather than writing "nothing this week"
- If covering multiple weeks, create separate files for each

### 6. Cross-Update

After writing the entry, update all of these:

1. `Weekly/README.md` — Add row to log table if present (most recent at top)
2. `CLAUDE.md` — Update the "Latest entry" pointer under the Weekly Professional Updates section
