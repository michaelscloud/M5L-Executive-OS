# M5L Executive OS — Claude Code Instructions

This repo is your personal knowledge base and management system. It tracks meetings, people, projects, actions, and risks.

---

## Repo Structure

| Folder | Purpose |
|--------|---------|
| `/meetings` | Processed meeting notes (structured summaries) |
| `/meetings/transcripts` | Raw unedited transcripts — never modify these |
| `/people` | One file per person — family, team, clients, network |
| `/projects` | One file per initiative or project |
| `/actions` | `open.md` — live register of every open action; `actions-YYYY-Www.md` — what was opened and closed each week |
| `/weekly` | Weekly prep notes and retrospectives |
| `/daily` | Daily and weekend briefs |
| `/risks` | `active.md` — live risks; `closed.md` — resolved/closed risks |
| `/context` | Durable narrative context — profile, relationships, projects summary — see Context Files below |
| `/time` | Time, expenses, and mileage tracked per client/engagement — one file per client |
| `<folder>/archive/YYYY/MM/` | Archived files — see Archiving section |

---

## File Naming Conventions

- **Meetings:** `YYYY-MM-DD-<short-title>.md` e.g. `2026-03-13-board-checkin.md`
- **Transcripts:** `YYYY-MM-DD-<short-title>.transcript.md`
- **People:** `<firstname-lastname>.md` e.g. `sarah-jones.md`
- **Projects:** `<project-slug>.md` e.g. `series-a-prep.md`
- **Open actions register:** `actions/open.md` (single file, never archived)
- **Actions:** `actions-YYYY-Www.md` e.g. `actions-2026-W11.md`
- **Weekly review:** `weekly/YYYY-Www.md` e.g. `weekly/2026-W11.md`
- **Weekly brief:** `weekly/YYYY-Www-brief.md` e.g. `weekly/2026-W13-brief.md`
- **Daily brief:** `daily/YYYY-MM-DD.md` e.g. `daily/2026-03-26.md`
- **Weekend brief:** `daily/YYYY-Www-weekend.md` e.g. `daily/2026-W13-weekend.md`
- **Active risks:** `risks/active.md`
- **Closed risks:** `risks/closed.md`
- **Time & expenses:** `time/<client-slug>.md` e.g. `time/acme-corp.md`

---

## Meeting Ingestion Pipeline

### Trigger
When you paste a Granola URL, share a meeting link, or paste raw transcript text — process it immediately without asking for confirmation.

### Steps

1. **Fetch / receive** the content
   - For Granola URLs: use the `/granola` command (see `.claude/commands/granola.md`) to fetch structured metadata (title, participants, summary, action items) via the API, AND accept any pasted transcript text directly
   - Use Granola metadata to enrich and cross-reference the transcript where useful

2. **Classify** the meeting type:
   - `1:1` → file under `meetings/YYYY-MM-DD-1on1-<person>.md`
   - `client` → file under `meetings/YYYY-MM-DD-<client>-<topic>.md`
   - `advisory` → file under `meetings/YYYY-MM-DD-advisory-<org>.md`
   - `internal` → file under `meetings/YYYY-MM-DD-internal-<topic>.md`
   - `other` → file under `meetings/YYYY-MM-DD-<description>.md`
   - Add your own types here as your context requires (e.g. `board`, `investor`) — see "Adapting for Your Context" in the README

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

9. **Log time if billable** — if the meeting is for a client that has a rate card in `/time`, add a time log entry (see Time & Expense Tracking below). Don't wait to be asked.

10. **Scan for risks** — if any risk signals detected, append to `risks/active.md` (see Risk Detection below)

11. **Report back** — summarise what was extracted and what was updated

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
Follow the full weekly review process described in `.claude/commands/wr.md` (also invoked via `/wr`) — read `actions/open.md` and the current week's actions file, close confirmed actions, write the summary and Executive Summary, then offer to commit and push.

### When asked for a weekly summary:
1. Read the current week's actions file, and `actions/open.md` for anything still open from earlier weeks
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

### Risk format — append to `risks/active.md`; move to `risks/closed.md` when resolved:
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

Each action has a sequential number scoped to its week, starting at 1. The number is always written with a week prefix: `W16#1`, `W16#2`, etc. Numbers never change once assigned — new actions added during the week continue from the highest existing number.

Use the short form `#N` only within the actions file itself (where the week is already clear from the heading). Everywhere else — people files, project files, meeting notes, cross-references — always use the full `W16#N` form to avoid ambiguity.

```
- [ ] #N <action description> | Owner: <name> | Due: <date or "TBC"> | Source: [meeting title](path/to/meeting.md)
- [x] #N <completed action> | Owner: <name> | Closed: <date>
```

### Two files, two jobs

| File | Job |
|------|-----|
| `actions/open.md` | **The live register.** Every currently-open action, whichever week raised it, grouped by category and always written in full `WNN#N` form. Never archived. This is what "what's open?" means. |
| `actions/actions-YYYY-Www.md` | **The weekly record.** What was opened and closed in that week. Historical, archived on the normal schedule. Not the live list. |

An open action must appear in **both**: the week file that raised it (so provenance survives) and `open.md` (so it stays visible after that week's file is archived). Numbers are assigned once by the week file and never change.

**Raising an action:** add it to the current week's actions file *and* to the matching category in `open.md`.

### "Close N" shortcut
When you say **"Close N"** or **"Close N, M, P"** (with or without week prefix):
1. Read `actions/open.md` to find the action — it may have been raised in an earlier week
2. Find each action by its number
3. In its **week file**, mark it `[x]` and append `| Closed: <today's date>`
4. Move it from **Open** to **Closed This Week** in that week file
5. **Remove it from `actions/open.md`** — the register holds only what is still open
6. Update the relevant `/people` files — remove from Open Actions, note as closed
7. Update the relevant `/projects` files — remove from Open Actions, note as closed
8. Confirm what was closed

Do this without asking for confirmation. If a number isn't found in `open.md`, check the week files before flagging it — and if it turns up there, that's a register drift, so say so.

### When actions are updated with new information
Whenever an action is edited — owner change, due date, description — update the entry in **`actions/open.md`, the week file, and the relevant `/people` and `/projects` files** so all four stay in sync. `open.md` is the version to trust if they ever disagree.

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

## Time & Expense Tracking

One file per client/engagement at `time/<client-slug>.md`, each opening with a Rate Card (hourly rate, minimum billable increment, mileage rate, other terms) followed by Time Log, Expenses Log, Mileage Log, and Totals tables. Full format and behaviour: `.claude/commands/time.md`.

This works equally well for time you're actually invoicing and for time you're tracking to demonstrate value contributed but not billing (e.g. sweat equity ahead of a funding round). The rate card's **Purpose** field controls which framing is used.

When a client meeting is ingested via the Meeting Ingestion Pipeline and that client has a rate card in `/time`, log the time entry automatically as part of ingestion — apply the client's minimum billable increment, don't wait to be asked. If a new client starts billable work, create their `/time` file with a rate card before logging anything, and flag that it's been created.

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
| `/pod` | Generate a podcast script from this week's review |
| `/pod W12` | Generate a podcast script for a specific week |
| `/granola <url>` | Fetch a Granola note and run it through the meeting ingestion pipeline |
| `/tidy [file]` | Remove excess blank lines from a file (or the most recently edited one) |
| `/time` | Show time/expense totals across all tracked clients |
| `/time <client>` | Show the time/expense log and totals for one client |

Weekly briefs are **mostly frozen on creation** — the narrative, meeting schedule, context, and strategic priority sections are never edited after the fact. The one exception: action checkbox states (`[ ]` → `[x]`) in the **Actions Due This Week** and **Overdue Actions** sections may be updated as actions are closed. Actions stay in the section they were assigned to at brief creation, so the week-start plan remains visible. Compare against `/wr` at end of week to see what changed.

---

## Context Files

The `/context` folder holds durable narrative context that should be loaded when generating reports, briefs, or scripts. These files go stale if not maintained — treat them as living documents and update when significant changes occur. A minimal starting set:

| File | Purpose | Load when |
|------|---------|-----------|
| `context/profile.md` | Your bio, business, voice/tone | Generating any report, script, or external-facing content |
| `context/relationships.md` | Key people — role and current state, one line each | Meeting prep, weekly brief, any people-facing task |
| `context/projects-summary.md` | Narrative summary per active project with risk level | Weekly brief, weekly review, project-related questions |

Add more files here as your context requires (e.g. one profiling each client organisation you're engaged with).

### When to update context files

- **After a significant meeting** — update the relevant file if the state of an engagement changes materially
- **After weekly review** — update `projects-summary.md` if a project status shifts
- **When a relationship goes cold or heats up** — update `relationships.md`
- Do not update context files for routine action closes or minor updates — they are narrative, not a log

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

## Extending the System — Optional Integrations

These are patterns from real usage, not required — adapt or drop them depending on your setup.

### Syncing to NotebookLM (or similar) via Drive

If you use a tool like NotebookLM for deeper Q&A over your context, you can have Claude push a standing set of files to a shared Drive folder on request (e.g. a `/sync-drive` shortcut):

```
Drive folder: <your-folder-name> (<folder-id>) — owned by <your-email>, shared with <your-other-email>
```

Upload each context/brief file as plain text (not converted to a Doc) so the ingestion tool reads clean markdown rather than a rendered document. Since most Drive APIs create new files rather than updating in place, periodically clear stale versions from the folder and re-link sources in the target tool.

### Enforcing brand/writing guidelines on generated documents

If you produce documents on Claude's behalf — proposals, reports, briefs — you can point it at your own style guide and have every document follow it automatically. Keep the guide file(s) somewhere Claude will read before generating a document (e.g. `context/brand/`), and reference them from here, e.g.:

| File | Covers |
|------|--------|
| `context/brand/writing-style-guide.md` | Voice and tone, sentence construction, structure |
| `context/brand/visual-brand-guidelines.md` | Fonts, colours, headings, tables, footer, logo |

Then list the concrete rules you want enforced — tone, sentence length, fonts, colours, table styling, footer text, whatever matters for your documents — and note any manual follow-up steps needed if the document tool (e.g. Google Docs) can't fully replicate something like a page-1-only logo or a true repeating footer.

---

## Friday Reminder

If today is a Friday, remind the user at the start of the conversation to push any uncommitted changes to remote and do any other end-of-week housekeeping they've configured (e.g. syncing a separate Claude config repo). Also add an action to the current week's actions file: "End-of-week push and housekeeping" — so it can be checked off.

When preparing the weekly brief on a Monday, check the previous week's actions file for the "End-of-week push and housekeeping" action. If it's missing (e.g. the user had a day off), flag it and ask whether it should be added retrospectively.

Also on Fridays — run the archiving check (see Archiving below). If the previous Friday's archive was missed, flag it at the start of the next session and offer to run it then.

---

## Archiving

Files are archived every Friday to keep the active file structure readable. Each subfolder uses an `archive/YYYY/MM/` path.

### Archive locations

| Folder | Archive path |
|--------|-------------|
| `meetings/` | `meetings/archive/YYYY/MM/` |
| `meetings/transcripts/` | `meetings/transcripts/archive/YYYY/MM/` |
| `actions/` | `actions/archive/YYYY/MM/` |
| `weekly/` | `weekly/archive/YYYY/MM/` |
| `daily/` | `daily/archive/YYYY/MM/` |
| `people/` | `people/archive/YYYY/MM/` |
| `projects/` | `projects/archive/YYYY/MM/` |

### Archiving rules

| Content | Archive when |
|---------|-------------|
| Daily briefs (`daily/`) | File date > 28 days ago |
| Meeting notes (`meetings/`, `meetings/transcripts/`) | File date > 28 days ago |
| Actions files (`actions/actions-YYYY-Www.md`) | Week end date > 28 days ago |
| **Open actions register (`actions/open.md`)** | **Never — it is the live list, not a weekly record** |
| Weekly notes/briefs (`weekly/`) | Week end date > 6 weeks ago |
| People files (`people/`) | Manual only — when a relationship becomes dormant |
| Project files (`projects/`) | Manual only — when a project completes or is abandoned |

### How to archive on Fridays

1. Identify files eligible for archiving based on the rules above
2. **Before archiving an `actions/actions-YYYY-Www.md` file, reconcile it against `actions/open.md`.** For every still-open item in the week file, confirm it appears in the register; add any that are missing, in full `WNN#N` form under the right category. Only then archive the week file. `actions/open.md` is **never archived** — an open action reachable only by opening an old archived file is effectively lost.
3. Move each file to its `archive/YYYY/MM/` path, where YYYY/MM is taken from the **file's own date** (not today)
4. **Rewrite inbound links.** Moving a file breaks every relative link elsewhere in the repo that pointed at its old path (evidence links in `risks/active.md`, Meeting History entries in `/people` files, etc.). After moving files, search the repo for links to the old paths and update them to the new `archive/YYYY/MM/...` location rather than leaving them broken.
5. Confirm what was moved and what links were rewritten
6. Commit as a content update directly to main (or just confirm the moves if you're not using git)

---

## Session Start

At the start of every conversation, remind the user to pull the repo if they haven't already — this matters if the setup runs across more than one machine:

```
git pull
```

Also check whether a daily brief exists for today (`daily/YYYY-MM-DD.md`). If it does not, prompt: "No daily brief yet — want me to run `/db`?" Do not create it automatically; wait for confirmation.

(The `git pull` step is optional — only relevant if you're using git for version history/backup. Skip it if you're not.)

---

## Things to Always Do

- Save raw transcripts before analysis
- Link actions back to source meeting files
- Never delete old content — append or mark superseded
- When updating files, make targeted edits only
- Flag ambiguity rather than guess
- Keep weekly files as running logs — append, never overwrite
- **Before booking any calendar event** — check for clashes with existing events in the same time slot across your configured calendars. Flag any conflicts before creating the event and ask for confirmation.

---

## Commit Convention

*Skip this whole section if you're not using git — it's entirely optional. Everything else in this file works the same either way.*

After processing meetings and updating files, offer to commit:
### Content updates (meetings, people, actions, briefs, weekly notes)
Commit directly to main. Use `pu` as normal.

Commit message format:
```
notes: ingest [meeting-type] YYYY-MM-DD — [short description]

Updated: meetings/, people/[name].md, projects/[slug].md
Actions: [N new actions added]
Risks: [new risks noted | none]
```

### Structural changes (CLAUDE.md, commands, new folders, conventions)
Always use a branch and merge request — never commit structural changes directly to main.

Branch naming:
| Type | Pattern | Example |
|------|---------|---------|
| Config / CLAUDE.md | `config/description` | `config/weekly-brief-system` |
| New commands / features | `feature/description` | `feature/daily-brief-commands` |

Push the branch, share the PR link, and wait for it to be merged via GitHub.

### "push updates" / "pu" shortcut
When you say **"push updates"** or **"pu"**, do the following without asking for confirmation:
1. `git add .`
2. `git status` — summarise what's changed in plain English
3. If **content only**: commit and push directly to main
4. If **structural changes are included**: create an appropriately named branch, commit, push, and display the GitHub PR link

---

## Owner Context

> **This section is the most important thing to personalise.** Fill it in before you start — it shapes how Claude understands your world and prioritises information. You can also just tell Claude about yourself in the chat and ask it to write this section for you.

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
- [Document defaults — e.g. "Always create Google Docs, not Word, unless asked"]
- [Any other working preferences Claude should know]
