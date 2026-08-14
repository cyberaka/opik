# ADR-0007: Content, Internationalization & Accessibility

- **Status:** Accepted
- **Date:** 2026-08-14
- **Deciders:** POC owner (practitioner / product), engineering
- **Tags:** content, i18n, accessibility

## Context

The source teaching is bilingual — Hindi (Devanagari) with embedded English technical
terms — and the practitioner thinks in that mixed register. Content fidelity matters for a
tradition-based tool, and the app should be usable by people with varied abilities and
devices. This ADR sets content, language, and accessibility requirements.

## Decision

### Language & content

- **CT-1:** The primary content register is **Hindi + English mixed**, matching the source
  (e.g. "भरा (Positive)", "Chandra = LEFT / Surya = RIGHT", "Saguna = inhale = Positive",
  "Entry = Initial"). Devanagari and traditional terms (Bhara/Khali, Chandra/Ida, Surya/Pingala,
  Sushumna, Saguna/Nirguna, Sadhak, Meethi Goli) are always paired with a plain gloss so meaning
  is unambiguous (per DR-2).
- **CT-2:** Canonical strings — the four prediction texts and the memory formula — MUST match
  ADR-0004 verbatim.
- **CT-3:** All user-facing strings are kept in one place (a strings/content module), so the
  wording can be reviewed and, in future, fully localized (see ADR-0010) without touching
  logic. Full multi-locale switching is **out of scope** for the POC, but the structure must
  not preclude it.
- **CT-4:** The document language and encoding are set correctly (`<html lang>`, UTF-8) so
  Devanagari renders reliably; a system Devanagari-capable font stack is used (no CDN font
  dependency, per ADR-0005 TS-2).

### Accessibility (POC baseline)

- **AX-1 — Not colour-alone:** every verdict/polarity is conveyed by text/label in addition
  to colour (supports colour-blind users; ties to UX-10).
- **AX-2 — Keyboard:** all interactive controls (nostril/entry/seat choices, reset, theme,
  example cards) are reachable and operable by keyboard, with visible focus styling.
- **AX-3 — Semantics:** choice groups use appropriate roles/labels (e.g. radio-group
  semantics for the mutually-exclusive selectors); the live result region is announced to
  assistive tech when it updates.
- **AX-4 — Contrast:** text and essential UI meet WCAG AA contrast in both light and dark
  themes.
- **AX-5 — Targets & zoom:** tap targets are comfortably sized for one-handed phone use and
  the layout tolerates browser zoom / larger text without breaking.

## Consequences

- Centralized strings + paired glosses keep the tradition's language intact while remaining
  clear and future-localizable.
- The accessibility baseline is modest but concrete and testable, appropriate for a POC.

## Alternatives considered

- **English-only UI** — rejected: loses fidelity to the teaching and the practitioner's
  natural register.
- **Full i18n framework now** — deferred: unnecessary weight for a single-locale POC, but
  CT-3 keeps the door open.
