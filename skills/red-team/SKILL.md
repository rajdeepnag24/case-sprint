---
name: red-team
description: >
  Attacks a case submission's load-bearing assumptions and prepares the user for the interview
  that is built on the deck: likely panel questions, weak numbers, rejected alternatives, and
  answers in the user's own reasoning. This skill should be used when the user says "red team my
  deck", "what will the panel ask", "prep me for the case interview", "stress test this", or when
  case-sprint reaches step 9.
disable-model-invocation: true
metadata:
  version: "0.1.0"
---

# Red Team + Panel Prep

Inputs: final deck, `case.md` (decisions and reasons), `03-modules.md`.

## 1. Attack the assumptions
List every claim the deck asserts. Keep the load-bearing ones (if false, the recommendation dies).
For each: steelman it, then attack the strong version. Write "Fails if ___" concretely. Rank by
impact × likelihood × cheapness to check. Do not invent doubt where evidence is solid; say so.

## 2. Likely panel questions (20)
Cover: why this persona over others · why this feature/option over the rejected ones · where each
key number came from and what happens if it is 50% off · what the company already does here · the
metric that could be gamed · what you'd cut with half the budget · what you'd do differently ·
the hardest stakeholder objection · one "is this even worth solving" question · AI cost/quality
trade-off if AI is involved. Mark the 5 most likely.

## 3. Answer scaffolds
For each top-5 question: the user's own reason from the decision log, the evidence, the honest
limitation, and the fallback ("if that assumption breaks, I'd …"). Short bullets, not scripts.
Interviewers punish rehearsed answers and reward reasoning under challenge.

## Output (`07-panel-prep.md`)
Kill-assumptions table · 20 questions (top 5 starred) · scaffolds · "numbers to memorise" box.
Offer a 15-minute mock: ask the top 5 one at a time, push back once on each, then give feedback.
