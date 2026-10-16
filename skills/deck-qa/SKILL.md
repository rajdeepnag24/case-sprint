---
name: deck-qa
description: >
  Quality-checks a case deck before submission: the two-minute skim test, claim headlines,
  consistent altitude, number provenance and consistency, building-block acceptance criteria,
  slide limits and submission mechanics. This skill should be used when the user says "QA my
  deck", "check the deck", "skim test", "is this ready to submit", or when case-sprint reaches step 7.
metadata:
  version: "0.1.0"
---

# Deck QA

Report findings; do not edit unless the user picks fixes at Gate 4b.

## Checks (in order)
1. **Two-minute skim.** Dispatch the `fresh-eyes-reviewer` agent with ONLY the slide headlines and
   one-line exhibit descriptions (no case context). It returns what it thinks the answer is. If its
   answer differs from the user's angle in `case.md`, that is finding #1.
2. **Headlines are claims.** Flag each topic headline (btc-playbook `references/slide-craft.md`).
3. **Consistent altitude.** Flag slides that drop into operational detail in a strategic deck, or
   the reverse.
4. **Numbers.** Extract every number with its slide. Flag: same metric with different values,
   numbers with no source/assumption, totals that do not add up, unit mix-ups (₹ vs $, lakh vs
   million).
5. **Block acceptance.** For each slide, check its block's criteria in
   btc-playbook `references/deck-blocks.md` (e.g., personas show the workaround and the prioritisation criterion;
   metrics have targets, guardrails and counter-metrics; GTM has acquisition economics and an order;
   risks have leading indicators).
6. **Type check.** The case type's distinctive slide exists and is strong.
7. **Coverage.** Every explicit deliverable and published criterion maps to a slide.
8. **Visual consistency.** One type scale, one palette, aligned, font floor respected, one focal
   exhibit per slide, no all-text slides. If slides can be rendered to images, look at them.
9. **Mechanics.** btc-playbook `references/submission-checklist.md`: limits, naming, links
   (public, opened logged-out), prototype link early.

## Output (`05-deck-qa.md`)
Ranked list: **Blocker** (breaks a rule or the skim) → **Major** (weakens a judged criterion) →
**Polish**. Each: slide #, issue, why it matters, a concrete fix, minutes to fix.
Gate 4b card: blockers plus the top 5 majors, with total fix time vs time left.
