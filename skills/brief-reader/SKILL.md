---
name: brief-reader
description: >
  Reads a PM case brief and classifies it into one of the six case types, separating what is
  explicitly asked, implied and deliberately left open, plus hard limits and evaluation criteria.
  This skill should be used when the user says "read this brief", "what type of case is this",
  "break down this case", "what are they really asking", or when case-sprint reaches step 1.
disable-model-invocation: true
metadata:
  version: "0.1.0"
---

# Brief Reader

Load btc-playbook `references/case-types.md` and `references/brief-reading.md` first.

## Steps
1. **Restate the ask** in one sentence, in plain words.
2. **Classify.** Score each of the six types 0–3 against the signal words and the shape of the
   deliverables. Report the dominant type, any secondary type, and confidence. If the top two
   scores tie, say what single fact would decide it. If nothing fits, say "none of the six" and
   name the closest.
3. **Three layers.** List: explicitly asked (each → a section), implied (with the reasoning:
   "revenue target → needs a financial model"), deliberately open (each → a choice that will be
   judged; note what criterion should justify it).
4. **Hard limits and mechanics.** Slide/page/word caps, font floor, required sections and order,
   format, naming, link rules, deadline. Quote exact wording for any ambiguous rule and flag it as
   "ask placement rep".
5. **Evaluation criteria.** Copy any published criteria verbatim. If none, infer the 3–4 the type
   implies (from case-types.md "What it really tests").
6. **Traps.** Name 2–3 likely mistakes for this brief (e.g., over-scoping, proposing something the
   company already runs, missing the implied model, hedging between options).
7. **Questions only the user can answer** (e.g., personal experience that gives a lens). Max 3.

## Output (`01-brief.md`)
Sections in this order: One-line ask · Case type (scores table, dominant, secondary, confidence) ·
Explicit / Implied / Open · Hard limits · Evaluation criteria · Traps · Draft section skeleton
(topics only, NOT claims; claims come at Gate 3b) · Questions for the user.

Then hand back to case-sprint for **Gate 1**. Do not research or ideate solutions here.
