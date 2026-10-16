---
name: research-pack
description: >
  Builds the evidence pack for a PM case after the brief is classified: precedents, parallels and
  contrasts, what the company already runs, public user voice (app reviews, Reddit, YouTube),
  and a first market-size estimate. This skill should be used when the user says "research this
  case", "build the research pack", "what's already out there", or when case-sprint reaches step 2.
disable-model-invocation: true
metadata:
  version: "0.1.0"
---

# Research Pack

Input: `01-brief.md` and the Gate 1 decisions in `case.md`.

## Dispatch
If `02a-precedents.md`, `02b-voc.md` (and `02c-sizing.md` when sizing applies) already exist in the
case folder, the orchestrator has run the agents: skip to Synthesis and read those files.
Otherwise run the agents in parallel when an agent tool exists, or do their work in sequence:
| Agent | Brief it with | Returns |
|---|---|---|
| `precedent-scout` | company, problem, case type, scope | precedents, parallels, contrasts, what the company already runs, competitor moves |
| `voc-miner` | product(s)/competitors, persona hints, the decision it informs | pains, workarounds, verbatim quotes with links and counts |
| `market-sizer` | market definition, geography, segments (skip for Type 1 unless the brief asks) | top-down + bottom-up estimate, assumption table |

Give each agent a self-contained brief (it has no conversation history). Ask for links on every
claim. Cap each at roughly the research budget in case-sprint `references/time-budgets.md`.

If an agent tool is unavailable, do the same work directly with web search/fetch; use the user's
browser (Claude in Chrome) for logged-in or JS-heavy pages such as Play Store reviews when available.

## Synthesis (`02-research.md`)
1. **Tensions** (top of file): 3–5 places where evidence conflicts or where the obvious reading
   looks wrong. These feed the user's angle choice.
2. Precedents / parallels / contrasts table.
3. "Already exists" list (company + competitors) → features to NOT propose as new.
4. User-voice table: pain · workaround · frequency signal · best quote · source. Mark the
   bias: public reviews skew angry and vocal; these are hypotheses.
5. Market size (if run) with every assumption sourced or labelled "estimate".
6. Gaps: what we could not find and how the deck will handle it (stated assumption).

## Gate 2 card
Show the tensions and at most three *framings as questions* (e.g., "Is this a trust problem or a
pricing problem?"). Ask the user to write the angle and hypothesis in their own words. Do not
pick one for them.
