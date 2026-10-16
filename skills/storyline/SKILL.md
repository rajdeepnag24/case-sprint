---
name: storyline
description: >
  Turns case analysis into a deck storyline of assertion headlines (one claim per slide) and
  critiques headlines the user writes. This skill should be used when the user says "build the
  storyline", "check my headlines", "ghost deck", "is this a claim or a topic", "does my deck
  argue something", or when case-sprint reaches step 4.
metadata:
  version: "0.1.0"
---

# Storyline

Load btc-playbook `references/slide-craft.md`, `references/deck-blocks.md` and
`references/case-types.md` (distinctive slide for the type).

## Mode A: user drafts (default, preferred)
Ask the user for their headlines (one line per slide, in order). Then critique only:
1. **Claim test** per line: is it a claim someone could disagree with? Rewrite suggestions only for
   lines that are topics, and keep the user's meaning.
2. **Read-only-headlines test**: read the sequence alone. Does it give the answer? Where does the
   logic jump?
3. **Coverage**: map each explicit deliverable and each published criterion to a slide; list gaps.
4. **Type check**: is the type's distinctive slide present (case-types.md)?
5. **Ambition check**: does the ambition match the brief?
6. **Slide cap**: fits the limit, with an exec summary if asked.

## Mode B: skeleton from decisions (only if the user asks)
Build a ghost deck from the decisions recorded in `case.md` (angle, persona, MVP, priorities,
North Star). Use only the user's decisions; mark every headline "DRAFT: rewrite in your words".
Never introduce a new angle.

## Output (`04-storyline.md`)
Table: # · headline (claim) · block (from deck-blocks) · one exhibit idea · evidence/number source.
Then: gaps list, logic jumps, items moved to appendix.

**Gate 3b**: the user approves the final headlines. Record the approved list in `case.md`.
