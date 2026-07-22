# Time & Expense Tracking (time)

Track time, expenses, and mileage per client/engagement — whether it's actually invoiced or just tracked to demonstrate value contributed (e.g. sweat equity ahead of a funding round or investment decision).

## Usage
- `/time log <client> <duration> <description>` — log a time entry
- `/time expense <client> <amount> <description>` — log an expense
- `/time mileage <client> <miles> <description>` — log mileage at the current HMRC rate
- `/time <client>` — show the log and running totals for a client
- `/time` — show totals across all tracked clients

## File path
`time/<client-slug>.md` — one file per client/engagement (e.g. `time/acme-corp.md`)

## Behaviour

### Rate cards
Each client file opens with a Rate Card: hourly rate, minimum billable increment, mileage rate, a **Purpose** (invoiced — cash actually changes hands — or value-tracking only, e.g. demonstrating sweat equity for a future funding/investment conversation), and any other terms (e.g. "parts/expenses only, no day rate", "pro bono"). Read it before logging anything — apply the minimum/rounding rule specified there, not a default, and never treat a value-tracking entry as something to actually invoice.

### Logging time
- Record the actual duration alongside the counted duration (after applying the client's minimum) — don't silently discard the real number
- One row per session in the Time Log table: Date | Workstream | Description | Actual | Counted | Rate | Value | Outcome / Next | Source
- **Workstream** groups entries when a client has more than one distinct thread under one rate card (e.g. "Product" vs "Infra"). Use a single consistent label if there's only one.
- **Outcome / Next** is a short phrase capturing what came out of the session and what happens next (e.g. "Requirements captured; follow-up scoping TBC") — keep it to one line
- Source links back to the meeting or project file that generated the entry

### Logging expenses
One row in the Expenses Log: Date | Description | Amount | Notes

### Logging mileage
- Confirm the current mileage allowance rate for your jurisdiction before applying it (rates change periodically — don't assume a previously-used figure still holds)
- One row in the Mileage Log: Date | Route | Miles | Rate | Amount | YTD miles running total (so any annual mileage threshold doesn't get missed)
- Head the Mileage Log with the current tax year and its reset date, since annual thresholds and YTD counts typically reset on a fixed date each year

### Summary
Keep a running Summary section at the **top** of each client file, right after the title: total time value (£ and hours), total expenses, total mileage (£ and miles, with tax year noted), and a grand total labelled according to the rate card's Purpose — "invoiced/invoiceable to date" for cash engagements, "value contributed (not invoiced)" for tracking-only ones. Update it whenever a new entry is logged. Separate each major section (Summary, Rate Card, Time Log, Expenses Log, Mileage Log) with a horizontal rule (`---`).

### Auto-logging during meeting ingestion
When the Meeting Ingestion Pipeline processes a meeting for a client that has a rate card in `/time`, add a time log entry as part of ingestion — don't wait to be asked. If duration isn't obvious from the calendar/transcript, use the scheduled meeting length.

## Client File Format

```markdown
# <Client> — Time & Expenses

## Summary
- **Time value to date:** £X (Y hours counted)
- **Expenses to date:** £X
- **Mileage to date:** £X (Z miles — YYYY/YY tax year)
- **Total value contributed (not invoiced): £X** — or **Total invoiced/invoiceable to date: £X** if the rate card's Purpose is Invoiced

---

## Rate Card
- **Rate:** £X/hour
- **Minimum:** X hours per session
- **Mileage:** confirm current rate for your jurisdiction
- **Purpose:** Invoiced | Value-tracking only (not invoiced — state why, e.g. "demonstrating sweat equity ahead of a funding round")
- **Notes:** <anything else — invoicing cadence, deposits, exceptions>

---

## Time Log
| Date | Workstream | Description | Actual | Counted | Rate | Value | Outcome / Next | Source |
|------|------------|-------------|--------|---------|------|-------|----------------|--------|

---

## Expenses Log
| Date | Description | Amount | Notes |
|------|-------------|--------|-------|

---

## Mileage Log (YYYY/YY tax year — resets Month YYYY)
| Date | Route | Miles | Rate | Amount | YTD Miles |
|------|-------|-------|------|--------|-----------|
```
