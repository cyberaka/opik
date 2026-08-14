# ADR-0016: Meethi Goli — Symbolic Action (Non-Causal)

- **Status:** Accepted
- **Date:** 2026-08-14
- **Deciders:** POC owner (practitioner / product), engineering
- **Tags:** domain, output, integrity

## Context

Sometimes the Swara reading already indicates a favourable outcome, but the visitor may not
believe the prediction. The practitioner may give a simple **symbolic action** — a *Meethi Goli*
("sweet pill") — such as "आज लाल रंग का लड्डू खा लेना" or "नींबू-मिर्च लटका लेना". The purpose is to
give the person a tangible action; it is **not** the cause of the outcome.

## Decision

- **MG-1 — Representation.** Meethi Goli is modelled as an **optional symbolic action attached to a
  prediction**, distinct from the prediction itself.
- **MG-2 — Non-causal (critical).** The app MUST NOT represent the symbolic action as *causing* the
  outcome. The following framings are **prohibited**:
  ```text
  ❌ Red Laddu   → Success
  ❌ Nimbu-Mirchi → Success
  ```
  Correct framing:
  ```text
  Swara → Positive Prediction
  Optional: Symbolic Action / Meethi Goli   (comfort/tangibility, not cause)
  ```
- **MG-3 — Optional & separable.** It is never required, never affects any signal or verdict, and
  is clearly labelled as a symbolic/optional suggestion.
- **MG-4 — Selection rules are pending.** Whether specific color/object/timing choices relate to
  Swara is **not yet taught** (ADR-0014, ADR-0010). Until then, the app treats Meethi Goli as free
  text / a simple suggestion and MUST NOT encode a color/object→outcome mapping.

## Consequences

- **Positive:** Preserves the practice while protecting the app's integrity — no fake causal claims.
- **Negative:** Meethi Goli remains unstructured for now (free text), pending a taught rule — an
  acceptable, honest placeholder.

## Alternatives considered

- **A catalogue of symbolic actions mapped to outcomes** — rejected: implies causation and invents
  a selection rule the Guru has not taught.
