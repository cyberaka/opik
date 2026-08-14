# ADR-0006: User Experience & Consultation Flow

- **Status:** Accepted (revised for Consolidated Master Notes v1)
- **Date:** 2026-08-14
- **Deciders:** POC owner (practitioner / product), engineering
- **Tags:** ux, ui, requirements

## Context

The tool is used during or right after a live consultation, so the flow must be fast,
unambiguous, and hard to misread. With multiple modes and signals now in scope (ADR-0012/0013),
the UX must guide the practitioner through *readiness → mode → observation → reading* while never
inventing an answer. This ADR defines the flow and UI requirements.

## Decision

### Overall flow

```text
[Rule 0 gate] → [choose mode] → [capture mode observations] → [additional signals]
     ↓                                                              ↓
 not ready → stop                                       [per-signal readings + conflicts]
```

### 1. Rule 0 — Readiness gate (ADR-0011)

- **UX-1:** A short, tappable readiness checklist opens each consultation. Until it is affirmed,
  the app shows a clear "not ready — do not predict" state and **no** prediction UI is reachable.
- **UX-2:** Sushumna / "Swara unclear" is selectable and fails the gate by default.

### 2. Mode selection (ADR-0012)

- **UX-3:** After readiness, the practitioner picks a mode: Independent Room, Shared/Chamber,
  Sabha, Remote/Position-Unknown, Behind. Each mode states **which moments to observe** before
  capture begins.
- **UX-4 (phasing):** Phase 1 ships **Independent Room** fully; other modes may appear as clearly
  marked "coming/limited" until Phase 2 (ADR-0001).

### 3. Observation capture (per mode)

- **UX-5 — Active nostril:** choose LEFT/RIGHT, labelled with nadi (Chandra/Surya) and derived
  Bhara/Khali. Where a mode has two moments (A, B), the app captures the active nostril **at each
  moment** (so a Swara change is recorded — Sunita, ADR-0004).
- **UX-6 — Sides/positions:** capture entry/seating (Mode A), sit/question energy (Mode B),
  questioner side (Sabha), or "behind" — each annotated live with its Bhara/Khali polarity.
- **UX-7 — Time-stage framing:** the two observations are always labelled *Initial* and *Later*.

### 4. Additional signals (ADR-0013)

- **UX-8 — Breath (Saguna/Nirguna):** capture inhale/exhale at the question moment **plus a
  `spontaneous?` toggle**; if not spontaneous, the signal is shown as **not usable**, not as a
  polarity.
- **UX-9 — Addressing:** capture whether the practitioner was addressed **before** or **after** the
  question (Positive/Negative signal).
- **UX-10:** Only the signals relevant to the chosen mode/context are requested; unavailable
  signals are simply omitted.

### 5. Result & signal display

- **UX-11:** Results appear only when required inputs exist; never a guessed result (RE-3).
- **UX-12 — Per-signal readings:** each applicable signal is shown **independently** with its
  reading (Positive / Negative / Rule #n / Pending / N-A) and a one-line "why".
- **UX-13 — Conflicts & pending (ADR-0014):** when signals disagree, the UI shows the conflict and
  states the resolution is **pending** — it does **not** pick a winner. Untaught cases
  (Behind+Chandra, Sushumna) render a "rule not yet known" note.
- **UX-14 — Agreement:** if all applicable signals agree, the UI may say "all available signals
  indicate …" (reported as agreement, not a merged verdict).
- **UX-15 — Verdicts are colour + text coded** (never colour alone; ADR-0007).

### 6. Reference, examples & Meethi Goli

- **UX-16:** Reference material — four rules, master matrix, canonical cheat sheet, golden
  principles, memory formulas.
- **UX-17 — Examples:** the Guru's examples (Pallavi, Manish, Mamta, Aman, **Sunita** swara-change)
  are loadable and populate the flow to reproduce the taught result.
- **UX-18 — Meethi Goli (ADR-0016):** an optional, clearly-symbolic suggestion attached to a
  prediction, never presented as the cause of the outcome.

### Remedies module (separate flow)

- **UX-23:** The app has a top-level choice between **Consultation** and **Remedies** (ADR-0018).
  The Remedies flow is Swara-first (read active Swara → pick condition → follow taught steps + taught
  duration), detailed in ADR-0018; its health-safety framing is ADR-0019.
- **UX-24 — Provenance rendering (ADR-0017):** across both flows, content is visibly tagged by
  provenance — **Guru Teaching** vs a set-apart **Research/Safety Note** vs a **Needs Clarification**
  flag. A safety note must never look like teaching, and vice versa.

### Cross-cutting

- **UX-19 — Theme** toggle (may persist locally, ADR-0008). **UX-20 — Responsive** (phone-first,
  single column). **UX-21 — Reset** clears the whole consultation. **UX-22 — No dead ends:** the
  next expected action and any incomplete/blocked state are always explicit.

## Consequences

- The readiness-first, per-signal, conflict-honest flow keeps the mental model (moment → energy →
  signal) visible and prevents false certainty.
- Phasing lets Phase 1 ship a complete Independent-Room experience while the UX for other modes is
  staged in.

## Alternatives considered

- **A single merged "answer" screen** — rejected: it would hide conflicts and imply an aggregation
  rule that is not yet taught (ADR-0014).
