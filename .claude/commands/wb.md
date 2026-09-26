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

0. **Ask for any uncaptured tasks** — before pulling data, ask:
   > "Before I build the brief — anything on Post-it notes or in your head that needs to go in this week's actions first?"
   Wait for a response. If items are given, add them to the current week's actions file as new action items (continuing the existing `#N` sequence) *and* to `actions/open.md`, then proceed. If the answer is no, continue immediately.

1. **Check Google Calendar** (if available) for meetings this week — list day, time, title, key attendees
2. **Read `actions/open.md`** — the live register of every open action, whichever week raised it. This is the full picture; no need to walk back through previous weeks' files
3. **Read the current week's actions file** (`actions/actions-YYYY-Www.md`) — for what was raised and closed this week specifically
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

## Open Actions Carrying Forward (from WNN)

<Actions from previous weeks that are still open, grouped by category>

## Project Snapshot

| Project | Status | Next Step |
|---------|--------|-----------|
| ... | Active | ... |

## Active Risks

| Risk | Level | Project |
|------|-------|---------|
| ... | High | ... |
```
