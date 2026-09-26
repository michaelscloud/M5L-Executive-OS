# Podcast Script (pod)

Turn a weekly review into a natural, engaging two-host podcast script.

## Usage
- `/pod` — generate a podcast script for this week's review
- `/pod W12` (or any week number) — generate for a specific week

## Behaviour

### Determine the target week
- If no argument: use the current week (`YYYY-Www`)
- If an argument like `W12` or `13` is given: resolve to the correct year and week

### Source files to read

Read all of the following before generating the script:

1. **Weekly review:** `weekly/YYYY-Www.md` — primary source. If it does not exist, say so and stop.
2. **Context files** (load silently — use to enrich the script, not to summarise): whatever exists in `/context` (e.g. `profile.md`, `relationships.md`, `projects-summary.md`, and any per-client/company files added under "Adapting for Your Context")

Use the context files to add colour that the weekly review doesn't spell out — who a person is and why a project matters, what a risk actually means in practice. Don't summarise the context files directly; weave the background in naturally as HOST A or HOST B explain things to the listener.

### Generate the script

You are a podcast script writer. Your job is to turn a weekly review document into a natural, engaging two-host conversational podcast script.

FORMAT RULES:
- The script should produce roughly 10-12 minutes of audio (approximately 1,500-1,800 words)
- Use exactly two hosts: HOST A and HOST B
- Mark every line with the speaker name in square brackets, e.g. [HOST A] or [HOST B]
- No stage directions, sound effects, or production notes — just dialogue
- Write in natural spoken English, not written English. Use contractions, filler words sparingly, and conversational rhythm.

HOST PERSONALITIES:
- HOST A is the anchor. They drive the structure, introduce topics, and keep things moving. Tone: warm, organised, slightly dry humour. Think "the one who actually read the agenda."
- HOST B is the colour commentator. They ask follow-up questions, react naturally, highlight what's interesting, and add energy. Tone: curious, enthusiastic, occasionally teasing. Think "the one who makes it fun to listen to."

STRUCTURE (follow this arc):
1. COLD OPEN (~30 seconds): HOST A and HOST B exchange a quick, natural greeting. HOST A sets up what the episode covers — no theme music references, just straight into it.
2. WHAT GOT DONE (~4-5 minutes): Walk through accomplishments and completions from the week. HOST A introduces each item, HOST B reacts and asks follow-ups. Celebrate wins, note what was harder than expected.
3. WHAT DIDN'T GET DONE (~2-3 minutes): Honest look at what slipped or stalled. Keep it constructive — HOST B can probe why things slipped without being judgmental. Acknowledge blockers vs. deprioritisation.
4. WHAT'S COMING UP (~3-4 minutes): Preview the week ahead. Key meetings, deadlines, focus areas. HOST B can ask "what are you most looking forward to?" or "what's the one thing that would make next week a win?"
5. WRAP-UP (~30 seconds): Quick, punchy close. No forced catchphrases. Just a natural "right, that's the week" energy.

TONE GUIDELINES:
- This is a private productivity podcast, not a public broadcast. It should feel like two colleagues catching up over tea, not a polished media production.
- Be specific — use actual names, project names, and details from the review. Don't genericise.
- It's OK to be honest about things that went wrong or were frustrating.
- Keep energy conversational but not manic. This is for listening in the car, not hyping up a crowd.
- Match the language/spelling convention set in "Owner Context" (e.g. British vs. American English).

IMPORTANT:
- Do NOT add intro/outro music cues
- Do NOT add [PAUSE] or [LAUGHS] or any non-dialogue directions
- Do NOT invent information not in the source material
- DO make the conversation flow naturally — it shouldn't sound like someone reading a list aloud
- DO have HOST B occasionally push back, ask "why?", or highlight something the review glosses over

Generate the script, then save it to `weekly/YYYY-Www-pod.md` using the Write tool. Confirm the file path when done.
