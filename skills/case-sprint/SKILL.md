---
name: case-sprint
description: >
  Orchestrates a PM case submission (pre-interview case or case competition) end to end with the
  user as human-in-the-loop. This skill should be used when the user says "start a case",
  "new brief", "case sprint", "run DS01", "here's the case brief", "resume my case", "where am I in
  the case", or pastes/attaches a case brief and asks for help building the submission.
metadata:
  version: "0.1.0"
---

# Case Sprint (orchestrator)

Run the pipeline below. Do the work between gates; **stop at every gate** and wait for the user's
decision. The user decides direction and judges quality; never decide the angle or the storyline
for them (see btc-playbook `references/ai-rules.md`).

## 0. Set up the case workspace
1. Ask once (or reuse from the conversation): case ID (e.g. DS01), time window (48 h / 24 h / 6 h /
   other) and deadline, and where cases live. Default: a `Cases/` folder inside the user's
   connected PM Prep folder; otherwise the working directory.
2. Create `<cases-root>/<ID>-<short-slug>/` with `case.md` from `references/case-template.md`.
   Save the brief verbatim to `00-brief-source.md` (or keep the attached file in `sources/`).
3. Fill the **time plan** in `case.md` using `references/time-budgets.md` for the window.
4. On "resume" / "where am I": read `case.md`, report current gate, decisions so far, time left,
   next action. Nothing else.

## Pipeline

| Step | Run | Output file | Then |
|---|---|---|---|
| 1 | `brief-reader` | `01-brief.md` | **GATE 1**: confirm case type(s), scope in/out, deliverables list |
| 2 | `research-pack` | `02-research.md` | **GATE 2**: user states angle + hypothesis in their own words |
| 3 | `case-modules` for the confirmed type | `03-modules.md` | **GATE 3a**: user picks personas, MVP cut, priorities, numbers to keep |
| 4 | `storyline` | `04-storyline.md` | **GATE 3b**: user writes or approves one claim per slide |
| 5 | `deck-builder` | deck artifact / file | (no gate) |
| 6 | `prototype-from-deck` (only if required or time allows) | `06-prototype-spec.md` + build | **GATE 4a**: user walks the golden path |
| 7 | `deck-qa` (+ fresh-eyes-reviewer agent) | `05-deck-qa.md` | **GATE 4b**: user picks which fixes to apply |
| 8 | Submission checklist (btc-playbook) | ticked in `case.md` | **GATE 5**: user confirms submitted |
| 9 | `red-team` → panel prep | `07-panel-prep.md` | Before the interview |
| 10 | `case-retro` | `08-retro.md` | After submission |

## Gate protocol
At each gate:
1. Show a **decision card**, not a document: max ~12 lines. What was found, the 2–4 options with one
   line of trade-off each, and a recommended default only where the choice is not the user's
   thinking (never recommend the angle or headlines).
2. Use AskUserQuestion when available; otherwise ask in one short message.
3. Record the decision, the reason given, and the timestamp in `case.md` → "Decision log".
4. If the user says "skip" or time is short, apply the time-budget fallbacks and log it.

## Routing rules
- Mixed brief → run the dominant type's must-run modules plus the secondary type's distinctive
  slide only.
- "None of the six" → treat as Type 1 or 2, whichever is closer; say so at Gate 1.
- Prototype: run only if the brief requires it, or if the window is ≥ 24 h and Gate 3 is done with
  > 40% of the time left. Otherwise log "prototype skipped (time rule)".
- If the brief publishes evaluation criteria, copy them into `case.md` and map every deck section
  to at least one criterion.
- Companion skills (use if installed, never required): phuryn `pm-skills` (market-sizing,
  north-star-metric, strategy-red-team, user-personas), deanpeters `voice-of-customer-miner`,
  tyroneross `pyramid-presentation` / `pyramid-audit`. Prefer this plugin's own steps when both exist.

## Time discipline
Keep a running "time left" line at the top of every gate card. When behind plan, propose cuts in
this order: optional prototype → appendix depth → secondary personas → extra risks. Never cut the
assembly-and-check buffer at the end.

## Files
- `references/case-template.md`: the `case.md` skeleton.
- `references/time-budgets.md`: time split per window and fallbacks.
