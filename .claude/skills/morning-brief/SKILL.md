---
name: morning-brief
description: "Karin's daily check-in — pulls calendar, Asana, and Slack into a short, scannable read of what matters today across Karin's projects. Use whenever Karin asks for a morning brief, daily brief, day plan, 'what's on today', 'start the day', or any close variant."
---

# Morning Brief

A lightweight daily check-in. Goal: a 2-minute, scannable read of what matters today across Karin's projects. You surface and propose; you don't act. Nothing is sent or changed without an explicit yes.

## Sources

Connectors available here: **Asana**, **Slack**, **Google Calendar** (if connected), **Google Drive**. The brief is read-only by design: surface things, don't act on them — anything worth sending gets drafted for Karin to send.

Read `CLAUDE.md` and `people.md` for who's who, and `projects/active.md` for what's live. Add channels as Karin confirms them (private channels won't show in search until Karin is a member).

## Step 1 — Gather (in parallel)

Fire these together to keep it fast:

**Calendar** (if connected). Today's events plus tomorrow's, with times in Karin's timezone: Pacific (America/Los_Angeles), three hours behind US Eastern, so East Coast colleagues have been online for hours by the time her day starts and ET-morning meetings land early in hers. Karin's standing meeting set is `[fill in — from the personalize block in CLAUDE.md once confirmed]`. For each meeting, note who it's with (check `people.md`) and one line on what they do, so Karin walks in oriented. Flag 1:1s, Water pod meetings, and grantee or partner calls especially. Remind Karin to record with Granola so `/process-meeting` can capture it after.

**Asana.** Karin's incomplete tasks. Flag overdue items and anything due today. Use these for both PRIORITIES and TRIAGE.

**Slack.** Scan everything Karin is a member of, not a fixed list. Work in this priority order and stop when you've covered what's actionable since ~3 days ago (East Coast colleagues start three hours earlier, so the first stretch of their morning has usually landed before Karin opens Slack):

1. **Pod channels:** #water (`C06DV3ZNV24`, the pod's own channel), #cross-cutting-water (`C07BWDDJ3PY`), #worldbank-crosspod (`C0B7X34KY4F`), #cross-team-grant-logistics (`C043X25J80Z`), and anything in the "Personalize me" block of `CLAUDE.md`
2. **DMs:** Karin's manager (`[fill in]`), Brendan Phillips (`U07HQQT7Y59`), plus anything else recent
3. **Org channels:** #ai-discussion (`C04UKP7NF2Q`), #research-team-meetings (`C07PWHJUTQA`)
4. Anything else Karin is in that's had activity.

Slack search returns false negatives, so read key channels directly rather than trusting an empty search. Classify each item: new request / follow-up needed / FYI-with-action / not-actionable (skip the last). Cross-reference against Asana to avoid duplicates. Include only actionable items; skip the section if nothing's live.

**Open projects.** Skim `projects/active.md` for anything with a near deadline, a "waiting" that's gone quiet too long, or a next step Karin could take today. A grant or process slipping silently is exactly what this section is for.

## Step 2 — Present

Scannable. Only include sections with real content; skip empty ones rather than padding.

```
Good morning, Karin — brief for [Day, Month Date].

CALENDAR
- [Time] [Meeting] — [who they are / prep note]
- Focus blocks: [open time]
- Tomorrow: [preview if notable]

PRIORITIES
1. [Priority — one line on why it's top]
2. ...

ASANA TRIAGE
- [Overdue or due-today; anything that needs re-dating or closing]

SLACK / FOLLOW-UPS
- [New request or pod item — who, what, link]
- Not yet in Asana: [items worth tracking]

PROJECTS
- [Only if a project has a near deadline, has gone quiet while "waiting", or has an obvious next step for today]
```

If a source failed or isn't connected, append a short `SOURCES UNAVAILABLE` line naming it (e.g., "Calendar not connected").

Keep it to a 2-minute read. Plain language, no editorializing.

## Step 3 — Offer

End with: "Anything you want to dig into?"

## Guardrails

- **Read-only by default.** No Slack messages sent, no Asana status changes (complete/drop), no writes to any tracker without an explicit yes. Proposing an Asana comment or a due-date fix is fine; doing it silently is not.
- **Cite sources.** Every item traces to an Asana task, a Slack thread (with link), a meeting note, or calendar.
- **Don't invent.** If a Slack item is ambiguous, flag it as a question rather than inventing a task or a deadline.
