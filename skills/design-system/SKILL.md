---
name: design-system
description: >
  The shared visual system for case decks AND prototypes: tokens (colour, type, spacing, radius),
  deck rules, UI component and state rules, and a swappable brand layer for the case's company.
  This skill should be used when building or styling a case deck or prototype, when the user says
  "apply my design system", "use the case theme", "match Swiggy's colours", "update my design
  system", or shares reference images to evolve the look.
metadata:
  version: "0.1.0"
  status: "placeholder defaults: refine with the user's references"
---

# Case Design System

One system, two surfaces. Structure stays fixed; only the **brand layer** changes per case.

## Files
- `references/tokens.json`: source of truth (base + brand layer).
- `references/tokens.css`: the same tokens as CSS variables for prototypes and HTML decks.
- `references/deck-rules.md`: how tokens apply to slides and exhibits.
- `references/ui-rules.md`: components and states for prototypes.
- `references/references-log.md`: the user's reference images and what was taken from each.

## Apply
1. Decide the brand layer: **neutral** (default, for decks judged on thinking) or **company**
   (prototype of a named company's product, or when the brief asks to look native). For company:
   set `brand.primary`, `brand.onPrimary`, optionally `brand.font`. Never change spacing, type
   scale or component shapes.
2. Decks: follow `deck-rules.md`. With a Slides artifact type, map tokens to its theme; with pptx,
   set theme colours and fonts from tokens.
3. Prototypes: inline `tokens.css`; components and states per `ui-rules.md`. For external builders,
   paste the token list into the prompt.

## Evolve (when the user shares references)
For each image: name 1–3 concrete properties to adopt (e.g., "8 px radius cards", "numbers in
tabular figures", "muted grey ground with one accent") and 1 to avoid. Update the tokens/rules,
log it in `references-log.md`, bump `metadata.version`. Keep the system small: no new colour
unless an existing one cannot do the job.

If the session offers a **Design System** artifact type, offer to publish these tokens and rules
there too, so Claude's Slides and Design types can use them directly.
