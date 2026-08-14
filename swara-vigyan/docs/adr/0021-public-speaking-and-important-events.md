# ADR-0021: Important Events — Public Speaking / Mass Gathering

- **Status:** Accepted
- **Date:** 2026-08-14
- **Deciders:** POC owner (practitioner / product), engineering
- **Tags:** domain, action-timing, events, module

## Context

Master Notes v2 adds a **proactive** use of Swara: choosing the Swara in which to *perform* an
action so it goes well — specifically for public speaking / mass gatherings (stage, lecture,
presentation, community address). This differs fundamentally from prediction: here the practitioner
**intentionally acts in a chosen Swara**, which is allowed and desired — unlike prediction, where
manufacturing the breath is forbidden (ADR-0013). This ADR captures the teaching and the module.

## Decision

### Action-vs-observation distinction (important)

- **EV-0:** For **prediction**, energy must be observed spontaneously and never manufactured
  (ADR-0013 SIG-C2, ADR-0020 philosophy). For **action practices** (public speaking, remedies),
  the practitioner **deliberately performs** the action in a specific Swara. The app must keep these
  two intents clearly separate so the spontaneity rule for prediction is not confused with the
  intentional-Swara rule for action.

### Public-speaking practice (GURU TEACHING) — three phases

```text
STAGE ENTRY → AUDIENCE CONNECTION → PRESENTATION
```

- **EV-1 — Stage entry:** Prefer entering the stage in **Chandra** Swara, so the stage connects with
  you.
  > चंद्र स्वर में stage पर जाओ ताकि stage आपके साथ जुड़ जाए।
- **EV-2 — Fallback:** If Chandra is not available, enter with **Surya + Saguna (inhale) + Bhara**.
  ```text
  Entry preference: 1) CHANDRA   or   2) SURYA + SAGUNA(inhale) + BHARA
  ```
- **EV-3 — Audience greeting:** On stage, **inhale in Surya** and greet the whole gathering
  ("Namaste") to connect with the audience.
- **EV-4 — Presentation:** Deliver the lecture/presentation in **Surya** Swara.
- **EV-5 — Memory formula:**
  > **चंद्र से Stage जोड़ो → सूर्य से Audience जोड़ो → सूर्य में Presentation दो।**

### Module requirements

- **EV-6:** An **IMPORTANT EVENTS → Public Speaking** module presents the three-phase guidance with
  the Swara for each phase and the fallback, all as `GURU TEACHING` (ADR-0017).
- **EV-7:** The module frames these as **preparation guidance** (act in the taught Swara), not a
  prediction; it does not output YES/NO.
- **EV-8:** As with all content, unstated variations are not invented; only the taught phases are
  encoded.

## Consequences

- **Positive:** Captures the proactive/auspicious-timing dimension of the practice and cleanly
  separates "act in a Swara" from "observe a Swara", preventing a category error with the prediction
  spontaneity rule.
- **Negative:** Adds a distinct interaction pattern (guidance vs prediction) the UX must signal
  clearly (ADR-0006).

## Alternatives considered

- **Treating public speaking as another prediction mode** — rejected: it is an action-timing
  practice, not an observation/prediction; conflating them would misapply the spontaneity rule.
