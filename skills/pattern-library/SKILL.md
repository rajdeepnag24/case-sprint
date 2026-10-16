---
name: pattern-library
description: >
  Maintains the user's library of product features and UX patterns (with screenshots) and pulls
  relevant patterns into cases and prototypes. This skill should be used when the user says "add
  this to my pattern library", "save this feature", "log this screenshot", "find patterns for
  trust in marketplaces", "what onboarding patterns do I have", or when prototype-from-deck needs
  references.
metadata:
  version: "0.1.0"
---

# Pattern Library

## Where it lives
Default: a `Pattern Library/` folder in the user's connected PM Prep folder, containing
`index.md` (one row per entry) and `shots/` (screenshots named `<app>-<feature>-<n>.png`).
Create both from `references/index-template.md` on first use. Ask once if the location differs.
If the user's squad keeps a shared feature bank, link entries to it rather than duplicating.

## Add an entry
From a screenshot, link, or description:
1. Identify app, feature and **pattern type** (taxonomy in `references/taxonomy.md`).
2. Fill: user problem it solves · mechanism (why it works) · metric it likely moves · trade-off ·
   case types it helps (1–6) · tags.
3. Save the screenshot to `shots/`, add the row to `index.md`. Ask the user for the one-line "why
   it works" if not obvious; their judgement is the point of the library.
Keep entries short: one row, one screenshot, one insight.

## Find patterns
Search `index.md` by pattern type, tag, case type or metric. Return the top 3–5 with screenshot
paths and one line on how each could apply to the current case. For prototypes, hand the chosen
entries to prototype-from-deck as references.

## Weekly tidy (optional)
Merge duplicates, add missing tags, and list pattern types with fewer than 2 entries as gaps to
look for in daily app use.
