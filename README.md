# case-sprint

A human-in-the-loop Claude plugin for PM case submissions (pre-interview cases and case
competitions). It reads a brief, classifies it into one of six case types, runs the matching
toolkit, builds the deck and prototype, and **stops for your decision at five gates**. You decide
direction and judge quality; Claude does the work in between.

Method source: ISB BTC Handbook 2026 (case competitions, decks and prototypes chapters), paraphrased.

## Pipeline

```
Brief → [brief-reader] → ◆ Gate 1: case type + scope
      → [research-pack: precedent-scout ∥ voc-miner ∥ market-sizer] → ◆ Gate 2: your angle + hypothesis
      → [case-modules for the type] → ◆ Gate 3a: persona, MVP cut, priorities, numbers
      → [storyline] → ◆ Gate 3b: your headlines (one claim per slide)
      → [deck-builder] → [prototype-from-deck]* → ◆ Gate 4a: walk the golden path
      → [deck-qa + fresh-eyes-reviewer] → ◆ Gate 4b: pick fixes
      → submission checklist → ◆ Gate 5: submitted
      → [red-team] panel prep · [case-retro] → improve the skills
```
\* only when the brief requires a prototype or time allows.

## Context use
The workflow is built to stay out of your chat's context window:
- Only **2 skill descriptions** sit in context (`case-sprint`, `pattern-library`). The other 11 skills
  are hidden from auto-loading and run only when the orchestrator dispatches them.
- **Every step runs in a separate subagent** that reads its skill file, writes to the case folder,
  and returns a ≤ 15-line gate card. Research and QA agents run in parallel, in their own contexts.
- **State lives in files** (`case.md` + step files), so you can start a fresh chat at any point and
  say "resume <ID>".
- Direct use of a hidden step: type `/case-sprint:<skill>` (e.g. `/case-sprint:deck-qa`).

## Skills

| Skill | Role |
|---|---|
| `case-sprint` | Orchestrator: workspace, time plan, gates, decision log |
| `btc-playbook` | Reference hub: case types, brief reading, deck blocks, slide craft, metrics stack, prototype standards, frameworks, AI rules, submission checklist, real briefs |
| `brief-reader` | Case type scoring; explicit / implied / open; limits; traps |
| `research-pack` | Dispatches the research agents; synthesises tensions for Gate 2 |
| `case-modules` | 16 analysis modules (personas, journey, MVP, prioritisation, metrics, economics, GTM, right-to-win, sizing, options, stakeholders, root cause, governance, pricing, roadmap gates, risks) |
| `storyline` | Critiques your headlines (claim test, read-only-headlines test, coverage) |
| `deck-builder` | Builds the deck (Claude Slides type or pptx) with the design system |
| `deck-qa` | Skim test, altitude, numbers, block criteria, mechanics → ranked fixes |
| `prototype-from-deck` | Needs golden journey + persona + references → spec → build or builder prompt |
| `red-team` | Kill-assumptions + 20 likely panel questions + answer scaffolds |
| `case-retro` | Post-sprint lessons → concrete skill edits; `LEARNINGS.md` |
| `design-system` | Shared tokens for decks and prototypes; swappable brand layer (v0.1 placeholder) |
| `pattern-library` | Your feature/UX pattern swipe file with screenshots and a taxonomy |

## Agents
`precedent-scout`, `voc-miner`, `market-sizer`, `fresh-eyes-reviewer` (isolated context; run in
parallel where the host supports agents).

## Install

**Claude app (Cowork / desktop):** Customize → Browse plugins → Personal → **+** → *Add marketplace
from GitHub* → `rajdeepnag24/case-sprint` → install **case-sprint**.

**Claude Code:**
```
claude plugin marketplace add rajdeepnag24/case-sprint
claude plugin install case-sprint@case-sprint
```

## Use
- "Start a case: DS01, 48 h window" + paste or attach the brief.
- "Resume DS01" / "where am I in the case?"
- "Add this to my pattern library" + screenshot.
- "Case retro for DS01" after submitting.

Case files are written to `Cases/<ID>-<slug>/` (default: your PM Prep folder): `case.md` (state +
decision log), `01-brief.md` … `08-retro.md`, and `Cases/LEARNINGS.md` across sprints.

## Optional companion skills
Used if installed, never required: [phuryn/pm-skills](https://github.com/phuryn/pm-skills)
(market-sizing, north-star-metric, strategy-red-team, user-personas),
[deanpeters/Product-Manager-Skills](https://github.com/deanpeters/Product-Manager-Skills)
(voice-of-customer-miner), [tyroneross/pyramid-principle](https://github.com/tyroneross/pyramid-principle)
(pyramid-presentation, pyramid-audit).

## Versioning
Bump `version` in `.claude-plugin/plugin.json` on every retro-driven change. Commit messages:
`retro <case ID>: <change>`.
