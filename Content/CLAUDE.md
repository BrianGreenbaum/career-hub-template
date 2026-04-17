# Content Hub — Instructions for Claude

## Overview

This folder contains the user's content creation workflow. The platforms and cadence are set during `/onboard` (or by editing this file directly).

**For writing style and voice, use the `/writing-style` skill** (or fall back to the defaults in the root `CLAUDE.md` if it hasn't been set up yet).

---

## Publishing Cadence

> Filled in by `/onboard`. Example:

| Platform | Target Frequency | Notes |
|----------|------------------|-------|
| {{platform_1}} | {{cadence_1}} | {{notes_1}} |
| {{platform_2}} | {{cadence_2}} | {{notes_2}} |

---

## Content Workflow

### 1. Capture Ideas
Add ideas to [ideas.md](./ideas.md) as they come up. Tag with the intended platform:
- `#{{platform_1_tag}}`
- `#{{platform_2_tag}}`

### 2. Draft
Move promising ideas to platform draft folders:
- `{{platform_1}}/drafts/`
- `{{platform_2}}/drafts/`

### 3. Publish
After publishing, log the post in the platform's `published.md`:
- Date, title/hook, link, brief notes on performance (optional)

---

## Writing Modes

The specifics of voice and tone live in the `/writing-style` skill. This file describes the *workflow*, not the voice.

General guidelines that apply across platforms:
- Lead with a hook — a surprising outcome, question, or concrete observation
- Specific details make writing real — anchor abstractions to examples
- End with a takeaway, question, or invitation (platform-appropriate)
- Avoid filler, hedge words, and corporate-speak

---

## Folder Structure

```
Content/
├── CLAUDE.md               # This file
├── README.md               # Content hub — status, upcoming, recent
├── ideas.md                # Running list of ideas (tagged by platform)
└── {platform}/
    ├── drafts/             # Drafts in progress
    └── published.md        # Log of published pieces
```

Platform subfolders are created lazily — no need to scaffold a folder for a platform that isn't in use.
