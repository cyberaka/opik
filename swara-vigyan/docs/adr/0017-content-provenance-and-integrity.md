# ADR-0017: Content Provenance & Integrity Convention

- **Status:** Accepted
- **Date:** 2026-08-14
- **Deciders:** POC owner (practitioner / product), engineering
- **Tags:** content, integrity, provenance, cross-cutting

## Context

The knowledge base mixes two kinds of statements: what the **Guru taught** (to be preserved
verbatim in meaning, strength, and duration) and any **external/derived commentary** (research
context, safety notes, engineering interpretation). The source notes are explicit:

> मूल teaching और commentary mix न हों। Guru की original teaching और external interpretation कभी
> mix नहीं होंगी।

This applies to **both** capabilities — Consultation/Prediction and Remedies. A single, project-wide
provenance convention is needed so nothing blurs the line, and so contradictions surface instead of
being silently resolved.

## Decision

Every substantive statement in the knowledge base and every user-facing claim in the app carries one
of three **provenance labels**:

| Label | Meaning | Rule |
|-------|---------|------|
| **GURU TEACHING** | Stated by the Guru | Captured in the Guru's form; **not** altered, "corrected", or embellished. Strength/duration preserved (e.g. "6th minute", "5–10 min"). |
| **RESEARCH / SAFETY NOTE** | External text, research, or app/engineering commentary | Clearly separated and labelled as commentary; never presented as the Guru's words. |
| **NEEDS CLARIFICATION** | Two teachings appear to contradict, or a detail is unconfirmed | Flagged, not resolved. No guess is substituted. |

### Requirements

- **PV-1:** Source content is stored with an explicit provenance field; **GURU TEACHING** content is
  never edited to merge in commentary.
- **PV-2:** The UI **visually distinguishes** the three labels (e.g. teaching vs a set-apart
  research/safety note vs a clarification flag). A safety note must never look like part of the
  teaching, and vice versa.
- **PV-3:** **Do not invent / do not resolve.** Unknown or unconfirmed items are labelled
  `NEEDS CLARIFICATION` (or `Pending`, ADR-0014) rather than filled with a plausible answer. This
  extends the consultation-side "never invent" principle (ADR-0014) to *all* content, including
  remedy details (e.g. Low-BP exact duration, ADR-0018).
- **PV-4:** Contradictions between two Guru teachings are surfaced as `NEEDS CLARIFICATION` with both
  statements shown; the app picks neither until the Guru clarifies.
- **PV-5:** Relationship to existing labels: `Pending` (ADR-0014, unresolved *prediction* cases) and
  `NEEDS CLARIFICATION` (contradiction/unconfirmed *content*) are both "not-yet-known" states and are
  presented with the same honesty; they may be tracked in one list (ADR-0010 §Pending).

## Consequences

- **Positive:** The tradition's exact teaching stays pristine and auditable; commentary is useful but
  never mistaken for scripture; disagreements become explicit learning prompts.
- **Positive:** Gives the remedies module (ADR-0018) a clean way to attach safety commentary
  (ADR-0019) without contaminating the teaching.
- **Negative:** Slightly more metadata per statement and more UI treatment — a worthwhile cost for
  integrity.

## Alternatives considered

- **One undifferentiated content stream** — rejected: it is exactly the mixing the source notes
  forbid, and it would let safety/engineering commentary masquerade as teaching.
