# ADR-0004: Four-Rule Energy Engine (First → Second)

- **Status:** Accepted (revised for Consolidated Master Notes v1)
- **Date:** 2026-08-14
- **Deciders:** POC owner (practitioner / product), engineering
- **Tags:** domain, logic, algorithm, testing

## Context

This ADR specifies the **four-rule energy engine** — one of several prediction signals
(ADR-0013), and the one used by the transition-based modes (Independent Room, Shared/Chamber).
It maps a **First Energy → Second Energy** transition to one of four predictions. What sources
First/Second energy is defined per mode in ADR-0012; this ADR defines the transition logic and
its acceptance cases.

## Decision

### Inputs (abstract)

```text
firstEnergy  : BHARA | KHALI     // initial stage energy
secondEnergy : BHARA | KHALI     // later stage energy
```

Each energy is itself derived elsewhere from `(activeNostrilAtThatMoment, observedSide)`:

```text
bharaSide = activeNostril                       // LEFT→LEFT(Chandra), RIGHT→RIGHT(Surya)
energy    = (observedSide == bharaSide) ? BHARA : KHALI
```

The active nostril is read **at each observation's own moment** — it may differ between the two
(see Sunita, below).

### Rule selection

`(firstEnergy → secondEnergy)` selects exactly one rule:

| Rule | First | Second | Initial | Later | Verdict / Meaning |
|------|-------|--------|---------|-------|-------------------|
| **#1** | BHARA | BHARA | Positive | Positive | **YES** |
| **#2** | KHALI | KHALI | Negative | Negative | **NO — Dead Energy** |
| **#3** | BHARA | KHALI | Positive | Negative | **Good start → challenges later** |
| **#4** | KHALI | BHARA | Negative | Positive | **Challenges first → success later** |

### Master matrix

```text
                     SECOND ENERGY
                 BHARA             KHALI
             ┌────────────────┬────────────────┐
   FIRST     │ RULE #1  YES   │ RULE #3 GOOD→PB │
   BHARA     │  ✅ → ✅       │  ✅ → ❌        │
             ├────────────────┼────────────────┤
   FIRST     │ RULE #4 PB→GD  │ RULE #2  NO     │
   KHALI     │  ❌ → ✅       │  ❌ → ❌ (Dead) │
             └────────────────┴────────────────┘
```

### Prediction texts (authoritative copy)

- **Rule #1 — YES:** शुरुआत positive और परिणाम भी positive।
- **Rule #2 — NO / Dead Energy:** शुरुआत और परिणाम दोनों negative।
- **Rule #3:** शुरुआत अच्छी, बाद में challenges/problems।
- **Rule #4:** शुरुआत में challenges, फिर solution और success।

### Memory formula (surface in UI)

> **FIRST STATE = INITIAL ENERGY, SECOND STATE = LATER ENERGY; भरा = Positive, खाली = Negative।**

### Engine requirements

- **RE-1:** Pure, deterministic function of `(firstEnergy, secondEnergy)`; no side effects, no
  randomness.
- **RE-2:** Total and mutually exclusive over the four combinations.
- **RE-3:** If either energy is missing, return an explicit **incomplete** state — never a guess.
- **RE-4:** Energy derivation (side→polarity) happens **before** this engine, using the active
  nostril in effect at each moment (per DR-3).
- **RE-5:** This engine is **one signal** among several; it does not aggregate other signals
  (that is ADR-0014's concern).

### Acceptance test cases — Independent Room (First=Entry, Second=Seating)

| # | Name | active (moment) | entrySide | seatSide | firstEnergy | secondEnergy | Rule | Verdict |
|---|------|-----------------|-----------|----------|-------------|--------------|------|---------|
| 1 | Pallavi | LEFT (Chandra) | RIGHT | RIGHT | KHALI | KHALI | #2 | NO |
| 2 | Manish | LEFT (Chandra) | RIGHT | LEFT | KHALI | BHARA | #4 | Problems→success |
| 3 | Mamta | RIGHT (Surya) | RIGHT | RIGHT | BHARA | BHARA | #1 | YES |
| 4 | Aman | RIGHT (Surya) | RIGHT | LEFT | BHARA | KHALI | #3 | Good→challenges |

### Acceptance test case — Swara change (Sunita, Shared/Chamber mode)

Demonstrates that the two energies use the active nostril **at their own moments**, and position
alone is not the signal:

```text
Sit-time:      practitioner RIGHT/Surya active → RIGHT = BHARA; Sunita sits RIGHT → firstEnergy  = BHARA
Question-time: practitioner LEFT/Chandra active → RIGHT = KHALI; Sunita still RIGHT → secondEnergy = KHALI
Transition:    BHARA → KHALI  ⇒  Rule #3 (good start → later challenges)
```

Key insight to encode: **person did not move; the practitioner's Swara changed**, flipping the
energy relationship. Therefore energy MUST be recomputed at each observation moment, not cached
from the first.

### Derived totality cases (must also be tested)

At least: LEFT-active entry/seat LEFT (Rule #1) and RIGHT-active entry/seat LEFT (Rule #2), to
prove Left/Right is never treated as fixed polarity.

## Consequences

- The engine is trivially unit-testable; correctness is objective.
- Generalizing to First/Second energy lets the same engine serve multiple modes (ADR-0012) while
  the mode decides what to observe.

## Alternatives considered

- **Baking entry/seating into the engine** — rejected: it couples the engine to one mode and
  cannot express the Sunita swara-change case.
