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

1. Read `actions/open.md` (the full live picture) and the current week's actions file (what moved this week)
2. Scan meetings from that week
3. Present all open actions as a numbered list — ask the owner to confirm which are done
4. Mark confirmed actions as closed with today's date — `[x]` in their week file, and removed from `actions/open.md`
5. Produce a summary: what happened, decisions made, actions closed, still open, risks flagged, anything to carry forward
6. Create the weekly note at `weekly/YYYY-Www.md`
7. Compare against the weekly brief (`weekly/YYYY-Www-brief.md`) if it exists — note anything planned that didn't happen, or unplanned things that did
8. **Write the Executive Summary last, and place it at the top of the file** (see below)
9. Offer to commit and push

---

## Executive Summary

Every weekly review opens with this. It is **written last** — it can only be produced once the rest of the review is done — but it **sits first in the file**, because it is the part that actually gets read.

It covers the whole picture, professional and personal together, and it must be readable in **90 seconds**. Brevity is the point. If it runs long it has failed, however good the content.

```markdown
## Executive Summary

**State of the week:** <2 sentences, professional and personal>

**Top 3 for the week ahead:**
1. <specific, actionable>
2. <specific, actionable>
3. <specific, actionable>

**Biggest opportunity:** <the one emerging thing worth leaning into>

**The one risk needing a decision:** <singular — not a list>

**Personal check-in:** <one line — family, health, whatever matters outside work>

**Momentum:** <net positive or negative, and why — one line>
```

### How to reach those conclusions

Work through these five lenses before writing. They are analytical passes, not sections to output — the summary above is the only thing that appears in the file.

| Lens | Ask |
|------|-----|
| **Actions** | What is most urgent? What are the top 3 to focus on? **Which actions are at risk of slipping with no forcing function?** |
| **Projects** | One-line health per active project (momentum, blockers). Which single project needs the most attention, and why? Any cross-project dependencies? |
| **Meetings** | Most significant outcomes and what they mean. Commitments made that need follow-through. Relationship opportunities to act on quickly. Lead with insight, not summary. |
| **Risks** | Which risk needs the most urgent action? Any changing status? One concrete action per high/medium risk. |
| **Personal** | Commitments outside work needing active support. Home tasks most impactful to clear. Anything with a real deadline. **One thing that could be done this weekend to make next week lighter.** |

The two bolded questions are the ones that most often surface something the rest of the review misses — an action quietly dying for want of a forcing function, and a small piece of weekend effort that buys back the following week.

### Rules

- Direct, no hedging and no filler. Match the tone/spelling conventions set in "Owner Context".
- Full names on first mention in each section.
- "Top 3" means exactly three. Forcing the choice is the value; a longer list is the thing this section exists to avoid.
- "The one risk" is singular. If two genuinely compete, pick one and say why it beat the other.
- State momentum as a judgement, positive or negative, with a reason. Do not hedge it into meaninglessness.
- If a lens produces nothing worth reporting, say so in a few words rather than padding it.
