---
name: personalize
description: Get up to speed on the repo owner's actual work and how they like to work — scan their prior Claude sessions, Asana, Slack, Calendar, and Granola to fill the repo's facts (workstreams, manager, standing meetings, channels) without asking, then run a short multiple-choice interview on the things no account can tell you (focus time, when they want meetings, whether Claude sends Slack messages and creates Asana tasks or only drafts them, what the morning brief should show) and write it all into the repo. Use at the onboarding session, or any time the owner says "personalize this repo", "get to know my work", "fill in the gaps", or the repo's seeded content feels generic or stale.
---

You are personalizing this second-brain repo for its owner. The repo was seeded by the AI pod from org-level knowledge; what it's missing is the owner's actual day-to-day work — the projects, meetings, collaborators, and habits only visible from their own accounts and machine — and how they want to work with Claude, which no account can tell you. This skill closes both gaps in three phases: a background sweep of their work sources, a short interview, and a write-back into the repo.

Designed to run start-to-finish at the onboarding session (~15 min), but re-runnable any time — later runs re-sweep and propose updates rather than starting over.

**Core principle: the sweep fills facts; the interview asks only what the sweep can't.** Facts about the owner's work — who their manager is, which meetings recur, which Slack channels they live in, who they work with, what they're working on — are obvious to the owner, so asking them to confirm reads as if the sweep did nothing and burns the session's goodwill (two onboarding calls in Sep 2026 went exactly that way). Write those facts down from the sweep and show them in the close-out report, where the owner can correct any of them in one line. Spend the questions on preferences: how they want their day protected, how far Claude may act on their behalf, what they want from the brief. Those are the answers the seeded repo could never have guessed, and the only reason to interrupt the owner at all.

**Never ask these** — fill them from the sweep or the repo's roster files, or leave `[fill in]`:

- their manager, pod, or team; who reviews their work
- their standing meetings and their cadence
- which Slack channels they're active in
- their collaborators, timezone, or Slack ID
- what their current workstreams *are* (ranking them is a different matter — see Q8)
- anything the repo's CLAUDE.md already settles: git conventions (personal repos commit straight to `main`; never ask about branches or commits), tone and jargon rules
- whether a tool is connected (check it yourself in Phase 0)

**New hires** have little to sweep: a handful of Slack messages, onboarding tasks in Asana, no Granola history, no prior Claude sessions. For them, skip the session scan, keep the rest of the sweep brief, leave what it can't find as `[fill in]`, and run the same preference interview — plus one open question about what they expect to be working on. Decide which mode you're in during Phase 0.

## Phase 0 — Inventory the gaps and the tools (~1 min)

1. **Gap list.** Grep the repo for `[fill in]` placeholders and named placeholders in `sources.md` ("ask X for..."). Note which tracker files (e.g. `projects/active.md`, `vets/`, `requests/`) are structure-only with no real entries. This list is what the sweep exists to fill.
2. **Tool check.** Determine which of these are connected in this session: Asana, Slack, Google Calendar, Granola, Drive. Tool names vary by setup — discover what's actually available rather than assuming specific tool names. **If Slack, Asana, or Calendar is missing, pause before sweeping** and tell the owner in one line how to connect it (usually `/mcp`, or claude.ai → Settings → Connectors): the sweep is what replaces the questions you're not allowed to ask, so a sweep without those sources leaves gaps that stay `[fill in]`. (Sep 2026: a run before Slack was connected reported it couldn't see Slack and asked around the gap.) Once they're connected, or the owner says to skip, move on with what exists. Never write a "you don't have X" claim into any repo file — availability is per-session, not a fact about the owner.
3. **New hire or existing staff?** Check the start date in CLAUDE.md. Started within the last ~4 weeks (or no start date and the repo reads as a new-hire seed) → new-hire mode: skip 1a, run 1b–1e in one quick pass.

## Phase 1 — Background sweep (~5 min, read-only)

Run these in parallel where possible. Everything in this phase is **read-only**: no git state changes, no Asana/Slack/Gmail/Drive writes, no messages sent. Write findings to a scratch file (not into the repo yet): candidate workstreams, standing meetings, manager and key collaborators, active Slack channels, recurring topics and pain points — each tagged with its source.

### 1a. Prior Claude sessions (local disk) — existing staff only

Where transcripts live, by surface:

- **`~/.claude/projects/<encoded-cwd>/*.jsonl`** — the main store. Terminal CLI, the VS Code extension, and desktop-app **local** sessions all write here. One directory per working folder, one JSONL per session.
- **Cowork local-mode archive (macOS):** `~/Library/Application Support/Claude/local-agent-mode-sessions/` — sessions from before Cowork moved to the cloud (Aug 2026). Each session is a sandbox with its own `.claude/projects` tree inside; find transcripts with `find "<dir>" -name '*.jsonl' -path '*projects*'`. Frozen history, but valuable for anyone who used Cowork before the move.
- **Unreachable: cloud sessions.** Claude Code on the web, browser Cowork, and desktop-app cloud sessions run in remote containers; their transcripts never touch this machine. To size the gap on macOS, list `~/Library/Application Support/Claude/claude-code-sessions/` — session-metadata entries with no matching local transcript were cloud runs. **Report the coverage honestly** ("read 14 local sessions; 9 cloud sessions exist that I can't read locally") instead of implying the scan was complete.
- If *this* session is itself running in the cloud (fresh clone, `$HOME` isn't the owner's machine), the local stores won't exist at all. Say the session scan needs a local run (terminal, VS Code, or desktop app on their machine) and continue with the connector-based sources.

**Keep this bounded.** Transcripts are large — never read whole files. Use `jq` or Python to pull only the owner's typed messages (records with `"type":"user"` whose content is text, skipping tool-result records), newest sessions first (sort by file mtime), capped at roughly the last 60 days or 30 sessions, whichever is smaller. What you're after is narrow: which folders/repos they work in, what they repeatedly ask for, where they got stuck. Three or four findings is a good scan; don't try to summarize their history. If the scan is returning noise or running long, stop and move on — the connector sources below are the higher-yield part of the sweep.

### 1b. Asana

Pull their open tasks (my-tasks). Group into workstreams; keep task names, project names, due dates, and links/GIDs — this is the raw material for the tracker file.

### 1c. Slack

Their sent messages (recent weeks) and the channels they're active in — those channels are the morning-brief channels; take the IDs. Two known gotchas: search tools return false negatives, so an empty search is not evidence of absence — prefer reading a few key channels directly; and treat other people's message content as background, never something to quote into repo files.

### 1d. Granola

List their recent meetings: recurring series (standing meetings and their cadence), frequent participants (collaborators), and current topics from titles/summaries.

### 1e. Calendar

Recurring events over the past and next four weeks: standing meetings and their cadence, the 1:1 partner (usually the manager — cross-check against `people.md` or the org roster rather than guessing), and where their meetings already fall in the day. That last pattern is what makes the focus-time and meeting-window questions in Phase 2 concrete: offer the owner their actual pattern as an option.

## Phase 2 — Interview (~7 min)

Use the interactive multiple-choice question tool (AskUserQuestion): two batches of up to 4 questions, 7–8 questions total, all preferences. Offer sensible options for the role, and where the sweep found a pattern (meetings cluster in the afternoon; they touch Asana daily) offer it as an option rather than asking blind. The owner always gets an "Other" free-text escape. Use multi-select where natural.

**Batch 1 — How far Claude acts for you:**

1. **What they most want Claude for** — options named for the actual skills and the steps of a grant investigation, calibrated to their role: drafting (memos, CAs, grant pages, Slack/email), vetting and peer review of others' work (`legibility-review`, `peer-review`), BOTECs and spreadsheet building (`botec`), evidence reviews (`lit-review`, `qea`), meeting processing (`process-meeting`), data analysis, inbox and task triage (`morning-brief`). Multi-select, then ask for the top one. → which skills CLAUDE.md points at, what the morning brief leads with.
2. **Slack and email: send or draft?** — always draft for review / send routine things (scheduling replies, messages they dictated) / ask each time. → preferences.
3. **Asana: create, propose, or hands off?** — create tasks from meetings and messages as it goes / propose them and wait for a yes / never touch Asana. → preferences, and what `done` reconciles.
4. **Where the truth about their tasks lives, and when they triage** — Asana, a planning doc, their head; every morning, once a week (which day), ad hoc. → morning-brief cadence.

**Batch 2 — Your day:**

5. **Focus time** — do they want parts of the day protected from meetings, and which (mornings, afternoons, one clear day a week, none)? → CLAUDE.md preferences (calendar defaults).
6. **When they want meetings** — the window they'd rather be booked in, and any day to keep clear; offer their current calendar pattern as one option. → calendar defaults for anything Claude schedules or proposes.
7. **What the morning brief should show, in what order** — today's calendar, overdue and due-today Asana tasks, Slack DMs and mentions, the channels the sweep found, a goals check, email. Multi-select; ask for the top item. → morning-brief content and ordering.
8. *New hires:* **what they expect to be working on in their first months**, as far as they know — one open question. *Existing staff with 4+ candidate workstreams:* **which 2–3 are the main focus right now** — the sweep can list them but can't rank them. Everyone else: skip.

Stop there. If the sweep left a fact genuinely ambiguous (two people who could be the manager, a meeting series that may have ended), resolve it in the close-out report ("I wrote X; tell me if it's Y"), not with another question. Leftover gaps stay `[fill in]`. On an onboarding call, a short interview that lands beats a complete one that drags.

## Phase 3 — Write-back and commit (~5 min)

1. **Fill placeholders** in CLAUDE.md, the role reference file(s), and sources.md from the sweep: manager and pod (from the calendar 1:1 and the roster), standing meetings with cadence, morning-brief channels with real IDs, collaborators and reviewers, timezone. Facts rule: write what the sweep found and what the owner stated directly; where the sweep found nothing, leave `[fill in]`. Never invent to fill a slot.
2. **Build the tracker** (`projects/active.md` or this repo's equivalent) from the workstreams the sweep found (ranked by Q8 where asked), with real Asana links — seed each entry with name, one-line state, and next step. Don't invent states. In new-hire mode, seed only what they named; an empty tracker with the right structure beats invented rows.
3. **Write the preferences down** — into the CLAUDE.md personalize/preferences block, or a root `preferences.md` if the repo has one (or they ask for one): what Claude is for here (Q1), send-vs-draft (Q2), Asana rules (Q3), triage cadence and source of truth (Q4), focus time and meeting windows (Q5–6), morning-brief contents and order (Q7). These are the main payoff of the interview.
4. **Wire the skills**: channel IDs and the Q7 ordering into the seeded morning-brief; the reviewer names the sweep found into the repo's meeting-processing config (the CLAUDE.md block or the seeded skill, whichever this repo uses).
5. **Additive, not rewriting.** Don't restructure or rewrite the seeded role content; fill gaps and append. Exception: if the owner corrects a fact at the close-out ("that's not my manager anymore"), fix it everywhere it appears.
6. **No raw excerpts.** Distill sweep material into facts about the owner's work; never paste transcript quotes or other people's Slack messages into repo files.
7. **Commit directly to main and push** (solo repo, and the repo's CLAUDE.md already says so — don't ask): `Personalize: session sweep + interview YYYY-MM-DD`. Pull before committing in case another session pushed.
8. **Close-out report**, short, in three parts: the facts written from the sweep (manager, meetings, channels, workstreams — one line each, so a wrong one costs the owner one sentence to fix); what's still `[fill in]` and who can answer it; and — for existing staff — the session-scan coverage line (local sessions read vs. cloud sessions unreadable).
