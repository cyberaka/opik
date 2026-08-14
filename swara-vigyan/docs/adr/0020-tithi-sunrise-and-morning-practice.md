# ADR-0020: Tithi, Sunrise & Morning Wake-Up Practice

- **Status:** Accepted
- **Date:** 2026-08-14
- **Deciders:** POC owner (practitioner / product), engineering
- **Tags:** domain, daily-practice, tithi, module

## Context

Master Notes v2 adds a **daily-alignment** capability: each day's **Tithi** implies an *expected
Swara*, and the practitioner aligns their morning with it. The primary checkpoint is **sunrise**.
This ADR captures that teaching and the "TODAY" module, while being explicit that the full
Tithi→Swara mapping is **not yet taught** (only one example is known) and must not be invented.

## Decision

### Core teaching (GURU TEACHING)

- **TS-1:** A day's **Tithi** has an **expected Swara**. The **sunrise** is the main reference: at
  sunrise, the expected Tithi Swara should be active.
  ```text
  TODAY'S TITHI → EXPECTED SWARA → (checkpoint) SUNRISE → expected Swara should be active
  ```
- **TS-2 (known example):** *Krishna Paksha Navami → expected Surya* (so Surya should be active at
  sunrise). This is the **only** Tithi→Swara mapping taught so far.

### Wake-up rules (GURU TEACHING)

- **TS-3 — Sunrise is the main alignment.** Waking earlier does not by itself set the alignment;
  e.g. Chandra at 04:00 does not determine the sunrise alignment if Surya is correctly active at
  sunrise.
- **TS-4 — Prefer waking in the correct Tithi Swara**, even when starting before sunrise. If today
  is a Surya day and you wake at 05:00, waking in Surya is preferable.
- **TS-5 — 50% + 50% model.** Early wake-up in the correct Swara balances the first ~50% of the
  day's energy; correct Swara at sunrise balances the next ~50%. Both correct → day energy balanced.
  Early wrong Swara → first 50% negative; correct at sunrise → next 50% positive.
- **TS-6 — Temporary wake-up doesn't count.** Waking briefly (e.g. for the washroom) and going back
  to sleep is **not** the main daily wake-up.
- **TS-7 — Final wake-up is the one that counts.** When you finally get out of bed to start the day,
  begin in the correct Tithi Swara.

### Pending (NEEDS CLARIFICATION — do not invent)

- **TS-P1:** The complete **Tithi → Chandra/Surya mapping for all Tithis** (only Krishna Paksha
  Navami is known).
- **TS-P2:** Which foot to place down first when leaving the bed.
- **TS-P3:** How to place the foot.
- **TS-P4:** The morning **intention / मनोवांछित** technique.

(These are also listed in ADR-0010 §Pending.)

### "TODAY" module requirements

- **TD-1:** A **TODAY** module surfaces: Tithi (paksha + name), sunrise time, expected Swara (only
  when known — see TD-3), and wake-up guidance (TS-3…TS-7).
- **TD-2:** The app helps the practitioner **compare** their observed sunrise Swara against the
  expected one and reflect the 50/50 alignment — it reports alignment, it does not judge the person.
- **TD-3 — No invented mappings.** The app MUST NOT compute an expected Swara for an arbitrary Tithi
  until the full mapping is taught. For unknown Tithis it shows `NEEDS CLARIFICATION` (ADR-0017), and
  it may still let the practitioner **manually record** the expected Swara they were taught for a
  given day.
- **TD-4:** Tithi/sunrise values used for alignment are inputs/observations (ADR-0015); any
  astronomical calculation added later is a `RESEARCH NOTE` convenience, clearly separated from the
  Guru's Tithi→Swara rule.

## Consequences

- **Positive:** Captures the daily-practice dimension and its "TODAY" module without fabricating the
  unknown Tithi mapping or the pending morning micro-rules.
- **Negative:** The module is partly a manual recorder until the full mapping is taught — the honest
  and correct state given the teaching.

## Alternatives considered

- **Auto-deriving expected Swara from any Tithi now** — rejected: only one mapping is known;
  computing the rest would violate the "never invent" principle (ADR-0017/0014).
