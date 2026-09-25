# Weekly Brief (wb)

Generate or display the weekly brief.

## Usage
- `/wb` — create or show this week's brief
- `/wb W12` (or any week number) — show the brief for that week

## Behaviour

### Determine the target week
- If no argument: use the current week (today's date → ISO week number → `YYYY-Www`)
- If an argument like `W12` or `13` is given: resolve to the correct year and week, e.g. `2026-W12`

### File path
`weekly/YYYY-Www-brief.md`

### If the file already exists
Display it. Weekly briefs are **mostly frozen on creation** — the narrative, meeting schedule, context, and strategic priority sections are never edited after the fact. The one exception: action checkbox states (`[ ]` → `[x]`) in **Actions Due This Week** and **Overdue Actions** may be updated as actions are closed, so the week-start plan stays visible alongside what actually happened.

### If the file does not exist (current week only)
Create it using the format below, then display it.

1. **Check Google Calendar** (if available) for meetings this week — list day, time, title, key attendees
2. **Read the current week's actions file** (`actions/actions-YYYY-Www.md`) — extract all open actions
3. **Read previous weeks' action files** — find any overdue open actions (due date has passed)
4. **Read `risks/active.md`** — include any high or medium risks
5. **Scan `/projects`** — brief one-liner status for each active project

---

## Weekly Brief Format

```markdown
# Weekly Brief — Week NN, YYYY (Mon DD Mmm – Fri DD Mmm)
*Generated: YYYY-MM-DD | Mostly frozen — only action checkboxes update after creation*

## This Week's Meetings

| Day | Time | Meeting | Key People |
|-----|------|---------|------------|
| Mon | 10:00 | ... | ... |

## Prep Notes
<For any meeting that has a relevant /people or /projects file, add a short prep note>

## Actions Due This Week

- [ ] #N <action> | Owner: [Your Name] | Due: YYYY-MM-DD

## Overdue Actions ⚠️

- [ ] #N <action> | Owner: [Your Name] | Due: YYYY-MM-DD | ⚠️ X days overdue

## Project Snapshot

| Project | Status | Next Step |
|---------|--------|-----------|
| ... | Active | ... |

## Active Risks

| Risk | Level | Project |
|------|-------|---------|
| ... | High | ... |
```
