# ADR-0002: Swara Domain Model & Terminology

- **Status:** Accepted (revised for Consolidated Master Notes v1)
- **Date:** 2026-08-14
- **Deciders:** POC owner (practitioner / product), engineering
- **Tags:** domain, glossary, model

## Context

The prediction logic rests on a small vocabulary that is easy to confuse. A precise, shared
glossary keeps UI copy, the rule engine, and tests aligned. Master Notes v1 adds nadi names,
breath polarity (Saguna/Nirguna), and generalizes the two observed "energies" beyond the
entry/seating pair. This ADR is the authoritative glossary and core model.

## Decision

### Glossary

| Term | Devanagari | Meaning |
|------|-----------|---------|
| **Bhara Swara** | भरा स्वर | The **active** nostril's side — breath currently flowing. Polarity **Positive**. |
| **Khali Swara** | खाली स्वर | The **inactive**/comparatively still side. Polarity **Negative**. |
| **Chandra / Ida** | चन्द्र / इड़ा | The **LEFT** nostril/nadi. When active: LEFT = Bhara. |
| **Surya / Pingala** | सूर्य / पिंगला | The **RIGHT** nostril/nadi. When active: RIGHT = Bhara. |
| **Sushumna** | सुषुम्ना | Both nostrils flowing / central channel. Consultation rule for this state is **pending** (ADR-0010) — do not predict by default. |
| **Active nostril** | — | The practitioner's currently flowing nostril (LEFT/RIGHT). Defines Bhara/Khali for that moment. |
| **First Energy** | प्रथम ऊर्जा | The **initial** observed energy (mode-dependent: e.g. entry, or energy when person sits). |
| **Second Energy** | द्वितीय ऊर्जा | The **later** observed energy (mode-dependent: e.g. seating, or energy at question time). |
| **Saguna** | सगुण | Practitioner **inhaling** at the exact question moment → Positive (ADR-0013). |
| **Nirguna** | निर्गुण | Practitioner **exhaling** at the exact question moment → Negative (ADR-0013). |
| **Practitioner / Sadhak** | साधक | The person performing the consultation. |
| **Visitor / Questioner** | — | The person with a question. |
| **Agni Tattva** | अग्नि तत्त्व | The fire element; in the remedies, linked to **Surya** Swara (ADR-0018). |
| **"रम रम" (beejakshara)** | रम रम | The Agni beejakshara chanted (aloud or mentally) with Surya Swara to activate Agni Tattva (ADR-0018). **Canonical spelling is "रम रम", not "राम राम"** — preserve exactly (ADR-0017/0018 RM-0). |
| **Tithi** | तिथि | The lunar day; each Tithi has an *expected Swara* (ADR-0020). |
| **Paksha** | पक्ष | The lunar fortnight — Shukla (bright) / Krishna (dark); part of a Tithi's name. |
| **Sunrise** | सूर्योदय | The main daily checkpoint: the expected Tithi Swara should be active at sunrise (ADR-0020). |

### Thermal polarity of the nadis (remedies)

For the therapeutic practices (ADR-0018), the two nadis carry a thermal quality:

```text
CHANDRA (LEFT)  → COOLING / CALMING
SURYA  (RIGHT)  → HEATING / ACTIVATING (Agni)
```

This is distinct from the Bhara/Khali *polarity* used for prediction: a nadi's thermal quality is
fixed to the nadi (Chandra cools, Surya heats), whereas Bhara/Khali depends on which nostril is
currently active.

### Core model (invariant relationships)

1. **Active nostril → Bhara/Khali sides:**
   ```
   LEFT active  (Chandra/Ida)     → LEFT  = BHARA, RIGHT = KHALI
   RIGHT active (Surya/Pingala)   → RIGHT = BHARA, LEFT  = KHALI
   ```

2. **Golden principle — polarity is never fixed to physical side:**
   ```
   LEFT  ≠ always Bhara
   RIGHT ≠ always Khali
   ```
   Physical side must be translated to Bhara/Khali via the **current** active nostril before any
   rule is applied. Because the practitioner's Swara can change between observations, the *same*
   physical position can be Bhara at one moment and Khali at another (see Sunita, ADR-0004/0012).

3. **Polarity mapping (universal):**
   ```
   BHARA = Positive
   KHALI = Negative
   ```

4. **Two energies, two time stages (generalized):**
   ```
   FIRST ENERGY  = Initial stage
   SECOND ENERGY = Later stage
   ```
   What sources First/Second energy depends on the consultation mode (ADR-0012).

5. **Breath polarity (independent signal):**
   ```
   INHALE → SAGUNA → Positive
   EXHALE → NIRGUNA → Negative
   ```

### Requirements derived from the model

- **DR-1:** All prediction logic operates on the `Bhara | Khali` (and `Saguna | Nirguna`) domains,
  computed from raw inputs — never keyed directly on Left/Right.
- **DR-2:** UI copy pairs each Devanagari term with a plain gloss (e.g. "भरा (Positive)",
  "Chandra = LEFT").
- **DR-3:** The active-nostril → polarity conversion is a **single, testable function**, evaluated
  with the active nostril *in effect at that observation's moment*.
- **DR-4:** Sushumna (both/uncertain) is a recognized state that **blocks** default prediction
  until a taught rule exists.

## Consequences

- Separating *physical side* (observed) from *polarity* (derived, time-dependent) prevents the
  most likely class of error and directly supports the raw/interpretation split (ADR-0015).
- Adding nadi and breath vocabulary now keeps later signal ADRs consistent with this glossary.

## Alternatives considered

- **Fixing polarity to Left/Right** — rejected by the golden principle; the Sunita case proves
  polarity is time-dependent.
