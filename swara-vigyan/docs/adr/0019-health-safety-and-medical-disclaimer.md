# ADR-0019: Health Safety & Medical Disclaimer

- **Status:** Accepted
- **Date:** 2026-08-14
- **Deciders:** POC owner (practitioner / product), engineering
- **Tags:** safety, health, disclaimer, compliance

> **Provenance (ADR-0017): this ADR is a `RESEARCH / SAFETY NOTE`, not `GURU TEACHING`.**
> It records the app's safety requirements and engineering/health commentary. It must never be
> presented to users as part of the Guru's teaching, and it does not modify the remedy content in
> ADR-0018 — it wraps that content with disclaimers and guardrails.

## Context

The Remedies module (ADR-0018) addresses conditions that can be serious — high fever, high/low blood
pressure, migraine, body pain. The remedies are traditional Swara-Vigyan practices captured for
personal study. To publish them responsibly, the app needs clear safety framing so users do not
mistake a spiritual-practice aid for medical treatment or delay real care.

## Decision

### Framing

- **SF-1 — Not medical advice.** The app MUST state plainly that remedy content is **traditional
  spiritual/self-practice**, provided for study, and is **not** medical advice, diagnosis, or
  treatment, and **not** a substitute for professional healthcare.
- **SF-2 — Do not delay or replace care.** For any concerning, severe, persistent, or worsening
  condition, the app MUST advise consulting a qualified medical professional and MUST NOT suggest
  using a remedy *instead of* medical care.
- **SF-3 — Do not alter prescribed treatment.** The app MUST advise users not to stop or change
  prescribed medication (e.g. BP medication) based on the app.
- **SF-4 — No diagnosis / no efficacy claims by the app.** The app itself makes no medical claims;
  taught results (e.g. "subsides in the 6th minute") and strong reliability statements (e.g.
  *"Swara Vigyan fail नहीं होता"*, ADR-0017 PV-7) are shown strictly as `GURU TEACHING` quotations,
  attributed and visually separated from app text — never as the app's own promise or guarantee.

### Placement & visibility

- **SF-5 — Persistent disclaimer.** A concise disclaimer is shown on entry to the Remedies module and
  is accessible from every remedy screen (ADR-0018 RM-7).
- **SF-6 — Visual separation (ADR-0017 PV-2).** Safety notes render distinctly from the teaching
  steps so a user never confuses commentary with the Guru's words.

### Condition-specific safety notes (`RESEARCH / SAFETY NOTE`)

- **SF-7 — Acute/emergency signs.** For symptoms that may signal an emergency (e.g. very high fever,
  severe/unusual headache, fainting, chest pain, breathing difficulty, very high or very low BP with
  symptoms), the app advises seeking urgent medical help immediately.
- **SF-8 — Breathing technique caution.** Breath practices should be gentle and never strained; stop
  if dizzy, breathless, or unwell. Users with cardiovascular or respiratory conditions, and during
  pregnancy, should consult a professional before breath-holding/forceful practices.
- **SF-9 — Water-remedy hygiene.** The teaching already prescribes keeping a hygienic gap so no germ
  enters the water (ADR-0018 R4/R5); the app reinforces general food/water hygiene as a safety note.
- **SF-10 — Personal-practice tracking is not medical monitoring.** The optional practice record
  (ADR-0018 RM-4) is for personal observation only; intensity numbers are subjective and not a
  clinical measurement.
- **SF-12 — New remedies (v2).** Persistent or severe **constipation** (or with pain/bleeding) should
  be seen by a professional, not self-managed indefinitely. The **charged-wool** practice is
  low-risk, but users should avoid overheating and watch for skin irritation; it is comfort practice,
  not treatment.

### Boundaries

- **SF-11:** The app does not target treatment of others as patients, does not provide dosing or
  clinical instructions beyond quoting the taught technique, and does not claim to cure any disease.

## Consequences

- **Positive:** The remedies can be shared responsibly; users are steered to real care when it
  matters, and the teaching stays intact and clearly attributed.
- **Negative:** More disclaimer surface in the UI — necessary and appropriate for health-adjacent
  content.

## Alternatives considered

- **Publishing remedies without safety framing** — rejected: irresponsible for health-related content
  and would risk users substituting the app for medical care.
- **Editing the teaching to soften claims** — rejected: violates ADR-0017 (do not alter teaching);
  the correct tool is separated disclaimers, not rewritten teaching.
