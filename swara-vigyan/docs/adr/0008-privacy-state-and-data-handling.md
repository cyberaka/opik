# ADR-0008: Privacy, State & Data Handling

- **Status:** Accepted (revised for Consolidated Master Notes v1)
- **Date:** 2026-08-14
- **Deciders:** POC owner (practitioner / product), engineering
- **Tags:** privacy, state, data

## Context

Consultations concern people's personal questions. The architecture (ADR-0005) is client-only,
which makes a privacy-first posture natural. Master Notes v1 adds a new requirement in tension with
the original "no history" stance: **raw observations should be storable so future rule changes can
reprocess them** (ADR-0015). This ADR reconciles reprocessability with privacy.

## Decision

### Data handling

- **PR-1: No transmission.** No input, observation, or result is ever sent off-device. No backend,
  analytics, telemetry, tracking, or third-party call (reinforces ADR-0005 TS-2).
- **PR-2: No server-side storage / accounts.** Everything stays on the practitioner's device.
- **PR-3: Minimize identifying data.** Core observations are abstract (nostril, sides, breath
  phase, addressing order, mode). The optionally-captured `question.raw_text` (ADR-0015) can be
  identifying and is therefore **off by default** and clearly optional.

### Client state

- **ST-1: Ephemeral session state.** The in-progress consultation lives in memory and clears on
  reset or reload. Derived verdicts are recomputed, never treated as stored truth (ADR-0015 DA-7).
- **ST-2: Non-sensitive UI prefs.** Theme and similar preferences may persist locally.

### Raw-observation log (reconciles reprocessing with privacy)

- **ST-3: Opt-in, local-only history.** A consultation **raw-observation log** (ADR-0015 schema)
  MAY be stored, but only:
  - **opt-in** — off by default; the practitioner explicitly enables saving;
  - **local-only** — device storage (e.g. `localStorage`/on-device), never synced or transmitted;
  - **raw facts + `ruleset_version`** — no persisted verdicts;
  - **`question.raw_text` excluded by default** — included only if the practitioner opts in per
    entry.
- **ST-4: User control.** The practitioner can **view, export (local file), and delete** the log,
  including a one-tap "clear all". Deletion is immediate and complete.
- **ST-5: Purpose limitation.** The log exists solely to enable reprocessing under updated rules
  (ADR-0015); it is not used for any other purpose.
- **ST-6: Remedy practice record.** The optional **personal practice record** (ADR-0018 RM-4) follows
  the identical rules: opt-in, local-only, user-controlled (view/export/delete), never transmitted.
  Its subjective intensity notes are personal-tracking data, not medical monitoring (ADR-0019 SF-10).

## Consequences

- **Positive:** Enables the reprocessing principle without weakening privacy — nothing leaves the
  device, history is opt-in, and the most sensitive field is excluded by default.
- **Negative:** No cross-device continuity (acceptable; a synced/multi-device design would need its
  own privacy ADR).

## Alternatives considered

- **No history at all (original stance)** — rejected: it conflicts with the taught reprocessing
  requirement (ADR-0015).
- **Always-on history including question text** — rejected: unnecessary identifiability; opt-in and
  default-excluded raw text is the safer default.
