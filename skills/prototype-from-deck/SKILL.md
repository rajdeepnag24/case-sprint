---
name: prototype-from-deck
description: >
  Turns a case deck into a clickable prototype with minimal back-and-forth, starting from a
  golden journey, a persona and visual references. This skill should be used when the user says
  "build the prototype", "prototype from my deck", "make the MVP clickable", "write the Lovable/v0
  prompt", or when case-sprint reaches step 6.
metadata:
  version: "0.1.0"
---

# Prototype from Deck

Load btc-playbook `references/prototype-standards.md` and the design-system skill.

## Hard preconditions (refuse to build until all three exist)
1. **Golden journey**: the one path a reviewer walks, as numbered steps from entry to visible result.
2. **Persona**: the prioritised persona from Gate 3a (context, job, workaround).
3. **References**: at least one visual reference (screenshot, app, or pattern-library entry), or an
   explicit "use the design system defaults".
If any is missing, extract it from the deck's MVP flow / wireframe slides; if still missing, ask
for exactly that item and stop.

## Step 1: Prototype spec (`06-prototype-spec.md`)
- Purpose line shown on the entry screen ("What this is, who it's for, what to try").
- Screens table: screen · primary action · data shown · states (default / empty / loading / error)
  · fidelity (hi for golden path, lo for supporting).
- Golden-path script with realistic, consistent demo data (Indian names, ₹, believable timestamps).
- Brand layer: company colours/font if the case is for a named company; else design-system default.
- Pattern references used (from pattern-library) and why.
- Out of scope list.
Show the spec as **Gate 4a pre-check** in ≤10 lines; build only after the user says go.

## Step 2: Build
- Default: a single self-contained web prototype as an artifact (use frontend-design guidance if
  available), hostable as a public link.
- If the user wants an external builder (Lovable, Bolt, v0, Replit, Figma Make): output one prompt
  that names screens, primary actions, data, states, the golden path and design tokens; nothing
  left for the tool to invent.
- Build order: golden path end to end → in-app guidance (entry screen, suggested path, labelled
  demo data) → empty/error states → polish.

## Step 3: Verify
Walk the golden path yourself; list any dead end. Remind the user to open the link logged out on
phone and laptop. **Gate 4a**: the user walks it and approves or lists fixes.
