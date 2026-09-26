# Start Here — Setting Up Your Executive OS on a Mac

This folder is a starter "Executive OS" — a personal assistant system built on Claude that tracks your meetings, contacts, projects, to-dos and risks, all in plain text files you can read yourself. No coding or GitHub knowledge needed — just Claude's desktop app.

Follow these steps in order. It should take about 10 minutes.

---

## What you'll need

- A Mac running a reasonably recent version of macOS (ideally macOS 13 "Ventura" or later)
- A Claude account on a **paid plan** — Pro, Max, Team, or Enterprise. The feature this uses (the "Code" tab) isn't available on the free plan.

---

## Step 1 — Install Claude Desktop

1. Go to **[claude.ai/download](https://claude.ai/download)** and download the Mac version.
2. Open the downloaded file and follow the install prompts (drag Claude into your Applications folder, as with any Mac app).
3. Open Claude from your Applications folder.
4. Sign in with your Claude account.

---

## Step 2 — Put this folder somewhere sensible

You should have received this as a zip file. Double-click it to unzip it — you'll get a folder called something like `Executive-OS`.

**Put it somewhere that gets backed up, not just anywhere on your desktop.** This folder becomes your entire system over time — everything Claude reads and writes lives inside it — so it's worth protecting from day one rather than after you've lost a few months of notes. Good options:

- A folder inside **Google Drive**, **OneDrive**, **Dropbox**, or **iCloud Drive** (if you have desktop sync turned on for any of these, just drop it inside the synced folder)
- Time Machine or another regular backup, if that's already covering your Documents folder

Either way works fine — Claude just needs a normal folder on your Mac to point at. The point is simply that it isn't the *only* copy.

---

## Step 3 — Open it in Claude

1. In the Claude Desktop app, click the **Code** tab at the top of the window.
   - If it asks you to upgrade, that means your account needs to be on a paid plan (see above) — you'll need to do that first.
2. Choose **Local** as the environment.
3. Click **Select folder** and choose the folder from Step 2.
4. Pick a model from the dropdown next to the message box — the most capable one available (e.g. Opus) gives the best results for this kind of work.

---

## Step 4 — Set yourself up

Type a message like this to get started:

> Hi — please read CLAUDE.md and README.md so you understand how this system works, then help me fill in the "Owner Context" section at the bottom of CLAUDE.md for myself. I'll tell you about my role, my priorities, and the key people I work with.

Claude will ask you a few questions and fill that section in for you. This is the single most important step — it's what tells Claude who you are and what matters to you.

---

## Step 5 — Start using it

Some things to try once you're set up:

- **Paste in notes from a meeting or call** — Claude will file it, pull out actions, and update the relevant people/project files automatically.
- **"Prep me for my meeting with [name] tomorrow"** — Claude pulls together everything relevant from past meetings, open actions, and project notes.
- **"Weekly review"** — Claude walks through what's open, checks what's done, and writes a summary.
- **`/db`** — today's brief (meetings, actions due, anything to watch).
- **`/wb`** — this week's brief.

There are also a couple of extra folders you'll grow into rather than need on day one:
- **`/time`** — if you track billable time or expenses per client, `/time` has a rate-card + time-log format and a `/time` command to show totals.
- **`/context`** — a place for durable background notes (your bio, key relationships, project summaries) that Claude pulls in when writing reports or briefs.

The full guide, with all the details, is in **README.md** in this same folder — worth a skim once you're comfortable with the basics.

---

## Ideas to grow into

None of this is set up yet — these are just things worth knowing exist, so you can ask Claude to help you build them in once you're comfortable with the basics. Just describe what you want in plain language in the Code tab and Claude will do the work.

- **[Granola](https://granola.so)** — an app that sits alongside your video calls and produces clean, structured AI notes automatically (participants, summary, action items) instead of you typing them up. This system already has a `/granola` command ready to pull those notes straight in and file them — you'd just need a Granola account and API key. Worth it if you're on a lot of calls.
- **Email triage** — if you connect an email account to Claude (Gmail, Outlook, etc.), you can ask it to sort your inbox against rules you describe once ("anything from a client goes here, newsletters go there, flag anything that needs a reply today") and it'll do this on request from then on. Ask Claude to help you design the rules and write them into `CLAUDE.md`.
- **A daily or weekly brief as a podcast** — once you're running `/db` or `/wb` regularly, you can ask Claude to turn a brief into a short two-person conversational script (a few minutes of "here's what's on today / this week") that you could have read aloud or turned into audio — handy for listening on a commute instead of reading. Ask Claude to draft one from your latest brief and see if the format's useful to you.
- **A standing weekly review** — pair `/wr` (weekly review) with a reminder to run it at the same time each week, so open items never quietly pile up.

If any of these sound useful, just ask — Claude can talk you through what's involved before you commit to setting anything up.

---

## A couple of things to know

- **You don't need to know anything about Git or GitHub.** Some parts of README.md and CLAUDE.md mention git commands (`pu`, "push", commits) — that's an optional extra for people who want version history/backup via a code repository. Ignore those sections entirely; everything else works exactly the same as plain files on your Mac.
- **Claude will ask before changing things**, depending on the "permission mode" shown near the message box in the Code tab. If you'd rather review every change before it happens, set that to **Manual**. If you're happy for it to just get on with routine edits (filing notes, updating action lists), **Accept edits** is faster day-to-day.
- **Everything is plain markdown text files.** You can always open any file in this folder directly (double-click, opens as text) to read or edit it yourself — nothing is locked away or proprietary.

If anything doesn't make sense, just ask Claude directly inside the Code tab — it can explain how the system works, since it's reading the same instructions (`CLAUDE.md`) that drive its own behaviour.
