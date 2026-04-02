# Weekly Review (wr)

Display or run the weekly review.

## Usage
- `/wr` — show (or run) this week's review
- `/wr W12` (or any week number) — show the review for that specific week

## Behaviour

### Determine the target week
- If no argument: use the current week (`YYYY-Www`)
- If an argument like `W12` or `13` is given: resolve to the correct year and week

### File path
`weekly/YYYY-Www.md`

### If the file already exists
Display it.

### If the file does not exist (current week)
Run the weekly review process as defined in CLAUDE.md under "When asked to run my weekly review":

1. Read the current week's actions file
2. Scan meetings from that week
3. Present all open actions as a numbered list — ask the owner to confirm which are done
4. Mark confirmed actions as closed with today's date
5. Produce a summary: what happened, decisions made, actions closed, still open, risks flagged, anything to carry forward
6. Create the weekly note at `weekly/YYYY-Www.md`
7. Compare against the weekly brief (`weekly/YYYY-Www-brief.md`) if it exists — note anything planned that didn't happen, or unplanned things that did
8. Offer to commit and push
