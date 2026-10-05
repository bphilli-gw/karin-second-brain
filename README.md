# karin-second-brain

A working repo for your Water PM work at GiveWell. It's seeded with your context (the pod, the grants machinery, where the real docs live) so Claude starts informed instead of generic, and it holds that context across sessions so you're not re-briefing it each time.

The idea: one seeded project you always work out of, a few regular skills, and your connectors wired in.

## How it's organized

- **Water PM work (primary)** — the pod's grants: investigations, renewals, grantee coordination, conditional payments and reporting, site visits, and the documents each grant produces. Reference: `water-pm-reference.md`.
- **The research it serves (context)** — the shape of GiveWell research, the artifacts your grants produce, and where AI helps vs. fails at the work around them. Reference: `research-reference.md`.
- **The spine: `projects/`** — one folder per piece of work you'll want to return to (a grant you're shepherding, a grant page moving through vetting, a renewal, a site visit, a process, a memo), indexed in `projects/active.md`. This is the answer to "how do I keep track of things I might come back to" — folders and a tracker file, not separate app-level projects. See `projects/README.md`.

## Access

Accept the GitHub invite, then clone the repo (Claude can do the clone for you) and open it in Claude Code on your machine (the desktop app, VS Code, or the terminal — a local clone is what lets the Drive connection and `/personalize` work fully). Make sure your Asana, Slack, and Google Drive connectors are on so the skills reach your live work.

The PM and research skills come from GiveWell's two staff plugins. `.claude/settings.json` points the repo at them, so they should appear once you trust the folder — check `/plugin`. If they don't show up, run these and restart:

```
/plugin marketplace add givewellorg/project-management-starter-kit
/plugin install project-management-starter-kit@project-management-starter-kit
/plugin marketplace add givewellorg/givewell-research-skills
/plugin install givewell-research-skills@givewell-research-skills
```

## Using it

The point is to do real work here. A few ways it earns its keep:

- **`/morning-brief`** — pulls your calendar, Asana, and Slack into a short read of what's moving and what's slipping.
- **`projects/active.md`** — have Claude build it from your Asana and what you're actually carrying, then keep it honest. Returning to a parked piece of work weeks later = "pick up projects/<slug>."
- **`/process-meeting`** on 1:1s, pod meetings, and grantee calls — record with Granola, then run it; each meeting becomes tracked notes and action items. `/meeting-prep` does the reverse before a call.
- **`/messages-recap`** when you've lost track of what's waiting on you, and **`/eod-wrap-up`** at the end of the day to turn what you committed to into Asana tasks you approve.
- **`/legibility-review`** before a grantee email, memo, or update goes out — checks it against GiveWell's writing standards.
- **`/done`** at the end of a working session — saves what happened to `memory/` so the next chat picks up where you left off.
- **`/personalize`** — run it once early on (and again whenever the seeded content feels stale) to fill in the placeholders from your real work. It also reads your earlier Claude sessions, so what you've been doing in your old folder isn't lost.
- **The research skills** — `peer-review`, `verify`, `lit-review`, `research-radar`, `qea`, `botec`, `givewell-footnotes`, `data-analysis`: the live versions the research team uses. You won't run them daily, but they're the fastest way to understand the artifacts your grants produce.
- **Spin off your own workflows** — when a task repeats (a grant-page vet request or a financial-reporting reminder to a grantee are obvious first candidates), have Claude write it up as a skill in `.claude/skills/`.

## What's in here

- `CLAUDE.md` — the context Claude reads automatically: your role, the pod, the house rules, the meeting-processing config.
- `people.md` — your pod, PM counterparts on other pods, leadership, and the AI and Tech people you'll work with.
- `water-pm-reference.md` — the pod, the shape of the PM work, the grants already in your Asana, the AI tools already pointed at this seat, and where AI helps and fails in it.
- `research-reference.md` — the shape of GiveWell research and the artifacts your grants produce.
- `projects/` — one folder per project, plus the `active.md` tracker.
- `meetings/` — processed meeting notes.
- `memory/` — session logs from `/done`.
- `sources.md` — links to the real docs, trackers, repos, and Slack channels.
- `guidelines/` — a short summary of GiveWell's writing standards.
- `.claude/settings.json` — the pointer to the two staff plugins; `.claude/skills/` — the three repo skills.
- `playground/` — scratch space.

The context is an October 2026 snapshot, and the structure's a starting point — edit, delete, and add as your work changes it. Something clunky or a skill you want: `/submit-feedback`, or Brendan directly.
