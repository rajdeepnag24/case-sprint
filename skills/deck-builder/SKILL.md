---
name: deck-builder
description: >
  Builds the case deck from an approved storyline using the case design system, so every slide
  carries one claim and one exhibit. This skill should be used when the user says "build the
  deck", "make the slides from my storyline", "turn this into a deck", or when case-sprint reaches
  step 5.
disable-model-invocation: true
metadata:
  version: "0.1.0"
---

# Deck Builder

Inputs: approved headlines (`case.md` / `04-storyline.md`), `03-modules.md`, the design system
(design-system skill), brief limits.

## Choose the output
1. If the session offers a **Slides** artifact type: create the deck from it (16:9, downloads as
   PowerPoint or PDF). Apply the design system as its theme.
2. If the brief demands .pptx with a template, or no Slides type exists: use the pptx skill.
3. If the brief demands pages (e.g., "3 pages"), build a document in the same design language.

## Build rules
- Headline = the approved claim, verbatim unless the user approved an edit.
- **One exhibit per slide** that the eye lands on: a table, 2×2, flow, chart or wireframe, chosen
  per block in btc-playbook `references/deck-blocks.md`.
- Body = evidence for the claim only: 3–5 lines max, numbers first, sources in a footer line.
- Density through structure (matrix, tree, labelled diagram), never by shrinking text below the
  brief's font floor (default floor 12 pt if none given; 10 pt only for footers).
- Exec summary first when asked or when > 6 slides: the headline sequence compressed into 4–6
  lines.
- MVP flow + wireframe slide whenever a prototype is in scope (it is the prototype's spec).
- Prototype link as a real hyperlink on slide 2 or the exec summary.
- Appendix: assumptions table (number → source/reasoning), extra analysis for panel questions.
- Indian context: ₹, lakh/crore where the brief uses them; otherwise follow the brief's units.

## After building
Run a self-check against `deck-qa` items 1–3 (skim, altitude, numbers), then hand to case-sprint
for the full QA gate. Report slide count vs limit.
