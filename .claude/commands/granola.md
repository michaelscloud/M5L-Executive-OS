# Granola Note Fetcher

Fetch one or more Granola notes via the API and process them through the meeting ingestion pipeline.

## Trigger

When the user provides one or more Granola URLs in the format:
`https://notes.granola.ai/t/{note-id}`

## Steps

### 1. Read the API key
Read the key from `~/.claude/granola-api-key` using the Read tool. Trim any whitespace.

> Store your Granola API key at `~/.claude/granola-api-key` (plain text, one line). Never commit this file.

### 2. Map share URL to API note ID
Share URLs use UUIDs but the API uses `not_` prefixed IDs (e.g. `not_C6di8NRh0qtsfC`).
Use `GET /notes` to list recent notes and match by title/date to find the correct API ID.

Share URL format: `https://notes.granola.ai/t/{uuid}-{short-code}`
API ID format: `not_XXXXXXXXXX`

### 3. Fetch each note from the API

Use bash curl for each note:

```bash
curl -s -H "Authorization: Bearer <key>" \
  "https://public-api.granola.ai/v1/notes/<note-id>?include=transcript"
```

Fetch all notes in parallel where possible.

### 4. Process each note

For each fetched note, run the full **Meeting Ingestion Pipeline** as defined in CLAUDE.md:
- Save raw transcript to `meetings/transcripts/`
- Create processed meeting note in `meetings/`
- Update `/actions` for the current week
- Update relevant `/people` files
- Update relevant `/projects` files
- Scan for risks and append to `risks/active.md` if needed

### 5. Report back

Summarise what was extracted and updated across all notes.

## Notes

- The API key is stored at `~/.claude/granola-api-key` — never log, display, or commit it
- If a note returns 404, it may not have an AI summary yet — flag it and skip
- If a note returns 429, pause and retry after a few seconds
- API base URL: `https://public-api.granola.ai/v1/`
