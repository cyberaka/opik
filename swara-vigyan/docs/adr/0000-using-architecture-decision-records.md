# ADR-0000: Using Architecture Decision Records

- **Status:** Accepted
- **Date:** 2026-08-14
- **Deciders:** POC owner (practitioner / product), engineering
- **Tags:** process, documentation

## Context

The Swara Vigyan POC begins as a requirements-and-design exercise, not code. The
domain (स्वर विज्ञान — Independent Room Consultation) has precise, non-obvious rules
that must be captured unambiguously before any implementation, because a subtle
mistake in the domain logic (e.g. confusing *left* with *bhara*) would silently
produce wrong predictions.

We need a lightweight, versioned way to record *what* the product must do and *why*
each design choice was made, that lives next to the eventual code and evolves with it.

## Decision

We will capture all requirements and significant design decisions as
**Architecture Decision Records (ADRs)** — one Markdown file per decision, stored in
`docs/adr/`, numbered sequentially (`NNNN-title.md`).

Each ADR uses this structure:

- **Title** — `ADR-NNNN: Short decision title`
- **Status** — `Proposed` → `Accepted` → (later) `Deprecated` / `Superseded by ADR-XXXX`
- **Date**, **Deciders**, **Tags**
- **Context** — forces at play, requirements, constraints
- **Decision** — what we will do (including explicit requirements)
- **Consequences** — resulting trade-offs, positive and negative
- **Alternatives considered** — where relevant

### Conventions

1. ADRs are **immutable once Accepted**; to change a decision, add a new ADR that
   supersedes the old one and update the old one's Status.
2. Requirements are written as testable statements. Where an ADR states behaviour,
   it should also state how that behaviour is verified (examples / acceptance cases).
3. The `README.md` index must be updated whenever an ADR is added.

## Consequences

- **Positive:** Shared, reviewable source of truth; onboarding is a single folder;
  domain rules are pinned before code exists, reducing correctness risk.
- **Positive:** History of *why* is preserved even when *what* changes.
- **Negative:** Slight upfront overhead; discipline required to keep ADRs current.

## Alternatives considered

- **A single monolithic requirements document** — harder to review incrementally and
  loses the decision/rationale framing.
- **Issue tracker only** — decisions get buried; no versioned narrative next to code.
