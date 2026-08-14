# ADR-0012: Consultation Modes

- **Status:** Accepted
- **Date:** 2026-08-14
- **Deciders:** POC owner (practitioner / product), engineering
- **Tags:** domain, modes, flow

## Context

The same underlying principle — *observe energy at the relevant moment, then apply the rules* —
manifests differently depending on the setting. Master Notes v1 identifies several
**consultation modes**, each defining *what* is observed and *when*. This ADR enumerates the
modes and specifies, per mode, how raw observations map to the prediction signals.

Unifying principle:

> **Relevant moment पर energy observe करो।**

## Decision

The practitioner selects a mode after passing Rule 0 (ADR-0011). Each mode defines its
observation points and which signal(s) apply.

### Mode A — Independent Room (transition, four rules)

- Practitioner's back to wall; visitor's LEFT/RIGHT chairs in front; entrance observable
  (ADR-0003).
- **First Energy = ENTRY side**, **Second Energy = SEATING side** → four-rule engine (ADR-0004).

### Mode B — Shared / Doctor's Chamber (transition, four rules)

- People wait and come one-by-one; the original room-entry is **UNKNOWN / NULL / mute**.
- **First Energy** = energy when the person **sits** (check practitioner's Swara + person's side
  at that moment).
- **Second Energy** = energy when the person asks the **actual question** (re-check Swara + side).
- → four-rule engine. Between the two, the practitioner's Swara may have changed (Sunita case,
  ADR-0004); energy is recomputed at each moment.

### Mode C — Sabha / Group (single-energy, position-swara)

- People sit on the practitioner's LEFT/RIGHT; a person asks from their place.
- Observe **questioner's side + active Swara at question time**:
  ```
  QUESTIONER SIDE == ACTIVE SWARA SIDE  →  Bhara  →  Positive
  otherwise                              →  Khali  →  Negative
  ```
- This is a **single Bhara/Khali reading**, not a First→Second transition (Signal E, ADR-0013).

### Mode D — Remote / Position Unknown (single-energy, breath)

- Phone/remote/car/behind — LEFT/RIGHT position not meaningful or unavailable.
- Use **question-time breath**: Saguna (inhale→positive) / Nirguna (exhale→negative), which MUST
  be spontaneous (Signal C, ADR-0013).

### Mode E — Behind-the-Practitioner (single-energy, partial rule)

- Questioner is physically **behind** the practitioner.
- Canonical taught case: **Behind + Surya (RIGHT) active → Positive / YES.**
- **Behind + Chandra (LEFT) active → PENDING** (not yet taught; must not be inferred — ADR-0014,
  ADR-0010).

### Mode F — My Question / Proxy (another person's Swara)

- For the practitioner's **own** question, until they have mastery they should **not** try to read
  the answer from their own Swara directly.
- Instead, use a **proxy**: call/ask a family member, note their **current Swara / spontaneous
  state**, and use *their* spontaneous energy as the indication.
  ```text
  QUESTION = mine
  SWARA SOURCE = another person (spontaneous, not manipulated)
  ```
- **MO-F1:** The proxy's observation must be **spontaneous** (not coached/manipulated), consistent
  with the observation philosophy (ADR-0013 SIG-C2, ADR-0021 EV-0).
- **MO-F2 — PENDING:** the **exact mapping of the proxy's Swara/state to a YES/NO** is not yet taught
  (ADR-0010 §Pending). The app records the proxy observation and shows `Pending` — it does not invent
  the mapping.

### Cross-mode requirements

- **MO-1:** Every mode reuses the same side→polarity conversion (ADR-0002 DR-3), evaluated at the
  observation moment.
- **MO-2:** Transition modes (A, B) feed the four-rule engine; single-energy modes (C, D, E)
  produce a direct Bhara/Khali (or Saguna/Nirguna) reading.
- **MO-3:** Multiple signals may be available in a mode; they are computed independently and
  displayed per ADR-0014 (no invented aggregation).
- **MO-4:** Additional signals (addressing, ADR-0013) may apply across modes wherever the
  practitioner can observe them.
- **MO-5:** A mode must clearly tell the practitioner *which moments to observe* before capture.

### Unified summary

```text
Independent Room : ENTRY → SEATING                        → four rules
Shared/Chamber   : ENERGY@SIT → ENERGY@QUESTION           → four rules
Sabha            : QUESTIONER SIDE + SWARA@QUESTION        → Bhara/Khali
Remote/Unknown   : BREATH@QUESTION (Saguna/Nirguna)        → positive/negative
Behind           : BEHIND + SURYA → positive ; +Chandra → pending
My Question/Proxy: ANOTHER PERSON's spontaneous Swara/state → indication (YES/NO mapping pending)
```

## Consequences

- One core principle, several thin mode adapters — easy to extend as new modes are taught.
- Explicitly marking single-energy vs transition modes prevents misapplying the four rules where
  only a single reading exists.

## Alternatives considered

- **One universal flow** — rejected: observation points genuinely differ by setting; forcing one
  flow would mis-collect data.
