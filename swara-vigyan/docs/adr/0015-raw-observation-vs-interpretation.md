# ADR-0015: Raw Observation vs Interpretation — Data Model & Rule Engine

- **Status:** Accepted
- **Date:** 2026-08-14
- **Deciders:** engineering, POC owner
- **Tags:** architecture, data-model, rule-engine

## Context

The Guru's teaching is still evolving (pending rules, ADR-0014). A design that hard-codes
*interpretations* would make historical consultations impossible to re-evaluate when a rule is
later corrected or added. Master Notes v1 states the principle directly:

> **Raw observation और interpretation अलग रखें** — पहले facts store करो, फिर derive करो, ताकि गुरु
> कोई rule change/add करें तो historical raw observations दोबारा process हो सकें।

## Decision

### Three-layer pipeline

```text
[1] RAW OBSERVATIONS  →  [2] DERIVATION (signals)  →  [3] PRESENTATION
   (facts, immutable)      (pure functions, versioned)   (independent signals + conflicts)
```

- **DA-1 — Store raw facts, not conclusions.** The record of a consultation stores *what was
  observed* (nostril, sides, breath phase, addressing order, mode, timestamps), **not** derived
  polarities or verdicts.
- **DA-2 — Derivation is pure & reproducible.** Signals (ADR-0004/0013) are pure functions from raw
  observations. Given the same raw record and the same ruleset version, they always produce the
  same output.
- **DA-3 — Reprocessable history.** Because interpretation is not baked into storage, any stored
  raw record can be re-derived under an updated ruleset. Derived results, if cached, are clearly
  marked with the ruleset version used and are safe to discard/recompute.
- **DA-4 — Ruleset versioning.** The interpretation rules carry a version (baseline: *Master Notes
  v1*). New/changed rules bump the version; reprocessing is re-running derivation at a new version.

### Raw observation schema (illustrative, per consultation)

```yaml
meta:
  ruleset_version: "master-notes-v1"
  mode: independent_room        # | shared_chamber | sabha | remote | behind
  timestamp: <captured at runtime>
practitioner:
  ready: true                   # Rule 0 gate (ADR-0011); false ⇒ no derivation
  active_nadi: chandra          # chandra(left) | surya(right) | sushumna
  active_nostril: left          # left | right | both/none
  breathing_phase: inhale       # inhale | exhale | unknown
  breath_spontaneous: true      # false ⇒ breath signal invalid (ADR-0013 SIG-C2)
questioner:
  position: right               # left | right | behind | unknown
  entry_side: right             # left | right | unknown/null (mode-dependent)
observations:
  # each moment records the ACTIVE NOSTRIL AT THAT MOMENT + the observed side,
  # so energy can be re-derived faithfully (Sunita case, ADR-0004)
  first_moment:  { active_nostril: right, observed_side: right }   # e.g. entry / sit
  second_moment: { active_nostril: left,  observed_side: right }   # e.g. seating / question
  addressing_order: before_question   # before_question | after_question | none
question:
  raw_text: "Sir, क्या यह काम सफल होगा?"   # optional; see privacy (ADR-0008)
```

Notes:
- Each observation moment stores the **active nostril at that moment**, not a pre-computed
  Bhara/Khali — polarity is derived later so a Swara change between moments is preserved.
- `ruleset_version` makes reprocessing explicit and auditable.

### Derivation output (not stored as source of truth)

```text
derive(raw) → {
  signals: [ {id, reading: Positive|Negative|Mixed(rule)|Pending|NotApplicable, why} ... ],
  conflict: none | pending,           # ADR-0014
  gated: false                        # true if Rule 0 failed → no signals
}
```

### Requirements

- **DA-5:** The domain/derivation layer has **no DOM/UI dependency** and is unit-testable in
  isolation (aligns with ADR-0005 layering).
- **DA-6:** Storage of raw records is subject to privacy rules (ADR-0008): local-only, opt-in, and
  `question.raw_text` (potentially identifying) is optional and off by default.
- **DA-7:** No derived verdict is ever persisted as authoritative; only raw + ruleset_version are.

## Consequences

- **Positive:** Future rule corrections apply retroactively; the knowledge base and the app stay in
  sync as the Guru teaches more.
- **Positive:** Clean testability and a stable data contract for the eventual mobile app.
- **Negative:** Slightly more storage/compute than caching verdicts — negligible at this scale and
  worth the reprocessability.

## Alternatives considered

- **Store the final verdict per consultation** — rejected: freezes an interpretation that may be
  revised, defeating the reprocessing principle.
