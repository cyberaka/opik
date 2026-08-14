# ADR-0018: Remedies / Therapeutic Practices Module

- **Status:** Accepted
- **Date:** 2026-08-14
- **Deciders:** POC owner (practitioner / product), engineering
- **Tags:** domain, remedies, module, content

## Context

Beyond consultation/prediction, the Guru's teaching includes **Swara-based remedies** — breath and
Swara techniques for specific conditions. This makes the product a two-capability practice assistant.
Remedy content touches health, so it is governed by the provenance convention (ADR-0017) and the
health-safety requirements (ADR-0019). This ADR captures the remedy module scope and the canonical
catalogue **as taught** (`GURU TEACHING`).

> **Master principle (GURU TEACHING):** पहले Swara observe करो, फिर remedy apply करो।

## Decision

### Module scope

- **RM-1:** A **Remedies** module lets the practitioner: read the current active Swara, browse
  remedies by condition, follow the step-by-step technique (with the taught duration), and optionally
  keep a personal practice record (ADR-0008/§practice-record).
- **RM-2:** Every remedy is **Swara-first**: the technique depends on observing the current active
  Swara (Chandra/Surya) before acting.
- **RM-3:** All catalogue text is `GURU TEACHING` provenance (ADR-0017). Any safety/medical
  commentary is a separate `RESEARCH / SAFETY NOTE` (ADR-0019) and is never merged into the steps.

### Thermal principle (GURU TEACHING)

```text
CHANDRA (LEFT)  → COOLING / CALMING      → High BP, High Fever
SURYA  (RIGHT)  → HEATING / ACTIVATING   → Low BP, Excessive cold, Body pain
```

### Canonical remedy catalogue (GURU TEACHING — strength/duration preserved)

| # | Condition | Technique | Duration | Taught result |
|---|-----------|-----------|---------:|---------------|
| R1 | Headache / Anxiety / Migraine | Observe active Swara; **close the active nostril**, inhale+exhale from the **opposite** nostril | ~5 min | subsides in the **6th minute** |
| R2 | High BP | Close **RIGHT**, breathe from **LEFT / Chandra** | 5–10 min | BP control/balance begins |
| R3 | Low BP | Close **LEFT**, breathe from **RIGHT / Surya** | (see Pending) | BP balance begins |
| R4 | High Fever | In **Chandra Swara**, blow toward a glass of water (hygienic gap), patient drinks | — | fever begins to come down |
| R5 | Very cold / chills | In **Surya Swara**, blow toward water (hygienic gap), person drinks | — | warmth felt in body |
| R6 | Body pain (frozen shoulder, knee, joint, back, muscle, abdominal, localized) | **Surya + Agni Tattva + RAM beejakshara + palm-rubbing** → apply warm palms to the area | ~15 min/day | relief |

### Technique details

**R1 — Headache / Anxiety / Migraine (opposite-Swara breathing)**
```text
Chandra/LEFT active  → close LEFT  → breathe RIGHT → 5 min → 6th minute subsides
Surya/RIGHT active   → close RIGHT → breathe LEFT  → 5 min → 6th minute subsides
```
Formula: *जो स्वर चल रहा है उसे बंद करो → opposite nostril से 5 minutes breathe करो।*

**R2/R3 — Blood pressure**
```text
HIGH BP → close RIGHT → LEFT/Chandra (cooling)  → 5–10 min → control
LOW  BP → close LEFT  → RIGHT/Surya (activating) → BP balance
```
Formula: *High BP → Chandra; Low BP → Surya.*

**R4/R5 — Water remedies (thermal)**
```text
FEVER: Chandra Swara → glass of water, keep hygienic distance so no germ enters water
       → blow toward water in Chandra → patient drinks → fever subsides
COLD : Surya Swara → water (hygienic distance) → blow in Surya → drink → warmth
```
Note (GURU TEACHING): maintain enough gap between nose/mouth and the glass that no germ enters the
water.

**R6 — Pain relief (Surya + Agni Tattva + RAM + palm rubbing)**
```text
Surya Swara → inhale → mentally chant "RAM RAM RAM..." (vocal not required)
   ↓ Surya is linked to the body's AGNI TATTVA; RAM is the Agni beejakshara that activates it
Rub both palms together while chanting → heat/Agni felt in palms
   ↓
Place warm palms on the painful area (use like sikai / warm compress)
   ↓
When palms cool: Surya inhale + RAM + rub again → reheat → reapply
   ↓
Repeat as needed, ~15 minutes daily
```

### Underlying principles (GURU TEACHING)

- **A — Opposite Swara:** for some conditions, close the current active Swara and activate the
  opposite (R1).
- **B — Chandra = Cooling/Calming:** applied to High BP, High Fever.
- **C — Surya = Heating/Activating (Agni):** applied to Low BP, cold, pain.
- **D — RAM = Agni beejakshara:** Surya + RAM activates Agni Tattva; used in palm-rubbing pain relief.

### Personal practice record (per ADR-0008/0015 storage rules)

Optional, opt-in, local-only tracking to observe effectiveness over time:

```yaml
date:
time:
problem:
before:   { active_swara: , intensity_0_to_10: }
practice: { technique: , duration: }
after:    { active_swara: , intensity_0_to_10: }
after_10_minutes: { intensity_0_to_10: }
notes:
```

- **RM-4:** The practice record is `RESEARCH / personal-tracking` data, not `GURU TEACHING`; it is
  subject to the same privacy rules as the consultation log (opt-in, local-only — ADR-0008).

### Requirements summary

- **RM-5:** Catalogue rules are rendered exactly as taught (durations, "6th minute", "5–10 min",
  "~15 min/day"); the app does not round, "improve", or add efficacy claims (ADR-0017 PV-1).
- **RM-6:** Unconfirmed details are marked (see ADR-0010 §Pending / ADR-0017 `NEEDS CLARIFICATION`) —
  e.g. Low-BP exact duration.
- **RM-7:** Every remedy screen surfaces the health disclaimer/safety note from ADR-0019, visually
  separated from the teaching.
- **RM-8 (optional):** The app MAY offer a simple timer for the taught durations, clearly a
  convenience, not a claim.

## Consequences

- **Positive:** A faithful, Swara-first remedies reference that stays pristine under ADR-0017 and safe
  under ADR-0019.
- **Negative:** Health-adjacent content raises the safety bar — addressed by ADR-0019 and the
  provenance separation.

## Alternatives considered

- **Folding remedies into the consultation flow** — rejected: different purpose (therapeutic vs
  predictive), different safety profile; a distinct module is clearer and safer.
