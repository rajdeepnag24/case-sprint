---
name: case-modules
description: >
  Runs the analysis modules a PM case needs for its case type: users and jobs, journey and pain,
  MVP, prioritisation, metrics stack, economics, GTM, right-to-win, market sizing, options and
  rejection, stakeholder map, root cause, governance, buyers and pricing, roadmap gates, risks.
  This skill should be used when the user says "run the modules", "build personas for the case",
  "do the metrics for this case", "work out the economics", "right to win", or when case-sprint
  reaches step 3.
metadata:
  version: "0.1.0"
---

# Case Modules

1. Read `case.md` (type, scope, angle + hypothesis) and `02-research.md`.
2. Pick modules from btc-playbook `references/case-types.md` → "Toolkit per type": all must-run
   modules, plus "usually add" modules only if time allows.
3. Run each module using `references/modules.md`. Each module's spec gives inputs, method,
   output shape and the **decision the user must make**.
4. Ground every claim in `02-research.md` or label it "assumption" with a number and a reason.
   Build any numbers in a spreadsheet when there are more than ~5 linked figures (use the xlsx skill
   if present), so the user can change an input and see the effect.
5. Write `03-modules.md`: one section per module, each ending with "Decision needed:".
6. **Gate 3a** card: list only the decisions (persona, MVP cut, priority order, numbers to keep),
   each with 2–3 options and trade-offs. Record answers in `case.md`.

Respect the angle the user set at Gate 2. If a module's evidence contradicts the hypothesis, say
so plainly on the gate card instead of silently changing direction.
