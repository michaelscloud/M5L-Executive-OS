# Job Hunt OS — Claude Code Instructions

This repo is Connor's job hunt brain. It tracks applications, CVs, cover letters, interviews, contacts, actions, and risks.

---

## Repo Structure

| Folder | Purpose |
|--------|---------|
| `/meetings` | Interview notes and networking call summaries |
| `/meetings/transcripts` | Raw unedited transcripts — never modify these |
| `/people` | One file per person — recruiters, hiring managers, contacts |
| `/projects` | One file per job application |
| `/cv` | Master CV and tailored versions per application |
| `/cover-letters` | Cover letters, one per application |
| `/actions` | Open and closed action items, organised by week |
| `/weekly` | Weekly prep notes and retrospectives |
| `/daily` | Daily briefs — one per weekday, one combined for weekends |
| `/risks` | Active risk register — applications going cold, deadlines, etc. |

---

## File Naming Conventions

- **Meetings:** `YYYY-MM-DD-<short-title>.md` e.g. `2026-03-13-interview-jaguar.md`
- **Transcripts:** `YYYY-MM-DD-<short-title>.transcript.md`
- **People:** `<firstname-lastname>.md` e.g. `sarah-jones.md`
- **Applications (projects):** `<company-role-slug>.md` e.g. `jaguar-grad-engineer.md`
- **CV (master):** `cv/master-cv.md`
- **CV (tailored):** `cv/<company-role-slug>.md` e.g. `cv/jaguar-grad-engineer.md`
- **Cover letter:** `cover-letters/<company-role-slug>.md` e.g. `cover-letters/jaguar-grad-engineer.md`
- **Actions:** `actions-YYYY-Www.md` e.g. `actions-2026-W11.md`
- **Weekly review:** `weekly/YYYY-Www.md` e.g. `weekly/2026-W11.md`
- **Weekly brief:** `weekly/YYYY-Www-brief.md` e.g. `weekly/2026-W13-brief.md`
- **Daily brief:** `daily/YYYY-MM-DD.md` e.g. `daily/2026-03-26.md`
- **Weekend brief:** `daily/YYYY-Www-weekend.md` e.g. `daily/2026-W13-weekend.md`
- **Risks:** `risks/active.md`

---

## Application Pipeline

### Status progression
`Researching → Applied → Screening → Interviewing → Offer → Accepted / Declined / Ghosted`

### When a new job is added (paste a job posting or URL):
1. Create a project file at `projects/<company-role-slug>.md` using the Application Project Template below
2. Create a tailored CV at `cv/<company-role-slug>.md` based on `cv/master-cv.md` — highlight relevant experience, reorder sections if needed, match keywords from the job description
3. Create a cover letter at `cover-letters/<company-role-slug>.md`
4. Add an action to the current week's actions file: "Apply to [Company] — [Role]"
5. Report back with: what was changed in the CV, what angle the cover letter takes, and any suggestions for the application

### CV Tailoring Rules
- Always start from `cv/master-cv.md` — never invent experience
- Reorder bullet points to surface most relevant experience first
- Mirror language from the job description where it's honest to do so
- Flag any gaps or weaknesses in the application and suggest how to address them
- Keep to 1–2 pages max
- Note what was changed and why at the top of the tailored CV file as a comment block

### Cover Letter Rules
- Keep to 3–4 short paragraphs: hook, relevant experience, why this company, close
- Tone: confident but not arrogant, specific not generic
- Must reference something real about the company — not boilerplate
- No "I am writing to apply for..." openers — lead with something stronger
- Flag if Connor needs to research the company more before the letter will land well

### Application Project Template

```markdown
# <Company> — <Role Title>
**Status:** Researching | Applied | Screening | Interviewing | Offer | Accepted | Declined | Ghosted
**Applied:** YYYY-MM-DD (or "Not yet")
**Closing date:** YYYY-MM-DD (or "Unknown")
**Source:** [Job board / referral / direct]
**Job posting:** [URL or "pasted"]
**CV used:** [cv/<slug>.md]
**Cover letter:** [cover-letters/<slug>.md]

## Role Summary
<2–3 sentence summary of what the role is and why it's interesting>

## Why This Role
<What appeals about this company/role specifically>

## Fit Assessment
<Where Connor is a strong fit, where there are gaps>

## Interview Stages
| Stage | Date | Format | Notes |
|-------|------|--------|-------|

## Decisions Log
| Date | Decision | Notes |
|------|----------|-------|

## Open Actions
<Kept in sync with /actions>

## Notes
<Running context — newest first>
```

---

## Meeting Ingestion Pipeline

### Trigger
When you paste a Granola URL, share a meeting link, or paste raw transcript text — process it immediately without asking for confirmation.

### Steps

1. **Fetch / receive** the content
   - For Granola URLs: use WebFetch to retrieve structured metadata (title, participants, summary, action items) AND accept any pasted transcript text
   - Use Granola metadata to enrich and cross-reference the transcript where useful

2. **Classify** the meeting type:
   - `interview` → file under `meetings/YYYY-MM-DD-interview-<company>.md`
   - `screening` → file under `meetings/YYYY-MM-DD-screening-<company>.md`
   - `networking` → file under `meetings/YYYY-MM-DD-networking-<person-or-org>.md`
   - `recruiter` → file under `meetings/YYYY-MM-DD-recruiter-<agency-or-company>.md`
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

8. **Update `/projects` files** — for any application discussed:
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

### When asked to prep for an interview:
1. Read the application project file in `/projects`
2. Check `/people` files for context on interviewers if known
3. Check `/meetings` for any previous interactions with this company
4. Check `/actions` for any open items related to this application
5. Produce a structured prep brief: role summary, likely question areas, things to emphasise, things to watch for, suggested questions to ask them

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

### When asked about an application:
1. Read the `/projects` file for that application
2. Find related meetings and interviews
3. Summarise: current status, recent decisions, open actions, risks if noted

---

## Risk Detection

### Flag application risks when you see:
- No response after more than 2 weeks post-application
- Interview stages stalling or being rescheduled repeatedly
- Offer deadlines approaching with no decision made
- Multiple applications rejected at the same stage (pattern worth noting)

### Flag opportunity risks when you see:
- Role closing date approaching and application not yet submitted
- A strong-fit role with a gap in the CV that needs addressing
- Dependency on one application with no pipeline backup

### Risk format — append to `risks/active.md`:
```
### [Short Risk Title] — [low/medium/high]
- **Type:** application | opportunity | dependency
- **Project:** [application slug]
- **Person:** [name, if relevant]
- **First noted:** YYYY-MM-DD
- **Last updated:** YYYY-MM-DD
- **Description:** What the risk is
- **Evidence:** Links to meeting notes or project files
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
**Company / Org:** <company>
**Relationship:** Recruiter | Hiring Manager | Contact | Interviewer | Network

## Contact
- Email:
- LinkedIn:
- Phone:

## Context
<Running notes — how we connected, their focus, anything useful>

## Open Actions
<Kept in sync with /actions>

## Meeting History
<Links or refs to relevant meetings — newest first>
```

---

## Project File Format

Use the Application Project Template defined in the Application Pipeline section above.

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

This brain belongs to **Connor Daly** — a 2025 automotive and motorsport engineering graduate actively hunting for entry/graduate level engineering roles, primarily in the automotive sector but open to adjacent industries.

**Key relationships:**
- None yet — update as recruiters and hiring managers are added

**Active priorities:**
- Land first graduate engineering role — primary focus, automotive sector preferred
- Build out application pipeline — CV tailoring, cover letters, tracking progress per company
- Networking — grow contacts in the automotive and engineering space

**Preferences:**
- Friendly, conversational tone
- Proactively suggest improvements — to CVs, cover letters, applications, and the system itself
- British English spelling
- Be direct about what's working and what isn't in applications
