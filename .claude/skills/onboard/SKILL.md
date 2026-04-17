---
name: onboard
description: |
  Main entry point for a new career-hub-template install. Interviews the user about their background, goals, and preferences, then populates CLAUDE.md and other template files with their details, generates a customized job-search skill via skill-creator, and seeds starter content. Use when the user says "onboard", "set up", "get started", "initialize", or when they've just cloned the template and haven't personalized it yet.
---

# Onboard Skill

You are helping a new user set up their career hub for the first time. This is the entry point — after this, the hub should feel personal and ready to use.

---

## Step 0: Detect State

Before starting, check whether this hub has already been onboarded:

1. Read the root `CLAUDE.md`.
2. Look for `{{placeholders}}` tokens (e.g., `{{user_name}}`, `{{current_role}}`).
3. **If placeholders exist** → first run. Proceed with the full flow.
4. **If placeholders are already replaced** → this hub has been onboarded. Ask the user:
   > "It looks like this hub has already been set up. Are you re-onboarding from scratch (this will overwrite your current CLAUDE.md), or did you want to run something else?"
   
   Only continue if they explicitly confirm.

---

## Step 1: Welcome + What This Hub Does

Open with a short, warm intro that explains *what they're setting up and why it matters*. The user needs to understand the full picture before they answer questions — otherwise the interview feels like a form instead of a setup process.

> Welcome! You're setting up a career management hub that runs on Claude Code. Let me tell you what this thing actually does, and then we'll spend about 10 minutes getting it dialed in for you.
>
> **What you're building here:**
>
> This hub is a system that helps you manage your job search, document your work history, and keep track of everything in one place. It's not just files — there are skills (commands you can run) that do real work for you:
>
> - **`/job-search`** — Searches job boards customized for your role type and industry (ATS boards, aggregators, role-specific boards, VC portfolios, and more — we'll pick which ones together during setup). Scores every role against your criteria and maintains a ranked pipeline. Run it whenever you want fresh results.
> - **`/process-work-history`** — Reads your resume, LinkedIn export, or old project docs and turns them into structured summaries organized by company. Flags gaps and suggests projects worth documenting in more detail.
> - **`/project-interview`** — An interactive conversation that captures everything about a specific project: what you did, what the challenges were, what the impact was. Produces a detailed dossier you can draw from for interviews.
> - **`/case-study`** — Turns a project dossier into an interview-ready case study outline with a presentation structure.
> - **`/update`** — A weekly check-in that captures what's been happening across work, job search, and life. Builds a log over time so you don't lose context.
> - **`/todo`** — A task board you manage from the command line. Renders as a drag-and-drop Kanban in Obsidian.
>
> **What we're about to do:**
>
> I'm going to ask you about who you are, what you're looking for, and what matters to you. The more you tell me, the better this works — don't just give me bullet points, tell me the story. Your answers get baked into the hub so that every skill already knows your background, your criteria, and your preferences.
>
> After the interview, I'll generate your customized files and show you what to do first.

Then show the roadmap with progress:

```
Onboarding Progress: ██░░░░░░░░ 0%

⬜ Profile — who you are and what you do
⬜ Job search — what you're looking for and why
⬜ Preferences — weekly journaling and other options
⬜ Review — confirm everything before I build
⬜ Generation — I create your customized hub
```

**Update the progress indicator after each section completes.** Redraw it with the completed sections checked off and the percentage updated. This gives the user a sense of where they are and what's left.

---

## Step 2: Profile Interview

Walk through these questions conversationally. Ask 1-2 at a time. **The goal is to get the user talking, not to collect form fields.** Frame questions so it feels weird to give a one-word answer.

### Asking style

- Use "Tell me about..." and "What's the story with..." instead of "What is your..."
- After the user answers, acknowledge what was interesting or surprising before moving on. This signals that the extra context was valued, which encourages more of it.
- If the user gives a short answer, follow up: "Say more about that — what does that actually look like day-to-day?" or "What's driving that?"

### Questions

**Opening:** "Let's start with the basics — what's your name, and tell me about what you do. Not just the job title, but what your actual work looks like day-to-day."

This one question should naturally pull out: name, current role, company, and a sense of what they actually do. Follow up to fill gaps:

- **Location** — "Where are you based?"
- **Experience** — "How long have you been doing this kind of work? Did you come to it from somewhere else, or has this always been the path?" (This invites the career arc story, not just "5 years.")
- **Areas of focus** — If not already clear: "What's your sweet spot — the kind of work where you feel like you're really in your element?"

### Context

After the basics, dig into the current situation:

"Tell me about where you're at right now with this job. What's working, what's not, and what's making you think about what's next?"

This one open-ended question should surface: what's good about the current role, what's frustrating, why they're considering a change, and their emotional state around it. Let them talk. Follow up on the interesting parts.

---

## Step 3: Job Search Interview

### Gate question

Ask directly: "Are you actively looking for a new role, or is this more of a 'keeping options open' situation?"

If **no** or **not yet**, skip the detailed criteria and move to Step 4. Note in CLAUDE.md that the search isn't active yet.

If **yes**, dig in. The key principle: **ask questions that surface motivation and context, not just data points.**

### Role & direction

"Tell me about what you're looking for in your next role — not just the title, but what's pulling you toward something new and what kind of place you want to end up."

This should surface: target titles, domain interests, career trajectory, and what's wrong with the current situation. Follow up to get specific:

- If they mentioned titles, confirm: "So you're targeting [X] and [Y] — would you also consider [Z], or is that a step in the wrong direction?"
- If they mentioned a domain or industry: "What draws you to that space? Is it the work itself, or more about the kind of companies in that world?"

### Location

"Are you open to relocating, or are you staying put? And what about remote — is that something you'd want, or just something you'd tolerate?"

### Compensation

"Let's talk money. What are you making now, and what do you need your next role to hit? Don't just give me a number — tell me what matters. Is it base salary, equity, total comp, something else?"

### Must-haves

"Think about what would make you turn down an otherwise good offer. What has to be true about the company or the role for you to say yes?"

### Industries and companies

"Any industries that are a hard no for you? And on the flip side — are there specific companies you're already watching or dreaming about?"

Follow up: "What about companies you'd never want to work at? Not just industries, but specific places."

### What drives you

"Tell me about your best days at work — the ones where you go home feeling like you actually did something. What were you doing?"

"And the flip side — what drains you? What kind of environment or dynamics have you learned to avoid?"

### Job board discovery & selection

After collecting role/domain preferences, **discover relevant job boards** for the user's specific role type. Don't assume — different professions have completely different board ecosystems.

1. **Run a WebSearch** for boards specific to the user's target roles and domain:
   ```
   best job boards for [target role] [year]
   [target role] job boards specialized
   [domain] jobs board site
   ```
   For example: "best job boards for accountants 2026", "product design job boards specialized", "legal jobs board site"

2. **Compile a recommended board list** organized into three categories:
   - **Always searched (universal):** ATS boards (Greenhouse, Lever, Ashby), LinkedIn, HN Who's Hiring, YC Jobs, general aggregators (We Work Remotely, Remotive if remote-eligible)
   - **Role-specific (discovered):** Boards you found that are specialized for their role type. Include a one-line description of each.
   - **Domain-specific (discovered):** Boards focused on their target industry/domain.

3. **Present the list and ask the user to review:**

   > Here's what `/job-search` will search every time you run it. I've included the standard boards plus some specialized ones for [role type]:
   >
   > **Always searched:**
   > [list]
   >
   > **Specialized for [role type]:**
   > [list with descriptions]
   >
   > **Focused on [domain]:**
   > [list with descriptions]
   >
   > A few questions:
   > - Are there any boards here you've used before and found useful? (I'll prioritize those.)
   > - Any boards you know about that I'm missing? Maybe ones specific to your field or community?
   > - Any of these you'd want me to skip? (e.g., if you know a board is low-quality or irrelevant)

4. **Record the user's choices** for use in Step 6c when generating the job-search skill:
   - Add user-confirmed role-specific boards to `{{role_specific_boards}}`
   - Add user-specified custom boards to `{{custom_boards}}`
   - Note any boards the user explicitly asked to skip

---

## Step 4: Optional Features

### Weekly journaling

> There's an `/update` skill that walks you through a short check-in every week. It captures what's been happening across work, job search, and life, and builds a log over time. Some people find it useful for keeping their head straight during a search — others don't want another thing to do. Want me to turn it on?

- **Yes** → keep the `Weekly/` folder, mention `/update` in next steps, seed a first entry stub
- **No** → delete the `Weekly/` folder, remove the weekly updates section from `CLAUDE.md`

---

## Step 5: Review & Confirm

Before generating anything, present a clear summary of everything the user told you. Organize it so they can quickly scan and confirm.

Include:
- Profile summary (name, role, company, location, experience, background)
- Job search criteria (titles, locations, comp, must-haves, domain, dream companies, skip list)
- Energizers and yellow flags
- Optional features (journaling yes/no)
- What you're about to generate (list the specific files and skills)

Ask: "Does this look right? Anything you want to change before I build?"

---

## Step 6: Generate Customized Files

**Narrate as you go.** Don't silently generate files — explain what you're creating and why it matters. The user should feel like they understand what each piece does, not just that "stuff was generated."

### 6a. Root CLAUDE.md

Narrate:
> "Starting with your CLAUDE.md — this is the most important file in the hub. It's what gives Claude context about who you are every time you open a session. I'm filling in your profile, your search criteria, and your preferences so you never have to re-explain yourself."

Read the current `CLAUDE.md` and substitute every `{{placeholder}}` token with the user's answer. The canonical token list for the root file:

| Token | Where it comes from |
|-------|---------------------|
| `{{user_name}}` | Profile interview |
| `{{user_location}}` | Profile interview |
| `{{current_role}}` | Profile interview |
| `{{current_company}}` | Profile interview |
| `{{years_experience}}` | Profile interview — use a phrase like "8 years total, 3 in PM" |
| `{{areas_of_focus}}` | Profile interview — comma-separated list |
| `{{focus_domain}}` | Profile interview — one or two words ("fintech", "AI", "climate") |
| `{{current_role_context}}` | Profile "current situation" paragraph |
| `{{active_search_summary}}` | One line from goals interview ("Actively job searching for X at Y") or "Not currently job searching" |
| `{{weekly_updates_section}}` | One of two variants based on opt-in (see the HTML comment in the template) |
| `{{current_search_year}}` | Current calendar year (e.g. `2026`) — used in folder path references |

**Worked example.** Given a user named "Alex Chen" in "San Francisco" working as "Senior PM" at "FakeCo", this block in the template:

```markdown
- **Name:** {{user_name}}
- **Location:** {{user_location}}
- **Current role:** {{current_role}} at {{current_company}}
```

becomes:

```markdown
- **Name:** Alex Chen
- **Location:** San Francisco, CA
- **Current role:** Senior PM at FakeCo
```

Do this for every token. Then write the file back. **Verify after:** grep the written file for `{{` — should return zero matches.

### 6b. Search year folder + Search CLAUDE.md

Narrate:
> "Now setting up your search pipeline. Search/[year]/ is where your job search lives — the dashboard that tracks every application, the prospects database, and the search history. I'm seeding [companies they mentioned] on your Watch List so the first `/job-search` run will check their career pages automatically."

**If the user is job searching:**

1. Create `Search/{{current_search_year}}/` folder (plus `companies/`, `searches/`, `networking/` subfolders)
2. Move `Search/CLAUDE.md` → `Search/{{current_search_year}}/CLAUDE.md`
3. In the moved file, substitute:
   - `{{current_search_year}}` → the year number (e.g., `2026`)
   - `{{target_roles}}`, `{{target_locations}}`, `{{target_comp_range}}`, `{{must_haves}}`, `{{industries_to_avoid}}`, `{{skip_list_companies}}`
   - `{{additional_preferences}}` — compose from the "energizers" and "yellow flags" answers, or the full stage/team/equity preferences
4. Create `Search/{{current_search_year}}/DASHBOARD.md`:
   ```markdown
   # Search {{current_search_year}} — Dashboard

   ← [Back to Career Hub](../../CLAUDE.md)

   **Last updated:** {today}
   **Last job search:** Not yet run

   ## Active Pipeline

   | Company | Role | Stage | Next Action | Updated |
   |---------|------|-------|-------------|---------|

   _No active applications yet. Run `/job-search` to start._

   ## Next Actions

   - [ ] Run `/job-search` to populate prospects
   ```
5. Create `Search/{{current_search_year}}/companies/prospects.md` with empty High/Medium/Watch List sections. If the user gave target companies in the goals interview, seed them into the Watch List table.
6. Create `Search/{{current_search_year}}/searches/overview.md` with an empty log table.

**If the user is NOT job searching:**

Do **not** delete the `Search/` folder. Leave `Search/CLAUDE.md` in place and add a note at the top of that file:

```markdown
> **Not yet active.** The user opted out of job search setup during onboarding.
> To activate later: re-run `/onboard` and choose "Yes" when asked if you're job searching,
> or move this file into `Search/{year}/CLAUDE.md` manually and fill in the criteria.
```

Also add a short sentence to the root `CLAUDE.md` "Active job search" section noting the hub is not currently set up for job search.

### 6c. Generate the customized job-search skill

Narrate:
> "Now building your custom job search skill. This is the engine that powers `/job-search` — it knows which job boards to search, what title variations to try, how to score roles against your criteria, and which companies to watch or skip. I'm tuning it for [target roles] in [locations], setting your comp floor at [amount], and configuring it to flag [must-haves]."

**Default: direct substitution (always works).**

1. Copy `.claude/skills/job-search-template/` → `.claude/skills/job-search/`
2. Delete `.claude/skills/job-search/TEMPLATE_README.md` (not needed in the real skill)
3. Walk every `.md` file in `.claude/skills/job-search/` (including `references/`) and substitute the tokens below. Use Read + Edit (or a small Python/shell script if many files):

   | Token | Value |
   |-------|-------|
   | `{{target_roles}}` | Comma-separated list from goals interview |
   | `{{target_locations}}` | Full location string ("NYC + Remote US", "Research Triangle + Remote US") |
   | `{{primary_location}}` | Single city for "must have office" rule |
   | `{{primary_location_slug}}` | Lowercased, hyphenated version for Built In URL (e.g., `nyc`, `boston`, `triangle`) |
   | `{{target_comp_range}}` | e.g., `$250K+ base`, `$180K-$220K base` |
   | `{{must_haves}}` | From goals interview |
   | `{{industries_to_avoid}}` | Comma-separated list |
   | `{{skip_list_companies}}` | Inline value or "None specific yet" |
   | `{{skip_list_companies_formatted}}` | Markdown sub-list(s) by category (industries, poor fit, etc.) |
   | `{{focus_domain}}` | 1-2 words ("AI", "fintech / consumer product", "climate") |
   | `{{user_background_summary}}` | 3-6 bullets composed from profile + work history |
   | `{{search_year}}` | Current year (e.g., `2026`) |
   | `{{search_title_variations}}` | Markdown bullet list of likely title variants; see below |
   | `{{role_specific_boards}}` | Markdown list of role-specific boards from job board discovery step |
   | `{{custom_boards}}` | Markdown list of any additional boards the user requested |

   **For `{{search_title_variations}}`:** derive from target roles. For example, if the user said "Senior/Staff PM at startups":
   ```
   **Primary:**
   - "senior product manager"
   - "staff product manager"
   - "product manager" (filter to Series A-C)

   **Also search:**
   - "principal product manager"
   - "group product manager"
   - "lead product manager"
   - "founding product manager"
   ```

4. After substituting, **open `references/target-companies.md`** and seed the Tier 1 / Tier 2 / Tier 3 tables with companies the user named in the goals interview.
5. **Open `references/scoring-and-fit.md`** and replace the empty "Energizers" and "Yellow flags" bullets with the user's actual answers from the goals interview.
6. **Verify:** grep the entire `.claude/skills/job-search/` folder for `{{` — should return zero matches.

**Optional: skill-creator polish pass.**

After direct substitution is complete, you can optionally hand off to the `skill-creator` skill for a review/polish pass. Use the Skill tool with `skill: "skill-creator"` and ask it to review the generated `.claude/skills/job-search/` folder for consistency and suggest improvements. This is optional — direct substitution is sufficient for a working skill.

**Known uncertainty:** whether `skill-creator` can be invoked from *inside* a running `/onboard` skill hasn't been verified. If the Skill tool call fails or produces unexpected behavior, skip the polish pass and tell the user they can run `skill-creator` themselves as a follow-up: "The job-search skill is generated and working. If you'd like a polish review, run `skill-creator` against `.claude/skills/job-search/` as a follow-up."

---

## Step 7: Seed Starter Content

### 7a. TODOs

Narrate:
> "Seeding your task board with your first three actions. The most important one is importing your work history — that gives you structured ammunition for interviews and helps the job search skill understand your background better."

Seed **at most 3** starter tasks into `TODOS.md` — enough to signal what to do first without overwhelming a brand-new board. Order by immediate next action.

If the user is job searching, use these three:

```markdown
## Not Started

- [ ] 🔴 Run `/process-work-history` to scan your resume and build timeline (drop files into `Work-History/inbox/` first) #work
- [ ] 🟡 Do a `/project-interview` for your current role — captures your most recent work while it's fresh #work
- [ ] 🟡 Run `/job-search` to populate the prospects database #search
```

If the user is NOT job searching, use these two (skip the job-search line):

```markdown
## Not Started

- [ ] 🔴 Run `/process-work-history` to scan your resume and build timeline (drop files into `Work-History/inbox/` first) #work
- [ ] 🟡 Do a `/project-interview` for your current role — captures your most recent work while it's fresh #work
```

Do **not** seed "run `/update` weekly" as a TODO — weekly updates are naturally recurring and the `/update` skill will prompt when due.

### 7b. First Weekly entry stub (only if weekly journaling opted in)

Narrate:
> "Creating your first weekly log entry — just a stub to mark that you set up the hub this week. When you run `/update` later, it'll fill in with real content."

Create `Weekly/{YYYY}-W{NN}.md` for the current ISO week:

```markdown
← [Back to Weekly Log](./README.md)

# Week {NN} — {Month Day} to {Month Day}

**Started this week:** Set up the career hub, onboarded, customized the job-search skill.

## Next actions
- Run `/process-work-history` to bring in past roles
- Run `/project-interview` for current role

Run `/update` any time to capture a full entry.
```

Update `Weekly/README.md` to add a row referencing the new entry.

### 7c. Update root README.md

Narrate:
> "Last thing — updating the README with your name so the hub feels like yours."

The template ships with a `README.md` that's mostly install-guide content. Read it, substitute `{{user_name}}` (and any other user-facing tokens you find), and write it back. Do not aggressively rewrite — the README is meant to stay close to the template's install guide even after onboarding.

---

## Step 8: Next Steps Summary

Close with a clear summary of what you built and what to do next. **Be specific about what each next step does and why it matters** — don't just list commands.

```
Here's what I set up:

- CLAUDE.md — Your profile and preferences, loaded every time you open the hub
- .claude/skills/job-search/ — A custom search skill that knows your target roles,
  locations, comp range, and which companies to watch or skip
- Search/{year}/ — Your job search pipeline (dashboard, prospects, search history)
- TODOS — Three starter tasks to get you moving
[- Weekly/{week}.md — First journal entry stub (if opted in)]

What to do next (in this order):

1. Drop your resume into Work-History/inbox/ and run /process-work-history
   → This scans your resume and builds structured summaries by company.
     It's the foundation — other skills reference this data.

2. Run /project-interview for your current role
   → An interactive conversation that captures everything about your best
     project. Produces a dossier you can draw from in interviews.

3. Run /job-search to pull in opportunities
   → Searches 15+ job boards, scores roles against your criteria, and
     populates your prospects database. Run it whenever you want fresh results.

The hub is yours now — edit CLAUDE.md, tweak skills, add files.
Everything is just markdown.
```

---

## Failure & Recovery

- If any step errors out (file not found, substitution fails), tell the user clearly what broke and what they can do to fix it manually
- If the user interrupts mid-interview, save whatever answers you have to `.claude/skills/onboard/partial-answers.md` so they can resume next time
- On re-run, check for `partial-answers.md` first and offer to pick up where they left off
