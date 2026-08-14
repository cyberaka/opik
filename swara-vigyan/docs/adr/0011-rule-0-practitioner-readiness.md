# ADR-0011: Rule 0 — Practitioner Readiness Gate

- **Status:** Accepted
- **Date:** 2026-08-14
- **Deciders:** POC owner (practitioner / product), engineering
- **Tags:** domain, safety-gate, ux

## Context

Master Notes v1 places a precondition before *any* prediction: the practitioner must be in a
state to read Swara reliably. A blocked nose or a disturbed mind makes the Swara reading
unreliable, and an unreliable reading must not be turned into a prediction.

> **पहले साधक clear होगा, तभी Swara clear पढ़ पाएगा।**

## Decision

### The gate

Before any mode/observation flow, the app presents **Rule 0**: a readiness checklist the
practitioner confirms. Prediction is **blocked** until readiness is affirmed.

Checklist (all must be clear/true):

- Nose clear (both nostrils physically unobstructed enough to read Swara)
- Swara clearly identifiable (which nostril is active is unambiguous)
- Natural breathing
- Ears clear
- Mouth clear
- Mind clear
- No significant stress
- Mental clarity to observe

```text
CLEAR BODY/SENSES + CLEAR MIND + CLEAR SWARA
                    ↓
             PREDICTION ALLOWED

Nose blocked / disturbed / stressed / Swara unclear
                    ↓
             SWARA UNRELIABLE → DO NOT PREDICT
```

### Requirements

- **R0-1:** The readiness gate MUST precede observation entry in every mode.
- **R0-2:** If readiness is not affirmed, the app MUST NOT compute or show any prediction; it
  shows a clear "not ready — do not predict" state instead.
- **R0-3:** Readiness is a per-consultation state (re-affirmed each session), not a permanent
  setting.
- **R0-4:** The **Sushumna** state (both nostrils flowing / no clear active nostril) is treated as
  "Swara not clearly identifiable" and therefore fails the gate by default (consistent with
  ADR-0002 DR-4; a taught Sushumna rule is pending, ADR-0010).
- **R0-5:** Readiness itself carries no prediction meaning; it is purely a gate.

## Consequences

- **Positive:** Prevents the tool from lending false confidence to an unreliable reading;
  encodes the tradition's own safeguard.
- **Negative:** One extra step per consultation — justified, and can be a fast single-tap
  affirmation once the practitioner is accustomed to it.

## Alternatives considered

- **Making readiness advisory (a reminder only)** — rejected: the teaching treats it as a hard
  precondition, so the app enforces it rather than suggesting it.
