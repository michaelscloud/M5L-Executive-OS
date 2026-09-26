# Daily Brief (db)

Generate or display the daily brief.

## Usage
- `/db` — show today's brief (or this weekend's brief if Sat/Sun)
- `/db 2026/03/24` — show the brief for a specific date

## Behaviour

### Determine the target date
- If no argument: use today's date
- If a date argument is given: parse it (accepts `YYYY/MM/DD` or `YYYY-MM-DD`)

### Determine if it's a weekend
- Saturday or Sunday → use the weekend brief for that ISO week: `daily/YYYY-Www-weekend.md`
- Weekday → use the day brief: `daily/YYYY-MM-DD.md`

### If the file already exists
Display it as-is.

### If the file does not exist
Create it using the format below, then display it.

1. **Check Google Calendar** (if available) for meetings on this day — list time, title, key attendees
2. **Read `actions/open.md`** — the live register of everything open, whichever week raised it. Extract anything due today, overdue, or due within 3 days
3. **Cross-reference `/people`** for anyone in today's meetings — pull any open actions or context worth noting

---

## Daily Brief Format (weekday)

```markdown
# Daily Brief — YYYY-MM-DD (Weekday)

## Today's Meetings

| Time | Meeting | Key People |
|------|---------|------------|
| 10:00 | ... | ... |

## Prep Notes
<Short notes for each meeting, drawn from /people and /projects>

## Actions Due Today

- [ ] #N <action> | Owner: [Your Name]

## Notes

<Running notes — add as the day goes on>
```

---

## Daily Brief Format (weekend)

```markdown
# Weekend Brief — Week NN, YYYY (Sat DD – Sun DD Mmm)

## Weekend Actions

- [ ] #N <action> | Owner: [Your Name] | Due: YYYY-MM-DD

## Notes

<Running notes>
```
