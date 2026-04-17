---
name: todo
description: Manage the user's unified Kanban board at TODOS.md. Use when the user says "/todo" followed by an action like add, done, move, list, or clean.
---

# /todo — Task Management

Manage the user's unified kanban board at [TODOS.md](../../../TODOS.md).

**Trigger:** User says `/todo` followed by an action.

---

## Actions

### Add a task
**Examples:** `/todo add follow up with recruiter`, `/todo add prep for interview #search 🔴`

1. Read `TODOS.md`
2. Parse the task description. Infer:
   - **Category tag** from context: `#search` (job-related), `#networking` (people/events), `#content` (writing/publishing), `#work` (day job). Ask if ambiguous.
   - **Priority** if mentioned: 🔴 High, 🟡 Medium, 🟢 Low. Omit if not specified.
   - **Due date** if mentioned: `@{YYYY-MM-DD}` format.
3. Add `- [ ] [priority] Task description #tag [@{date}]` to the **Not Started** column
4. Write the updated file
5. Confirm what was added

### Mark a task done
**Examples:** `/todo done interview prep`, `/todo done follow up with recruiter`

1. Read `TODOS.md`
2. Find the matching task (fuzzy match on description — doesn't need to be exact)
3. If multiple matches, show them and ask which one
4. Move the task to the **Archive** column (below the `***` divider) and change `- [ ]` to `- [x]`
5. Write the updated file
6. Confirm what was completed

### Move a task
**Examples:** `/todo move [company name] to waiting`, `/todo start the outreach`

1. Read `TODOS.md`
2. Find the matching task (fuzzy match)
3. Move it to the specified column: `Not Started`, `Started`, `Waiting`, `Done`, or `Archive`
4. If moving to `Done` or `Archive`, also check the box (`- [x]`)
5. If moving out of `Done`/`Archive`, uncheck the box (`- [ ]`)
6. Write the updated file
7. Confirm the move

### List tasks
**Examples:** `/todo list`, `/todo list #search`, `/todo what's on my plate?`

1. Read `TODOS.md`
2. If a filter is specified (tag, priority, column), apply it
3. Display tasks grouped by column, with tags and priorities visible
4. Show counts per column

### Clean archived items
**Examples:** `/todo clean`, `/todo clean archive`

1. Read `TODOS.md`
2. Show the Archive items and ask for confirmation
3. Remove confirmed items from the board entirely
4. Write the updated file
5. Confirm what was removed

---

## Board Format

The file uses Obsidian Kanban plugin format:

```markdown
---

kanban-plugin: board

---

## Not Started
- [ ] 🔴 Task description #search @{2026-02-05}

## Started
- [ ] Task in progress #content

## Waiting
- [ ] Blocked on someone #search

## Done

***

## Archive
- [x] Completed task #search

%% kanban:settings
{"kanban-plugin":"board"}
%%
```

**Tags:** `#search`, `#networking`, `#content`, `#work` (defaults — the user can customize these in `TODOS.md`)
**Priority prefixes:** 🔴 High, 🟡 Medium, 🟢 Low (optional)
**Due dates:** `@{YYYY-MM-DD}` (optional, Kanban plugin date picker format)

---

## Rules

- Always read the current file before making changes (never write from memory)
- Preserve the kanban frontmatter (`kanban-plugin: board`) and the `%% kanban:settings %%` block at the end
- Keep items within their column's section
- When adding, default to **Not Started** unless user says otherwise
- Fuzzy match task descriptions — partial descriptions should still find the right task
- If a match is ambiguous, show options and ask
- Don't duplicate tasks — if a similar task exists, flag it
