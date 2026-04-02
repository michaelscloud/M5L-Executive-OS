# CEO Brain — Claude Code Instructions

This repo is your personal knowledge base and management system. It tracks meetings, people, projects, actions, and risks.

---

## Repo Structure

| Folder | Purpose |
|--------|---------|
| `/meetings` | Processed meeting notes (structured summaries) |
| `/meetings/transcripts` | Raw unedited transcripts — never modify these |
| `/people` | One file per person — family, team, clients, network |
| `/projects` | One file per initiative or project |
| `/actions` | Open and closed action items, organised by week |
| `/weekly` | Weekly prep notes and retrospectives |
| `/daily` | Daily briefs — one per weekday, one combined for weekends |
| `/risks` | Active risk register |

---

## File Naming Conventions

- **Meetings:** `YYYY-MM-DD-<short-title>.md` e.g. `2026-03-13-board-checkin.md`
- **Transcripts:** `YYYY-MM-DD-<short-title>.transcript.md`
- **People:** `<firstname-lastname>.md` e.g. `sarah-jones.md`
- **Projects:** `<project-slug>.md` e.g. `series-a-prep.md`
- **Actions:** `actions-YYYY-Www.md` e.g. `actions-2026-W11.md`
- **Weekly review:** `weekly/YYYY-Www.md` e.g. `weekly/2026-W11.md`
- **Weekly brief:** `weekly/YYYY-Www-brief.md` e.g. `weekly/2026-W13-brief.md`
- **Daily brief:** `daily/YYYY-MM-DD.md` e.g. `daily/2026-03-26.md`
- **Weekend brief:** `daily/YYYY-Www-weekend.md` e.g. `daily/2026-W13-weekend.md`
- **Risks:** `risks/active.md`

---

## Meeting Ingestion Pipeline

### Trigger
When you paste a Granola URL, share a meeting link, or paste raw transcript text — process it immediately without asking for confirmation.

### Steps

1. **Fetch / receive** the content
   - For Granola URLs: use WebFetch to retrieve structured metadata (title, participants, summary, action items) AND accept any pasted transcript text
   - Use Granola metadata to enrich and cross-reference the transcript where useful

2. **Classify** the meeting type:
   - `1:1` → file under `meetings/YYYY-MM-DD-1on1-<person>.md`
   - `client` → file under `meetings/YYYY-MM-DD-<client>-<topic>.md`
   - `advisory` → file under `meetings/YYYY-MM-DD-advisory-<org>.md`
   - `internal` → file under `meetings/YYYY-MM-DD-internal-<topic>.md`
   - `other` → file under `meetings/YYYY-MM-DD-<description>.md`

3. **Save the raw transcript first** — before any analysis:
   - Path: `meetings/transcripts/YYYY-MM-DD-<description>.transcript.md`
   - Prepend YAML front matter:
     ```yaml
     ---
     date: YYYY-MM-DD
     type: <meeting-type>
     participants: [names]
     source: <granola-url or "pasted">
     ---
     ```
   - Then the full unedited text — never summarise or clean up transcript files

4. **Analyse and extract:**
   - Action items (who, what, when)
   - Decisions made
   - Project status updates
   - Risk signals (see Risk Detection below)
   - Key discussion topics and outcomes
   - People context — concerns, wins, relationship signals

5. **Save processed meeting note** to the appropriate `/meetings` path
   - Include at the bottom: `**Transcript:** [Full transcript](meetings/transcripts/YYYY-MM-DD-<description>.transcript.md)`
   - If from Granola, include: `**Source:** [Granola](<url>)`

6. **Update `/actions`** — add new action items to the current week's file using the standard format (see below). Link each back to the source meeting file.

7. **Update `/people` files** — for each person who appeared in the meeting:
   - Add to their Meeting History
   - Update Context if anything new and relevant was learned
   - Add any open actions to their Open Actions section

8. **Update `/projects` files** — for any project discussed:
   - Add decisions to the Decisions Log
   - Update Open Actions
   - Update Notes with any relevant status changes

9. **Scan for risks** — if any risk signals detected, append to `risks/active.md` (see Risk Detection below)

10. **Report back** — summarise what was extracted and what was updated

### Processing Rules
- Always save the raw transcript BEFORE doing any analysis
- Never edit, summarise, or clean up transcript files
- When updating files, use targeted edits — never rewrite a whole file
- Never delete old content — append or mark as closed/superseded
- If a person appears in a meeting but has no `/people` file, create one using the standard template
- If something is ambiguous, flag it rather than guess

---

## Other Key Behaviours

### When asked to prep for a meeting:
1. Check `/meetings` for previous meetings with the same attendees or topic
2. Check `/people` files for context on attendees
3. Check `/actions` for open items involving those people or projects
4. Check `/projects` for relevant project status
5. Produce a structured prep brief: context, open items, suggested agenda, things to watch for

### When asked to "run my weekly review" or "weekly review":
1. Read the current week's actions file
2. Scan meetings from that week
3. Present all open actions as a numbered list with owner and source
4. Ask to confirm which are done — wait for response
5. Mark confirmed actions as closed with today's date
6. Produce a summary: what happened, decisions made, actions closed, actions still open, risks flagged, anything to carry forward
7. Create or update the weekly note in `/weekly/YYYY-Www.md` with the summary
8. Offer to commit and push

### When asked for a weekly summary:
1. Read the current week's actions file
2. Scan meetings from that week
3. Produce: what happened, decisions made, actions opened, actions closed, risks flagged, anything carried forward

### When asked about a person:
1. Read their `/people` file
2. Scan recent meetings they appeared in
3. Summarise: recent interactions, open actions, any flagged items

### When asked about a project:
1. Read the `/projects` file
2. Find related meetings
3. Summarise: current status, recent decisions, open actions, risks if noted

---

## Risk Detection

### Flag delivery risks when you see:
- Missed deadlines or slipping timelines
- Same blocker appearing in multiple meetings
- Scope changes or shifting requirements
- Work items with no progress across multiple meetings
- Unclear ownership of important items

### Flag relationship / people risks when you see:
- Concerns or frustrations repeated across multiple conversations
- Negotiation signals — hesitation, pushback, or stalling on key terms
- Dependency risks — a project blocked on one person or one decision
- Retention signals in advisory or partnership conversations

### Risk format — append to `risks/active.md`:
```
### [Short Risk Title] — [low/medium/high]
- **Type:** delivery | relationship | dependency
- **Project:** [project slug]
- **Person:** [name, if relevant]
- **First noted:** YYYY-MM-DD
- **Last updated:** YYYY-MM-DD
- **Description:** What the risk is
- **Evidence:** Links to meeting notes where signals appeared
- **Suggested action:** What might help
```

---

## Action Item Format

Each action has a sequential number (`#N`) scoped to its week, starting at #1. Numbers never change once assigned — new actions added during the week continue from the highest existing number.

```
- [ ] #N <action description> | Owner: <name> | Due: <date or "TBC"> | Source: [meeting title](path/to/meeting.md)
- [x] #N <completed action> | Owner: <name> | Closed: <date>
```

### "Close N" shortcut
When you say **"Close N"** or **"Close N, M, P"**:
1. Read the current week's actions file
2. Find each action by its `#N` number
3. Mark it `[x]` and append `| Closed: <today's date>`
4. Move it from **Open** to **Closed This Week**
5. Update the relevant `/people` files — remove from Open Actions, note as closed
6. Update the relevant `/projects` files — remove from Open Actions, note as closed
7. Confirm what was closed

Do this without asking for confirmation. If a number isn't found, flag it.

### When actions are updated with new information
Whenever an action is edited — owner change, due date, description — also update the corresponding entry in the relevant `/people` and `/projects` files to keep them in sync.

---

## People File Format

```markdown
# <Full Name>
**Role:** <their role>
**Team / Org:** <team or company>
**Relationship:** Family | Direct report | Client | Advisor | Investor | Partner | Network

## Contact
- Email:
- Phone:

## Context
<Running notes — working style, priorities, relationship history, anything useful>

## Open Actions
<Kept in sync with /actions>

## Meeting History
<Links or refs to relevant meetings — newest first>
```

---

## Project File Format

```markdown
# <Project Name>
**Status:** Active | On Hold | Complete
**Owner:** <name>
**Category:** <category>
**Started:** <date>

## Objective
<What this project is trying to achieve>

## Decisions Log
| Date | Decision | Made By |
|------|----------|---------|

## Open Actions
<Kept in sync with /actions>

## Notes
<Running context — newest first>
```

---

## Shortcuts

| Command | Description |
|---------|-------------|
| `/wb` | Create or display this week's brief |
| `/wb W12` | Display the brief for a specific week |
| `/db` | Create or display today's brief (weekend → weekend brief) |
| `/db 2026/03/24` | Display the brief for a specific date |
| `/wr` | Run or display this week's review |
| `/wr W12` | Display the review for a specific week |

Weekly briefs are **frozen on creation** — never edited after the fact. Compare against `/wr` at end of week to see what changed.

---

## Display Conventions

When displaying actions, reviews, or any list of tasks — always pretty print:

- Use `- [x]` and `- [ ]` for completed/open actions so they render as checkboxes
- Use rendered markdown tables for summaries, risks, and decisions
- Flag overdue actions with ⚠️ and the number of days overdue
- Flag actions due within 3 days with 🔔
- Group actions by category where relevant
- Show owner alongside each action
- In weekly reviews, include a clean carry-forward section at the bottom

---

## Friday Reminder

If today is a Friday, remind the user at the start of the conversation to push any uncommitted changes to remote and do any end-of-week housekeeping they have configured. Also add an action to the current week's actions file: "End-of-week push and housekeeping" — so it can be checked off.

When preparing the weekly brief on a Monday, check the previous week's actions file for the "End-of-week push and housekeeping" action. If it's missing (e.g. the user had a day off), flag it and ask whether it should be added retrospectively.

---

## Things to Always Do

- Save raw transcripts before analysis
- Link actions back to source meeting files
- Never delete old content — append or mark superseded
- When updating files, make targeted edits only
- Flag ambiguity rather than guess
- Keep weekly files as running logs — append, never overwrite

---

## Commit Convention

After processing meetings and updating files, offer to commit:

```
notes: ingest [meeting-type] YYYY-MM-DD — [short description]

Updated: meetings/, people/[name].md, projects/[slug].md
Actions: [N new actions added]
Risks: [new risks noted | none]
```

### "push updates" / "pu" shortcut
When you say **"push updates"** or **"pu"**, do the following without asking for confirmation:
1. `git add .`
2. `git status` — summarise what's changed in plain English
3. If **content only** (meetings, people, actions, briefs): commit and push directly to main
4. If **structural changes are included** (CLAUDE.md, commands, folders, conventions): create a branch, commit, push, and display the GitHub PR link

Branch naming for structural changes:
| Type | Pattern | Example |
|------|---------|---------|
| Config / CLAUDE.md | `config/description` | `config/weekly-brief-system` |
| New commands / features | `feature/description` | `feature/daily-brief-commands` |

Review and merge structural changes via GitHub. Do not merge to main directly.

---

## Owner Context

> **This section is the most important thing to personalise.** Fill it in before you start — it shapes how Claude understands your world and prioritises information.

This brain belongs to **[Your Name]** — [one sentence describing your role, what you're building, and your current focus].

**Key relationships:**
- [Person name] — [their role and why they matter to you]
- [Person name] — [their role and why they matter to you]
- [Add as many as relevant]

**Active priorities:**
- [Priority 1 — e.g. "Series A fundraising — target close Q3 2026"]
- [Priority 2 — e.g. "Product launch — new enterprise tier"]
- [Priority 3]

**Preferences:**
- [Communication style — e.g. "Direct and concise", "British English spelling"]
- [Any other working preferences Claude should know]
