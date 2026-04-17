---
name: case-study
description: Build a case study presentation outline and companion dossier from an interactive interview. Use when the user says "create a case study", "case study outline", "build a case study", or wants to prep a project presentation for interviews.
args:
  project: Project name or company (optional — skill will ask if not provided)
  source: Path to existing dossier or documents to scan first (optional)
---

# Case Study Builder

You are helping the user build a case study presentation for job interviews. The output is a slide-by-slide outline they can build from in their slide tool of choice, plus a companion dossier with deeper detail, talking points, and anticipated Q&A.

This is a **single-project** skill — one case study per run. Each presentation starts with a personal intro section.

---

## Output Location

Save all files to `Portfolio/case-studies/[project-name]/`:
- `outline.md` — Slide-by-slide presentation outline
- `dossier.md` — Companion reference document
- `raw-notes.md` — Running interview transcript and notes (updated every turn)

Use a kebab-case folder name based on the project.

---

## Raw Notes — Continuous Capture

Throughout the interview (Phase 2), maintain a `raw-notes.md` file that captures everything the user shares. **Update this file after every conversational turn** — don't wait until the end.

### Format

```markdown
# [Project Name] — Raw Interview Notes

**Started:** [date]
**Last updated:** [date/time of latest update]

---

## Session Notes

### [Timestamp or turn indicator]

**Topics covered:** [brief list]

**Raw capture:**
[Organized summary of what the user said — not a verbatim transcript, but close. Preserve specific details, numbers, names, anecdotes, and their own language. Group by topic if they covered multiple things.]

**Key quotes / phraseable moments:**
[Anything that stood out as particularly quotable or slide-worthy]

**Visual / artifact callouts:**
[Anything the user mentioned wanting to show, demo, or highlight visually]

**Open threads:**
[Things the user said they'd come back to, or areas that need follow-up]
```

### Rules
- **Capture everything.** Raw notes are cheap — better to have too much than too little.
- **Preserve the user's language.** Don't clean up their phrasing into corporate-speak. Their natural voice is the voice of the presentation.
- **Flag visual callouts separately.** These feed directly into slide visual recommendations.
- **Track open threads.** Use these to guide follow-up questions in Phase 2B.
- **Update incrementally.** Append new sections after each turn — don't rewrite earlier sections.

---

## Phase 1: Setup & Source Gathering

Before the interview, gather context:

1. **Ask what project** this case study is for (if not provided via args)
2. **Check for existing dossiers** — look in `Work-History/[company]/summaries/` for relevant project summaries. If one exists, read it first and use it as context for the interview.
3. **Ask about source material** — "Do you have any existing presentations, PDFs, or case studies I should reference?" Also check `Portfolio/case-studies/` for prior versions.
4. **If a `source` arg was provided**, read that file first.
5. **Ask about the target audience** — "Who will you be presenting this to?" (e.g., "design team at [company]", "VP of product at [company]"). This shapes emphasis:
   - Design-heavy audience → more process, rationale, craft details
   - Product/leadership audience → more strategy, impact, cross-functional collaboration
   - Mixed/hiring panel → balanced, emphasize breadth of contribution

If source material exists, read it all before starting the interview. Use it to skip questions you already have answers for, and to ask sharper follow-ups.

---

## Phase 2: Story Capture & Interview

This phase has two parts: an open-ended storytelling pass, then targeted follow-ups.

### Part A: "Tell me everything"

Start by letting the user dump everything they know. Say something like:

> "Before I dig into specific questions, just tell me about this project. Be as detailed as you want — the whole story, what it was, what you did, what happened, what you're proud of. I'll listen and take notes, then follow up on anything I need more on."

Let them go unstructured. Don't interrupt with clarifying questions unless they pause or ask. If source material was loaded in Phase 1, you already have context — use it to follow along and note gaps, but don't redirect them.

After they finish (or say they're done), summarize what you heard back to them in a few bullets:
- "Here's what I got from that — let me know what I'm missing or got wrong."
- Note which sections of the case study are well-covered vs. need more detail.

### Part B: Targeted follow-ups

Now fill the gaps. Ask conversationally, 1-2 questions at a time. **Only ask about things the dump didn't cover or where you need sharper detail.** Skip anything already well-covered. Acknowledge what was interesting from the dump before asking follow-ups.

**Company Context** *(skip if already covered or well-known company)*
"Quick one — can you give me a sentence on what [company] does and who the users are? Just so the audience has context."

**Problem & Background** *(if thin from the dump)*
"Tell me more about what the situation looked like *before* this project. What were people doing, and what was the specific moment or data point that triggered this work?"

**Process & Methodology** *(flexible — adapt to the actual process)*
"Walk me through how you actually approached this — not the clean version, but what it really looked like. How did you explore the problem space, what ideas got killed, and what were the key decision points along the way?"

Follow up on specifics: constraints that shaped the solution, how you worked with the team, any pivots or surprises.

**Solution & Key Features**
"Walk me through what shipped — the key features and decisions. For the ones you're most proud of, tell me *why* you made that choice vs. the alternatives."

**Validation & Insights**
"Did you validate the direction along the way? Tell me about what you learned from users, testing, or feedback — especially anything that surprised you or changed the plan."

**Post-Release & Impact**
"What happened after launch? How did you measure success, and what were the results?"

If no hard metrics: "If you don't have clean numbers, that's fine — what about usability evidence, stakeholder reactions, user quotes, adoption data? What would you measure if you could?"

Follow up: "Any unexpected outcomes? Those are often the best stories."

**Reflection**
"Looking back — what did you learn, and what would you do differently? Not the polished answer, the real one."

**Wrap-Up**
"Any specific moments, anecdotes, or quotes worth highlighting? And what visuals do you have — screenshots, design files, before/after comparisons?"

---

## Interview Style

- Ask questions conversationally, 1-2 at a time
- Follow interesting threads — dig into specifics, ask for examples
- Don't be robotic — this should feel like a good conversation with a colleague who's genuinely curious
- Skip sections that don't apply or are already well-covered by the open-ended dump or source material
- **Acknowledge before moving on:** React to what the user said before asking the next thing. "That's a great story — the part about [X]..." signals that detail was valued and encourages more of it.
- **Draw out short answers:** If the user gives a one-liner, follow up: "Say more about that" or "What did that actually look like?"
- **Probe for specifics:** Numbers, dates, names, quotes. "How many customer calls?" not just "Did you do research?"
- **Probe for the "why":** Why this approach vs. another? Why did that decision matter?
- **Probe for the user's unique role:** What wouldn't have happened without them? Use "I" not just "we."
- **Look for tension and payoff:** What was hard, what was surprising, what changed — these make good slides

---

## Phase 3: Workshop the Structure

Before writing the full outline, **propose a structure and iterate with the user**. Don't jump straight to generating slides.

1. **Propose a section outline** — Based on the interview, recommend which sections to include, roughly how many slides each, and the narrative arc. Present it as a numbered list, not full slide details yet. Example:

   > Here's what I'm thinking for the structure:
   > 1. Personal Intro (2-3 slides) — title, career timeline, unique skillset
   > 2. What is [Company]? (2 slides) — company context, users
   > 3. The Problem (3 slides) — discovery, what you heard, hypothesis
   > 4. The Process (2 slides) — approach, timeline
   > 5. Design (4 slides) — sketches, wireframes, reviews, key decisions
   > 6. Validation & Insights (3 slides) — testing, key insights
   > 7. Results (3 slides) — positive, negative, unexpected
   > 8. Reflection (1 slide) — takeaways
   >
   > Total: ~20 slides, ~18 minutes. What would you change?

2. **Include a table of contents slide** — A TOC slide after the intro section helps the audience know what's coming. Recommend one unless the deck is very short.

3. **Recommend section dividers** — Dark/colored divider slides between major sections help pacing. Suggest where to place them.

4. **Iterate** — The user may want to reorder, merge, split, add, or remove sections. They may have a specific vision for the narrative arc. Workshop until they're happy with the skeleton.

5. **Only proceed to full outline after the user approves the structure.**

---

## Phase 4: Output Generation

After structure approval, generate both documents.

### Document 1: `outline.md` — Slide-by-Slide Presentation Outline

Target length: **15-20 minutes** per project (roughly 18-25 slides total, but can go higher if using progressive reveal or build slides).

Use the approved structure. Adapt section lengths based on what's interesting — don't pad weak sections or compress strong ones.

```markdown
# [Project Name] — Case Study Outline

**Target audience:** [who this is tailored for]
**Estimated length:** [X] minutes, [Y] slides

---

## Mini Outline

[One line per slide, nested under section headers with timing. Section dividers shown in italics. This gives the user a scannable view of the full structure at a glance.]

**Section Name** (~X min)
1. Slide title
2. Slide title
3. *Section Divider*
4. Slide title

---

## Personal Intro (~1-2 min, 2-3 slides)

### Slide 1: Title
- **Title:** [Your name]
- **Content:** [Your current title / tagline]
- **Visual:** Clean title card, photo optional
- **Layout:** Centered text, minimal
- **Speaker note:** Brief, warm intro

### Slide 2: Career Overview
- **Title:** [Headline that frames your background]
- **Content:** Career timeline showing the arc of your experience
- **Visual:** Timeline graphic
- **Layout:** Full-width timeline
- **Speaker note:** Brief narrative of your trajectory

### Slide 3: What Makes You Different (optional)
- **Title:** [Your differentiator]
- **Content:** 2-column layout highlighting your unique combination of skills
- **Visual:** Clean two-column layout
- **Layout:** Text-focused, minimal
- **Speaker note:** Bridge to the case study — "Let me show you what this looks like in practice..."

---

## Company Context (~1 min, 1-2 slides)

### Slide [N]: What is [Company]?
- **Title:** [Company name]
- **Content:** 1-2 bullets on what the company does, who the users are
- **Visual:** Product screenshot or logo + product UI
- **Layout:** Text left, image right
- **Speaker note:** Keep this brief — just enough context

---

## The Problem (~2-3 min, 2-3 slides)

### Slide [N]: The Situation Before
- **Title:** [Headline that captures the pain]
- **Content:** What was broken/missing/painful
- **Visual:** Screenshot of the old state, or a data chart showing the problem
- **Speaker note:** Set up the tension — why should the audience care?

### Slide [N]: The Trigger
- **Title:** [What made this project happen]
- **Content:** The specific moment, data point, or customer pain
- **Speaker note:** This is the "inciting incident" of the story

### Slide [N]: My Role & Hypothesis
- **Title:** [Your role and initial direction]
- **Content:** What you were brought in to do, initial hypothesis
- **Speaker note:** Be specific about what you owned

---

## Process & Discovery (~4-5 min, 4-6 slides)

[Flexible structure — adapt to the actual project. Each slide should have:]

### Slide [N]: [Title]
- **Title:** [Descriptive headline]
- **Content:** Key points (2-3 bullets max)
- **Visual:** Artifact — early exploration, sketch, research finding, killed idea, competitive analysis
- **Layout:** [varies — image-heavy slides work well here]
- **Speaker note:** [What to say]

[Prioritize:]
- Early explorations and killed ideas (what you didn't do is as interesting as what you did)
- Key decision points and pivots
- Anything unique about your process
- How constraints shaped the solution

---

## The Solution (~4-5 min, 4-6 slides)

[Marketing-style feature walkthrough. Each slide:]

### Slide [N]: [Feature Headline]
- **Title:** [Benefit-oriented headline, not feature name]
- **Content:** 1-2 bullets — what it is and why this approach
- **Visual:** Product screenshot, UI mockup, or video recommendation
- **Layout:** [Image-forward — full-bleed, image left/right, etc.]
- **Speaker note:** Design rationale — why this vs. alternatives

[Focus on:]
- Key decisions and their rationale
- Show the shipped product, not just the source file
- Lead with the most impressive/interesting feature

---

## Impact & Results (~2-3 min, 2-3 slides)

### Slide [N]: Results
- **Title:** [Impact headline]
- **Content:** Metrics, data, or qualitative evidence
- **Visual:** Data visualization, chart, or quotes
- **Layout:** [varies — big numbers work well]
- **Speaker note:** If hard metrics aren't available, use: usability evidence, stakeholder quotes, engineering efficiency gains, adoption data

### Slide [N]: Iteration & Learning
- **Title:** What happened after launch
- **Content:** Feedback loop, iteration, ongoing impact
- **Speaker note:** Shows you care about outcomes, not just shipping

---

## Reflection (~1 min, 1 slide)

### Slide [N]: Takeaways
- **Title:** What I learned / what I'd do differently
- **Content:** 2-3 key takeaways
- **Visual:** [optional — clean text slide]
- **Layout:** Minimal text, plenty of space
- **Speaker note:** End with forward-looking energy — what you're taking into future work
```

**Per-slide format — every slide includes:**
- **Title** — Headline for the slide (benefit-oriented, not generic)
- **Alt title** — A super basic, generic version of the title. Having both options gives the user flexibility when actually building slides.
- **Content** — Key talking points (not a script, not a paragraph)
- **Visual** — Recommended image, screenshot, video, or diagram
- **Layout** — Choose from the layout catalog below. Use the layout name exactly.
- **Speaker note** — Brief reminder of what to say and why this slide matters

---

### Slide Layout Catalog

Use these layout names in the **Layout** field. These map well to a common Figma Community template style ("Light slides") many people use for building decks. Layouts can be mapped to any equivalent slide template.

**Title & Section Layouts:**
- `Deck Title` — Title + subtitle, bottom-left aligned. For the opening slide.
- `Section Title (centered)` — Large centered title only. For section dividers.
- `Section Title + Description (left)` — Title + description text, left-aligned.
- `Section Title + Description (centered)` — Title + description text, centered.
- `Section Title + Image` — Image area top, title + description bottom-left.

**Text-Heavy Layouts:**
- `Highlight` — Single bold word/phrase on the left, longer description on the right. For a key insight or quote.
- `Simple List (stacked)` — Title + 3 items stacked vertically with descriptions.
- `Two Columns` — Title + 4 items in a 2x2 grid with descriptions.
- `Simple List (3-col)` — Title + 3 items in a horizontal row with descriptions.
- `Simple List (4-col)` — Title + 4 items in a horizontal row with descriptions.
- `Principles (cards)` — 3 colored cards with labels and descriptions. For values/principles/pillars.

**Image + Text Layouts:**
- `Header + Image (right)` — Header + description on the left, large image on the right.
- `Subtitle + Header + Image (right)` — Subtitle, header, description bottom-left, image on right.
- `Subtitle + Header + Image (left)` — Same but image on the left side.
- `Full Image + Caption` — Full-width image with caption text below.
- `Image with Description (2-col)` — 2 images side-by-side, each with a title and description below.
- `Image with Description (3-col)` — 3 images in a row, each with a title and description below.

**Metric / Data Layouts:**
- `Big Metric` — Large XX% number with supporting description text below.
- `Key Metrics (stacked)` — Title + 3 metrics stacked vertically, each with a description.
- `3 Column Metric` — 3 large numbers in columns with descriptions.
- `Metrics (2x2)` — Title + description on left, 4 metrics in a 2x2 grid on right.

**Diagram Layouts:**
- `Timeline` — Horizontal timeline with milestones and descriptions.
- `Overlaps` — Concentric/nested circles showing related concepts.
- `2x2 Matrix` — Quadrant chart with labeled axes and positioned items.
- `Venn Diagram` — 2 or 3 overlapping circles.
- `Top of Funnel` — Funnel/pyramid diagram with labeled layers.

**Device / Screenshot Layouts:**
- `Desktop Designs` — Laptop frame with screenshot, text description on left.
- `Desktop Full` — Full-width laptop frame with screenshot, no text.
- `Mobile Designs (3-up)` — 3 phone frames side by side.
- `Mobile Designs (2-up with text)` — 2 phone frames with text description.
- `Mobile Annotated` — Single phone frame with annotation callout lines.

**Quote Layouts:**
- `Quote (single)` — Centered quote with avatar and attribution.
- `Quotes (2-col)` — 2 quotes side by side.
- `Quotes (3-col)` — 3 quotes side by side.

---

### Document 2: `dossier.md` — Companion Reference

```markdown
# [Project Name] — Case Study Dossier

**For:** [Target audience]
**Presentation outline:** [Link to outline.md]

---

## Section-by-Section Deep Dive

[For each section of the outline, include:]

### [Section Name]

**Extra detail:** Things that didn't fit on slides but are worth knowing

**Talking points:** Specific things to practice saying out loud

**If asked:** Backup detail to pull from if the audience probes deeper

---

## Anticipated Questions (8-12)

For each question:
- **Q:** [The question]
- **Why they'd ask:** [What's behind the question]
- **Suggested answer:** [2-3 sentence response in the user's voice]
- **Evidence to cite:** [Specific data, quote, or example]

[Cover questions like:]
- "Why this approach vs. [alternative]?"
- "What would you do differently?"
- "How did you handle [constraint/challenge]?"
- "What were the metrics / how did you measure success?"
- "What was your specific contribution vs. the team's?"
- "How did you handle disagreement or pushback?"
- "What surprised you?"
- Audience-specific questions based on target company/role

---

## Quotable Moments

[Specific anecdotes, customer quotes, stakeholder reactions, or memorable moments. These are gold for Q&A and for making the presentation feel real.]

---

## Data Points & Evidence

[All numbers, metrics, and concrete evidence in one place for quick reference. Include:]
- Research stats (# of interviews, calls, tests)
- Impact metrics (adoption, revenue, efficiency)
- Timeline data (how long, key milestones)
- Team size / scope indicators

---

## Audience-Specific Emphasis

[Based on the target audience, what to emphasize and what to skip:]
- **If they ask about craft:** [specific details to highlight]
- **If they ask about leadership:** [specific examples of driving alignment, influencing without authority]
- **If they ask about collaboration:** [specific cross-functional moments]
- **If they ask about technical depth:** [specific technical decisions or constraints]

---

## Things to Review Before Presenting

- [ ] Review the outline and practice transitions between sections
- [ ] Have screenshots/visuals ready and know which ones you'll show
- [ ] Practice the "trigger" story — this is the hook
- [ ] Practice the reflection — this is the closer
- [ ] Review anticipated questions and your answers
- [ ] Know your 1-sentence summary of the project for when someone asks "what's this about?"
```

---

## Best Practices (Enforced During Output)

Apply these when generating the outline and dossier:

- **Lead with the problem, not the solution.** Hook the audience with what was at stake before showing what you built.
- **Avoid the "and then" trap.** Don't narrate chronologically — create tension and payoff. Structure around decisions and turning points, not a timeline.
- **Be specific about your role.** Use "I" not just "we." Clarify what wouldn't have happened without you.
- **One idea per slide.** Less text, more visuals. Slides support the speaker, not the other way around. If a slide has more than 3 bullets, split it.
- **Show killed ideas.** What you didn't do is as interesting as what you did. It shows thinking, not just output.
- **Handle missing metrics gracefully.** Not every project has clean numbers. Use: usability evidence, stakeholder quotes, engineering efficiency, adoption data, "what I would measure if I could."
- **Budget for Q&A.** The dossier's anticipated questions section exists for this reason. Practice answers to the hardest 3-4 questions.
- **Depth over breadth.** 15-20 minutes means you can go deep on one project. Don't rush through to fit everything — cut slides before you compress them.
- **Personal intro is reusable.** The first 2-3 slides can stay the same across case studies (update title/role as needed). Each case study presentation starts with one.
- **Section divider slides are optional.** Dark/colored divider slides between sections help pacing, but don't mandate them.
- **Table of contents slide.** A TOC slide after the intro section listing the major sections helps the audience know what's coming and sets expectations.
- **Progressive reveal / build slides.** Progressive reveal works well for complex concepts — consider it for responsibility lists, product context, or multi-step frameworks.
- **Numbered insights / decisions.** Numbered insights ("Insight #1, #2, #3") or numbered key decisions work well as a storytelling device — concrete, memorable, easy to reference in Q&A.
- **Separate "unexpected" results.** Split results into positive, negative, and unexpected. The unexpected section often contains the best stories.
- **Visuals first, then content.** When recommending slides, think about what image or artifact would be most compelling, then write the content to support it.

---

## After Generation

**Narrate as you generate.** Don't silently write files — explain what you're creating:

> "Building two documents for you. The **outline** is a slide-by-slide structure you can build from in whatever slide tool you use — each slide has a headline, content bullets, visual recommendation, and speaker notes. The **dossier** is your companion reference: deeper detail, talking points for each section, and anticipated Q&A so you're ready for the hard questions."

After saving:

> "Your strongest material is [specific moment/story] — that's your hook. And the [specific metric/insight] is concrete enough to anchor the impact section. The anticipated Q&A covers [N] questions, including [hardest one] — worth practicing out loud."

1. Save all three files to `Portfolio/case-studies/[project-name]/` (outline, dossier, raw-notes)
2. Ask the user to review the outline — any slides to add, remove, or reorder?
3. Ask if they want to adjust emphasis for a different audience
4. Remind them to gather the recommended visuals (screenshots, design file exports, data charts)
5. Offer to refine any section or generate additional anticipated questions
