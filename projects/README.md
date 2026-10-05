# Projects — The Working Area

Everything you're carrying lives here, one folder per project. A "project" is anything you'll want to return to later: a grant you're shepherding, a renewal, a conference meeting plan, a process you're running, a template revision, a memo, performance-review prep. This replaces app-level workarounds (separate Cowork Projects, one endless chat) — the folder plus `active.md` is what lets any fresh chat pick a project back up.

## The pattern

```
projects/
├── active.md                   # the one-page tracker: every live project, one entry each
└── <project-slug>/             # e.g. <grantee>-grant-page/
    └── notes.md                # the question, what you looked at (links), what you found, status
```

Returning to a project = "pick up projects/<slug> — read the notes and active.md entry first."

## active.md — the tracker

Build it from your real work (Asana, your list, what the pod has asked for), not from scratch. Suggested shape per entry (adapt freely):

```markdown
## [Project name]
- **What:** [one line — the question or deliverable]
- **Status:** [active / waiting / parked] — [1 line on where it stands]
- **Next step:** [the next concrete move]
- **Links:** [Drive docs, Asana task, Slack thread — links, not copies]
```

Keep it honest via `/done` at the end of working sessions, and let `/morning-brief` read it each day for what's slipping.

## Rules that keep this useful

- **Link the sources.** `notes.md` holds links to the tracker, the CA, the grant agreement, or the source docs — the live versions stay the source of truth.
- **Log what you looked at and what you concluded, not just the answer.** "Checked the renewal's deliverables against the grant agreement, 4 of 6 reports are in, 2 are blocked on the grantee's M&E data; my read is the timeline slips a month, medium confidence" is what makes the notes useful to future-you and legible to the pod.
- **Say your confidence.** Name how sure you are and what would change it.
- **Parked is a status, not a deletion.** When a project goes dormant, mark it parked in `active.md` with a line on why and what would revive it.
- When a project teaches you something durable about how GiveWell works, route it to `people.md`, `water-pm-reference.md`, or `research-reference.md` via `/done` rather than leaving it buried here.
