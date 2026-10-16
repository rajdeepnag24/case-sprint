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

## Execution model: keep the user's chat context-light (mandatory)
The main conversation is a **control room**, not a workspace. It holds only gate cards and
decisions; all reading, research, analysis and building happens in subagents and on disk.

1. **Paths.** Note this skill's base directory when it loads. Step skills are siblings:
   `<skills-root>/<step>/SKILL.md`; playbook files are `<skills-root>/btc-playbook/references/…`.
   Step skills are hidden from auto-loading on purpose; never load them into the main thread.
2. **Dispatch every step to a fresh subagent** (general-purpose) with a self-contained prompt:
   - "Read `<skills-root>/<step>/SKILL.md` and follow it. Resolve 'btc-playbook `references/x`' as
     `<skills-root>/btc-playbook/references/x`."
   - Case folder path, the input files to read, the output file(s) to write.
   - "Write all output to files. Reply with ONLY the gate card (≤ 15 lines), nothing else."
3. **Research and QA agents run from the main thread** (subagents cannot start subagents):
   - Step 2: dispatch `precedent-scout`, `voc-miner` and (if needed) `market-sizer` **in parallel**,
     each with an output path (`02a-precedents.md`, `02b-voc.md`, `02c-sizing.md`); then dispatch the
     research-pack synthesis subagent to read those files and write `02-research.md`.
   - Step 7: dispatch `fresh-eyes-reviewer` with only headlines + exhibit lines and output path
     `05a-skim.md`; then dispatch the deck-qa subagent.
4. **Never paste file contents into the main chat.** If the user wants detail, give the file path
   or summarise in ≤ 5 lines via a subagent.
5. **Main-thread replies ≤ 15 lines**, gate cards included. Decisions are written to `case.md`
   immediately, so nothing needs to stay in conversation memory.
6. **Fresh chat is always safe.** Everything needed to continue is in the case folder. Suggest a new
   chat after Gate 2 and after Gate 3b on long cases ("resume <ID>" picks up from `case.md`).
7. **Exception:** if a subagent reports it cannot create the deck (no Slides/Artifact tool), run
   deck-builder in the main thread, then return to the rules above.
8. If no subagent tool exists at all, run steps inline but still write to files and show only the
   gate card.

## Simulation mode (evaluating the workflow without training it on the test)
Trigger: case ID starts with `SIM-`, or the user says "simulation", "test run", "eval run",
"replay". Write `mode: simulation` at the top of `case.md`.

**Isolation (no carry-in):** do not read `LEARNINGS.md`, `_evals/`, other case folders, memory, or
any file outside this case folder except the plugin's own skill files. Tell every subagent the same.
Do not use the user's known solution for this case (e.g. a past team submission) until Gate 5.

**No carry-out:** do not write to `LEARNINGS.md` or memory; do not propose or apply skill edits
during or right after the run. Gates run normally, the user still decides.

**Scoring:** at each gate, ask the user for a 1–5 quality rating and one line on what was missing;
log time per step. After Gate 5 (or when the user stops), write `09-eval.md`: ratings, time vs plan,
misses, and, only now, a comparison with any reference solution the user provides.

**Aggregation:** append one row to `<cases-root>/_evals/EVALS.md` (case ID, type, window, gate
ratings, total time, top 3 misses as *general* patterns: no company names or case specifics).
Skill changes come only from case-retro's eval review (see case-retro "Simulation runs").

## 0. Set up the case workspace
1. Ask once (or reuse from the conversation): case ID (e.g. DS01), time window (48 h / 24 h / 6 h /
   other) and deadline.
   **Locate the cases root before saying it is missing**, in this order:
   a. A full path the user gives (Windows paths like `C:\Users\…\PM Prep\Cases\SIM-MMT-01` are on
      their computer: reach them through the linked-computer tools, not the local shell).
   b. Folders connected to this chat: list them (e.g. `ls $HOME/mnt/` in the computer's shell or the
      folder-listing tool) and look for `*/Cases/` (default: `PM Prep/Cases/`).
   c. The working directory.
   d. Only then ask. If no computer/folder is connected at all, say so in one line and offer two
      fixes: link this chat to the computer with the PM Prep folder, or attach the brief file.
   Never conclude a case folder is missing without checking a–c.
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
