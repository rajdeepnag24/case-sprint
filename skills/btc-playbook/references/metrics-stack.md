# Metrics stack (layered, with targets)

Name the layers out loud; a flat list of metrics is the weak answer.

| Layer | Definition | Test |
|---|---|---|
| **North Star** | Captures delivered value; moves only if users are genuinely better off | Could it rise while users get worse off? If yes, it is a vanity metric |
| **Inputs (2–4)** | Levers the team can actually influence that drive the North Star | Can a squad own and move it this quarter? |
| **Outputs** | Revenue, retention, margin: matter but lag | Lagging; report, don't steer by them |
| **Guardrails** | Must not degrade while optimising the primary | Who could be harmed by the optimisation? |
| **Counter-metrics** | How the primary metric could be gamed | What behaviour would inflate it without value? |

**Targets, not words.** "7-day retention, 30% by month 6" is a metric; "retention" is a word.

## Choosing the goal (GAME)
Goals (agree user + business objective) → Actions (what users can do) → Metrics (convert key
actions) → Evaluate (recommend, then name trade-offs and limits).
Lifecycle lens (AARRR) when unsure which stage matters. A new feature on an established product is
usually an activation or retention question, not acquisition; saying so shows judgement.

## Multi-sided products
Build the tree per side (e.g., customers, restaurants, riders) and state whose metric wins in
year one and why.

## Measurement design traps (raise unprompted for extra credit)
- Selection bias / causality (users of a feature convert better: cause or self-selection?).
- No A/B possible (few enterprise customers, pricing change for all): use pre/post with controls,
  cohort comparison, synthetic control, qualitative signals.
- Can't see content (encryption, private cloud): measure behaviour around it.
- Mix shift / Simpson's paradox: overall flat while every segment falls.

## AI features add
Task success, groundedness/accuracy, escalation rate, latency, cost per completed task, and the
business outcome (resolution rate, conversion, time saved).
