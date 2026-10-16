---
name: case-retro
description: >
  Runs a short retrospective after a case sprint and turns it into concrete improvements to the
  case-sprint skills. This skill should be used when the user says "case retro", "what went
  wrong in this sprint", "improve the system", "log learnings", or when case-sprint reaches step 10.
disable-model-invocation: true
metadata:
  version: "0.1.0"
---

# Case Retro

## Ask (one message, max 5 questions)
1. Which step felt slowest, and why?
2. Which output did you throw away or heavily rewrite?
3. Where did the system decide something you wanted to decide (or ask something it should have
   decided)?
4. What did reviewers or squad say about the deck/prototype?
5. Time actually spent vs plan (read the time table in `case.md`).

## Produce (`08-retro.md`)
- 3 keep / 3 change / 1 try-next-time.
- **Skill change proposals**: for each "change", name the skill file and the exact instruction to
  add, remove or reword. Keep each change small and testable on the next sprint.
- Pattern-library candidates: any feature/pattern found during research worth saving.

## Append
Add a dated entry to `<cases-root>/LEARNINGS.md` (create if missing): case ID, type, window,
score/feedback if any, top lesson, skill changes proposed. Read the last 3 entries at the start of
each new sprint (case-sprint step 0) and surface relevant lessons on the Gate 1 card.

## Simulation runs (anti-overfitting rules)
For `mode: simulation` cases, do NOT run the normal retro or append to `LEARNINGS.md`. Instead,
only when the user asks for an **eval review** across runs:
1. Read `_evals/EVALS.md`. A change is eligible only if the same *general* miss appears in
   **≥ 2 runs with different briefs** (ideally different case types).
2. Write each change as a general rule. It must not mention any company, product, persona or
   number from a test brief; reject any change that would only have helped one specific brief.
3. Keep a **holdout**: at least one brief the system has never been tuned on. Re-run it after
   applying changes and compare its ratings; revert if they fall.
4. Never add a test brief or its answer to `btc-playbook/references/real-briefs.md`; that file is
   calibration material, not a test set.
5. Commit as `eval: <rule summary>` and bump the patch version.

Offer to apply the skill changes to the case-sprint repo (commit with message
"retro <ID>: <summary>") once the user approves.
