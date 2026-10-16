# UI rules (prototypes)

- **Layout**: mobile-first (390 px) for consumer cases, desktop (1280 px) for B2B dashboards.
  8-pt spacing scale only. Max content width 1120 px on desktop.
- **Type**: `ui` scale; one heading size per level; body 16 px; line-height 1.5.
- **Buttons**: one primary style (`brand.primary` fill, `onPrimary` text, `r-md`), one secondary
  (outline), one text/link. Min tap target 44 px. One primary action per screen.
- **Cards**: `surface`, `r-md`, `shadow.card`, 16 px padding.
- **Inputs/forms**: label above field, helper text below, inline validation message in `negative`.
- **Tables**: left-align text, right-align numbers, tabular figures, zebra off, row dividers `rule`.
- **Navigation**: bottom tab bar (consumer) or left sidebar (B2B); max 5 items.
- **Required states for every data view**: default, **empty** (what it is + one action),
  **loading** (skeleton), **error** (what happened + retry), **first-time user** (no history).
- **In-app guidance for evaluators**: entry screen with "What this is · Who it's for · Try this",
  a dismissible 3-step walkthrough, a visibly highlighted suggested path, "Demo data" badge.
- **Data**: realistic Indian names, ₹ amounts, believable dates/times, internally consistent totals.
- **Accessibility floor**: contrast ≥ 4.5:1 for body text, focus states visible, no colour-only meaning.
- **Don't**: three button styles, mixed radii, lorem ipsum, unlabelled icons, dead links on the
  golden path.
