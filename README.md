# M5L Executive OS — Personal Knowledge OS for Executives

A structured knowledge base and management system built on top of [Claude Code](https://claude.ai/claude-code). It ingests meetings, tracks people, manages actions, and surfaces risks — all through natural conversation.

---

## What This Is

M5L Executive OS turns Claude Code into a personal chief of staff. You paste a meeting link or transcript, and it automatically:

- Saves a raw transcript
- Extracts actions, decisions, and risks
- Updates your people files, project files, and action register
- Flags risks and relationship signals

Over time it builds a dense, interconnected knowledge base about your work — and because it lives in a git repo, it's version-controlled, searchable, and portable.

---

## How It Works

The system is driven by a single `CLAUDE.md` file that gives Claude Code detailed instructions for how to behave in this repo. Claude Code reads this file at the start of every session and follows its rules.

The key behaviours are:

| Trigger | What happens |
|---------|-------------|
| Paste a Granola URL or transcript | Full meeting ingestion pipeline runs automatically |
| `close N` or `close N, M, P` | Actions marked done, people/project files synced |
| `weekly review` | Open actions listed, you confirm done ones, summary produced |
| `prep for [meeting/person]` | Context brief assembled from all relevant files |
| `pu` | Staged commit and push to remote |

---

## Prerequisites

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) installed and authenticated
- A git repo (this one) — local or with a remote (GitHub, GitLab, etc.)
- Optional: [Granola](https://granola.so) for AI-structured meeting notes (the ingestion pipeline works best with Granola URLs, but also accepts pasted text)

---

## Setup

### 1. Clone or fork this repo

```bash
git clone <this-repo-url> my-brain
cd my-brain
```

### 2. Personalise CLAUDE.md

Open `CLAUDE.md` and update the **Owner Context** section at the bottom. This is the most important step — it tells Claude who you are, what your priorities are, and who the key people in your world are.

```markdown
## Owner Context

This brain belongs to **[Your Name]** — [one sentence about your role and focus].

**Key relationships:**
- [Person] — [their role and relevance]
...

**Active priorities:**
- [Priority 1]
- [Priority 2]
...

**Preferences:**
- [Any style/tone preferences — e.g. "Direct and concise", "British English"]
```

### 3. Configure Claude Code permissions (optional but recommended)

To avoid permission prompts for routine file edits, create `.claude/settings.local.json`:

```json
{
  "permissions": {
    "allow": [
      "Edit(actions/**)",
      "Edit(people/**)",
      "Edit(projects/**)",
      "WebFetch(domain:notes.granola.ai)"
    ]
  }
}
```

> Note: `settings.local.json` is gitignored by default. This is intentional — it may contain machine-specific paths. If you want consistent permissions across devices, move the rules to `.claude/settings.json`.

### 4. Start Claude Code in this directory

```bash
claude
```

That's it. Claude will read `CLAUDE.md` and be ready to go.

---

## Folder Structure

```
/
├── CLAUDE.md                      # The brain — system instructions for Claude
├── meetings/                      # Processed meeting notes
│   ├── transcripts/               # Raw unedited transcripts (never modified)
│   │   └── archive/YYYY/MM/       # Archived transcripts (>28 days)
│   └── archive/YYYY/MM/           # Archived meeting notes (>28 days)
├── people/                        # One file per person
│   └── archive/YYYY/MM/           # Archived (dormant relationships — manual)
├── projects/                      # One file per initiative
│   └── archive/YYYY/MM/           # Archived (completed/abandoned — manual)
├── actions/                       # Weekly action registers
│   └── archive/YYYY/MM/           # Archived weeks (>28 days old)
├── weekly/                        # Weekly prep notes and retros
│   └── archive/YYYY/MM/           # Archived weeks (>6 weeks old)
├── daily/                         # Daily and weekend briefs
│   └── archive/YYYY/MM/           # Archived briefs (>28 days)
└── risks/
    ├── active.md                  # Live risk register
    └── closed.md                  # Resolved / closed risks
```

### File naming

| Type | Convention | Example |
|------|-----------|---------|
| Meeting | `YYYY-MM-DD-<short-title>.md` | `2026-03-13-layerd-checkin.md` |
| Transcript | `YYYY-MM-DD-<short-title>.transcript.md` | `2026-03-13-layerd-checkin.transcript.md` |
| Person | `<firstname-lastname>.md` | `sarah-jones.md` |
| Project | `<project-slug>.md` | `series-a-prep.md` |
| Actions | `actions-YYYY-Www.md` | `actions-2026-W11.md` |
| Weekly | `YYYY-Www.md` | `2026-W11.md` |

---

## Usage Guide

### Ingesting a meeting

Paste a Granola URL or raw transcript text into Claude Code. It processes automatically — no confirmation needed.

```
https://notes.granola.ai/t/your-meeting-id
```

Or paste transcript text directly. Claude will ask for the date and participants if they're not clear from the content.

### Closing actions

```
close 5
close 3, 7, 12
```

Actions are marked done, moved to the closed section, and synced across people and project files.

### Weekly review

```
weekly review
```

Claude lists all open actions, asks you to confirm which are done, then produces a summary and updates the weekly file.

### Meeting prep

```
prep for my call with Sarah Jones tomorrow
prep for the board meeting
```

Claude pulls context from the relevant people files, recent meetings, open actions, and project files.

### Quick push

```
pu
```

Stages, commits (with a generated message), and pushes to your remote.

---

## Example Files

The repo includes example files to show the expected format:

- `people/example-person.md` — person file template
- `projects/example-project.md` — project file template
- `actions/actions-example.md` — weekly actions format
- `risks/active.md` — risk register format

Delete or rename these once you've created your own.

---

## Tips

**Start with your people.** Create files for the 10-15 people you interact with most. Even a stub with role and relationship is enough — Claude will fill in context as meetings are ingested.

**Create project files early.** The more projects you have files for, the better Claude can cross-reference and surface relevant context.

**Use Granola.** The ingestion pipeline is significantly richer with structured Granola notes than with raw transcripts. Granola extracts participants, titles, and action items which Claude uses to enrich its analysis.

**Commit regularly.** The `pu` shortcut makes this easy. A clean git history means you can always roll back if something goes wrong.

**Review your risks file weekly.** Claude appends to it automatically but never resolves risks on its own — that's intentional. Reviewing and closing risks is a useful forcing function.

---

## Adapting for Your Context

The `CLAUDE.md` is designed to be modified. Some things you might want to change:

- **Meeting types** — add your own classification rules (e.g. `board`, `investor`, `sales`)
- **Risk categories** — add domain-specific risk types relevant to your work
- **Shortcuts** — add your own trigger phrases (e.g. `board prep` → specific behaviour)
- **Action format** — adjust the fields to match how you think about tasks
- **File structure** — add folders for your context (e.g. `/board`, `/fundraising`)

---

## Built With

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) — Anthropic's CLI for Claude
- [Granola](https://granola.so) — AI meeting notes (optional)
- Markdown + Git — the world's most durable knowledge format

---

## Licence

[MIT + Commons Clause](./LICENSE) — use it freely at work or in your own projects, fork it, adapt it. You just can't sell it.
