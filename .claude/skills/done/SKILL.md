---
name: done
description: "Karin's end-of-session capture. Before ending a chat, records decisions and durable learnings, writes a session log so the next chat has context, reconciles Asana, and commits. Use whenever Karin says 'done', 'wrap up', 'let's close out', 'end of session', 'save what we did', or is finishing a substantive working chat."
---

# Done — End-of-Session Capture

You're closing out a working session with Karin. Your job is to capture what happened so the next chat starts with full context, instead of Karin re-explaining or digging back through an old chat. Writing things down here is what lets Karin open a fresh chat anytime rather than living in one endless thread.

If this was just a quick one-off question, say so and stop — don't run the full process. Otherwise work through the steps below.

## Step 1: Review the session

Look back through the conversation and pull out:

1. **Decisions made** — choices, prioritization calls, or direction changes
2. **Context updates** — anything that changes `people.md`, `water-pm-reference.md`, `research-reference.md`, `projects/active.md`, or a project's `projects/<slug>/notes.md`
3. **Action items** — things *Karin* needs to do next (not Claude)
4. **Open questions** — unresolved threads to follow up on
5. **Learnings** — durable facts about GiveWell, the pod, the tools, or how Karin likes to work

## Step 2: Update the context files

Mandatory whenever context moved this session. Don't punt to "I'll flag it for next time" — propose the specific edit, get a quick yes, apply it.

1. For each touched file (`people.md`, `water-pm-reference.md`, `research-reference.md`, `projects/active.md`, `projects/*/notes.md`), propose the exact change.
2. Ask Karin a single yes/no, then apply with Edit.
3. If nothing changed, say so explicitly and skip.

## Step 2b: Reconcile Asana

If this session finished or advanced the next move on a tracked task, reflect it — don't leave done work showing as open.

1. **Find candidates.** Search Karin's incomplete tasks with a keyword from what you worked on. Re-run with different keywords rather than stopping at one miss.
2. **Judge each match:** next move done → comment why + complete; advanced → comment the new state, update due date; superseded → complete with a note on what replaced it.
3. **Confirm before changing Asana.** Show the proposed close-outs and get a single yes/no. Don't create new tasks unless the session surfaced a genuinely new item Karin owns the next move on.
4. If no tracked work was touched, say so and skip.

## Step 3: Write a session log

Save to `memory/sessions/YYYY-MM-DD-brief-topic.md`:

```markdown
# Session: [brief topic]
*Date: YYYY-MM-DD*

## Decisions
- [decision]

## Context Updates
- [file]: [what changed]

## Action Items (Karin)
- [ ] [item]

## Open Questions
- [question]

## Learnings
- [durable insight worth remembering]
```

## Step 4: Capture durable learnings

Only for things true across sessions, not just today's context. Route each to where it belongs so it auto-loads next time (prefer these files over letting notes pile up in session logs):

- A person or who-owns-what fact → `people.md`
- A fact about the pod's grants, processes, or how water PM work gets done → `water-pm-reference.md`
- A fact about GiveWell research itself → `research-reference.md`
- Project state → `projects/active.md` and the project's `notes.md`
- A GiveWell-process fact, tool gotcha, or working convention → `CLAUDE.md` (House rules / Conventions)
- A standing preference about how Karin wants you to work → the **Personalize me** / **How I want Claude to respond** blocks in `CLAUDE.md`
- A workflow that's now repeated a few times (a weekly grant-status roundup, a renewal-prep checklist) → offer to pin it down as a skill in `.claude/skills/`
- A skill behaved wrong or has a rough edge → run `/submit-feedback` to file it to Brendan

Show the proposed edits, get a yes, apply. If nothing is durable, say so in one sentence and move on.

## Step 5: Commit

This is Karin's repo, so everything should end up on `main` (no long-lived feature branches). Run `git status`, stage the session log plus any context-file edits from this session, and commit:

```
Session YYYY-MM-DD: [same brief topic as the session-log filename]
```

Then get that commit onto `main`. How you do it depends on where this session is running. Check with `git branch --show-current`:

- **On `main`** (desktop app or CLI): just `git push`. That's it.
- **On a `claude/*` branch**: Claude Code on the web pins every session to its own branch and can't push to `main` directly. This is normal platform behavior, not a mistake to undo. Publish the branch and fold it into `main` so Karin never has to touch GitHub:
  - `git push -u origin HEAD`
  - `gh pr create --fill --base main && gh pr merge --merge --delete-branch`
  - Confirm it landed: `git log origin/main -1 --oneline`
  - If `gh` is unavailable or the merge is blocked, don't leave Karin thinking it failed. Say plainly: "Your changes are saved on a branch. On GitHub, open the repo, click **Compare & pull request**, then **Create pull request** and **Merge pull request**. That copies them into `main`."

Report the commit hash and how it reached `main` (direct push or merged PR).

## Step 6: Confirm

Show Karin a short summary:

```
Session captured:
- [N] decisions logged
- [N] context updates applied
- [N] Asana tasks closed/updated (or "no Asana changes")
- [N] action items noted
- Session log: [filepath]
- Committed: [short hash] — pushed to origin/main
```

## Guidelines

- Concise reference notes, not transcripts.
- Don't fabricate decisions or learnings — capture only what actually happened.
- Draft, don't send: no Slack messages go out, no Drive writes; Asana and repo edits need an explicit yes.
- If nothing meaningful happened, say so and skip the full process.
