# ADR-0014: Signal Independence, Conflicts & Pending Rules

- **Status:** Accepted
- **Date:** 2026-08-14
- **Deciders:** POC owner (practitioner / product), engineering
- **Tags:** domain, logic, integrity

## Context

Multiple signals (ADR-0013) can apply to one consultation and may **disagree** — e.g. a Bhara
reading says Positive while a Nirguna breath says Negative. The Guru has **not yet taught** how to
resolve such conflicts, nor certain individual cases (e.g. Behind + Chandra). The cardinal rule of
this project is: **do not invent** what has not been taught.

## Decision

### Principles

- **CF-1 — Independence:** Every applicable signal is computed and stored **independently**. The
  app never silently combines signals into a single verdict using an unspecified rule.
- **CF-2 — Surface conflicts:** When applicable signals disagree, the app **displays the conflict**
  — each signal with its reading — and explicitly states that a resolution rule is **pending**. It
  does not pick a winner or average them.
- **CF-3 — Pending outcomes are first-class:** Cases the Guru has not taught (e.g. Behind+Chandra,
  Sushumna, conflict priority) resolve to a `Pending` state with a short note, never a guess.
- **CF-4 — No fabricated priority:** No implicit precedence between signals (e.g. "breath beats
  position") may be encoded until it is explicitly taught and recorded in a future ADR.
- **CF-5 — Agreement is reportable, not merged:** If all applicable signals agree, the app may say
  "all available signals indicate Positive/Negative", but this is a *report of agreement*, not a
  new aggregated rule.

### Behaviour matrix

```text
All applicable signals agree      → report the shared reading (as agreement, not a merge)
Signals disagree                  → show each reading + "Conflict: resolution rule PENDING"
A signal's case is untaught       → that signal returns PENDING (e.g. Behind+Chandra)
Practitioner not ready (Rule 0)   → no signals computed at all (ADR-0011)
```

### Known pending items (tracked; must not be invented)

- Priority/resolution when signals conflict.
- Behind + Chandra result.
- Sabha reading when questioner is on the Khali side (exact rule).
- Consultation/prediction rule when **Sushumna** is active.
- Swara-transition timing rules.
- How interpretation changes with different question types.
- How to combine Saguna/Nirguna with Bhara/Khali.
- Exceptions / special cases.
- Meethi Goli selection rules (color/object/timing relation to Swara), if any.

(This list mirrors ADR-0010 §Pending; both must be updated together as the Guru teaches more.)

### Requirements

- **CF-6:** The signal-aggregation layer is a thin presenter that only **groups and displays**
  independent signal outputs; it contains no hidden decision logic.
- **CF-7:** Every `Pending` outcome links to (or names) the specific open question so the
  practitioner understands *why* no verdict is given.

## Consequences

- **Positive:** The tool stays faithful — it never manufactures certainty the tradition hasn't
  granted. Conflicts become learning prompts for the next Guru session.
- **Negative:** Users sometimes get "pending/conflict" instead of a crisp answer — this is
  intended honesty, not a defect.

## Alternatives considered

- **Majority vote / weighted score across signals** — rejected: it would invent an aggregation
  rule the Guru has not taught (violates the project's core integrity principle).
