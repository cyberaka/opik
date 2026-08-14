# ADR-0013: Additional Prediction Signals

- **Status:** Accepted
- **Date:** 2026-08-14
- **Deciders:** POC owner (practitioner / product), engineering
- **Tags:** domain, signals

## Context

Beyond the four-rule energy transition (Signal B, ADR-0004), Master Notes v1 teaches several
other prediction signals. Each is an **independent reading**; this ADR specifies them. How they
are combined (or not) is ADR-0014.

## Decision

### Signal catalogue

| Signal | Source | Reading |
|--------|--------|---------|
| **A — Bhara/Khali** | A single side vs current active Swara | Bhara→Positive, Khali→Negative |
| **B — Energy transition** | First→Second energy (ADR-0004) | one of four rules |
| **C — Saguna/Nirguna (breath)** | Practitioner's breath at exact question moment | Inhale→Saguna→Positive; Exhale→Nirguna→Negative |
| **D — Question addressing** | Order of addressing vs question | Sadhak-first→Positive; Sadhak-later→Negative |
| **E — Position-swara (Sabha)** | Questioner side vs active Swara side | Same side (Bhara)→Positive; else Negative |
| **F — Behind-position** | Person behind + active nadi | Behind+Surya→Positive; Behind+Chandra→**Pending** |

### C — Saguna / Nirguna (breath)

```text
INHALE  → SAGUNA  → POSITIVE
EXHALE  → NIRGUNA → NEGATIVE
```

- **SIG-C1:** Observe the breath phase at the **exact moment** the question is spontaneously asked.
- **SIG-C2 (spontaneity, critical):** The breath MUST be natural. Deliberately inhaling/exhaling
  to force a result is **invalid** and MUST NOT be recorded as a valid reading. The app captures a
  `spontaneous` flag; a non-spontaneous breath yields **no** Saguna/Nirguna signal.
  > **Swara/Breath को बनाना नहीं है — जो naturally मौजूद है उसे observe करना है।**

### D — Question addressing

```text
SADHAK FIRST → QUESTION   =  POSITIVE   ("Sir, ... <question>")
QUESTION → SADHAK LATER    =  NEGATIVE   ("<question> ..., Sir, ...")
```

- **SIG-D1:** Capture whether the practitioner (Sadhak/Sir/Guru) was addressed **before** the
  question began or **during/after** it.
- **SIG-D2:** Rationale (for help text, not logic): naming the Guru/Ishwar before beginning a task
  is treated as an auspicious start.
  > **पहले साधक, फिर सवाल = Positive; पहले सवाल, फिर साधक = Negative।**

### E — Position-swara (Sabha)

Single Bhara/Khali reading, per Mode C (ADR-0012):

```text
QUESTIONER SIDE == ACTIVE SWARA SIDE → Bhara → Positive
otherwise                            → Khali → Negative
```

### F — Behind-position

```text
PERSON BEHIND + SURYA (RIGHT) ACTIVE → POSITIVE / YES
PERSON BEHIND + CHANDRA (LEFT) ACTIVE → PENDING   (do not infer)
```

- **SIG-F1:** The Behind+Chandra outcome is **not taught yet**; the app records the observation
  and returns a "pending — rule not yet known" state (ADR-0014, ADR-0010). It MUST NOT guess.

### General requirements

- **SIG-1:** Each signal is computed by a pure function of its raw inputs and returns one of
  `Positive | Negative | Mixed(rule) | Pending | NotApplicable`.
- **SIG-2:** A signal that lacks its inputs (or fails a validity condition like spontaneity)
  returns `NotApplicable` / `Pending`, never a default polarity.
- **SIG-3:** Signals are surfaced independently; they are **not** silently merged (ADR-0014).

## Consequences

- A uniform signal interface (`→ Positive|Negative|Mixed|Pending|NotApplicable`) makes signals
  composable later without changing their individual definitions.
- Encoding spontaneity and the Behind+Chandra "pending" as first-class outcomes prevents invalid
  or invented predictions.

## Alternatives considered

- **Collapsing all signals into a single score now** — rejected: the Guru's aggregation rule is
  not yet taught (ADR-0014); collapsing would invent one.
