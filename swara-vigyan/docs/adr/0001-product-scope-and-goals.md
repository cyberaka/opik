# ADR-0001: Product Scope & Goals

- **Status:** Accepted (revised for Consolidated Master Notes v1)
- **Date:** 2026-08-14
- **Supersedes:** the original single-mode scope of this ADR
- **Deciders:** POC owner (practitioner / product), engineering
- **Tags:** scope, requirements, product

## Context

A Swara Vigyan practitioner predicts the outcome of a visitor's question by observing energy
(**Bhara** / **Khali**, derived from their own active nostril) at meaningful moments. The
consolidated teaching (Master Notes v1) shows this is not a single procedure but a **family of
consultation modes and prediction signals** sharing one core idea:

> **Relevant moment पर energy observe करो, फिर interpret करो.**

The product must serve daily practice **and** act as a durable **knowledge base** for a future
mobile app, faithfully encoding the canonical rules while clearly marking what the Guru has not
yet taught (so nothing is invented).

## Decision

### Purpose

Build a **single-practitioner Swara Vigyan practice assistant** with **two capabilities**:

**Capability 1 — Consultation & Prediction.** Given the practitioner's active Swara and observations,
identify the applicable rule(s)/signal(s) and present the reading. It:

1. gates prediction behind practitioner readiness (**Rule 0**, ADR-0011);
2. lets the practitioner pick a **consultation mode** (ADR-0012);
3. captures **raw observations** for that mode;
4. derives one or more **prediction signals** (ADR-0004, ADR-0013);
5. presents each signal's reading — and, when signals disagree, shows the conflict rather than
   inventing a resolution (ADR-0014);
6. carries reference material and the Guru's examples.

**Capability 2 — Remedies & Therapeutic Practices** (ADR-0018). A Swara-first reference for the
taught breath/Swara remedies (headache/anxiety/migraine, BP, fever, cold, **constipation**, body
pain, **charged wool**), with taught durations, an optional personal practice record, and — clearly
separated from the teaching — health-safety disclaimers (ADR-0019).

**Capability 3 — Daily Practice / TODAY** (ADR-0020). Tithi → expected Swara, the sunrise checkpoint,
and morning wake-up guidance (50/50 model, final vs temporary wake-up) — recording only what is
taught (the full Tithi mapping and morning micro-rules are Pending).

**Capability 4 — Important Events** (ADR-0021). Proactive *action-in-a-chosen-Swara* guidance,
starting with public speaking / mass gathering (Chandra→stage, Surya+inhale→greet, Surya→present).

Cross-cutting for all capabilities: the Swara domain model (ADR-0002), the **content-provenance
convention** (Guru Teaching / Research-Safety Note / Needs Clarification — ADR-0017), the raw-first
data approach (ADR-0015), and the privacy stance (ADR-0008). Consultation adds a **My Question /
Proxy** mode (ADR-0012 Mode F). The envisioned module map (ADR-0005): **TODAY · SWARA OBSERVATION ·
PREDICTION · REMEDIES · IMPORTANT EVENTS · PRACTICE JOURNAL**.

> **Reliability (GURU TEACHING, attributed):** *"Law of Attraction fail हो सकता है, लेकिन Swara
> Vigyan fail नहीं होता।"* Captured as the Guru's words, never as the app's own guarantee
> (ADR-0017 PV-7, ADR-0019 SF-4).

### Primary user

- **The practitioner** — the only interactive user. Visitors are observed, never users.

### Functional requirements (FR)

Core Bhara/Khali & four rules:

| ID | Requirement |
|----|-------------|
| FR-1 | Select the active nostril (LEFT/RIGHT); derive Bhara/Khali sides (with Chandra/Surya labels). |
| FR-2 | Convert any observed side to Bhara/Khali using the current active nostril, never fixed to L/R. |
| FR-3 | Apply the four energy rules to a First → Second energy transition and show the prediction. |

Readiness & modes:

| ID | Requirement |
|----|-------------|
| FR-4 | Enforce **Rule 0**: block prediction unless the practitioner marks body/senses/mind/Swara clear. |
| FR-5 | Offer the consultation modes: Independent Room, Shared/Chamber, Sabha/Group, Remote/Position-Unknown, Behind-the-Practitioner. |
| FR-6 | Capture the mode-appropriate observation moments (e.g. entry+seating; sit-time+question-time; questioner side + question-time swara; question-time breath). |

Additional signals:

| ID | Requirement |
|----|-------------|
| FR-7 | Capture question-time breath phase and derive Saguna (inhale→positive) / Nirguna (exhale→negative). |
| FR-8 | Capture whether the practitioner was addressed before or after the question (addressing signal). |
| FR-9 | Support position-swara (Sabha) and behind-position readings, including the *pending* Behind+Chandra case (must not invent a result). |
| FR-10 | Record whether breath observation was spontaneous; a manipulated breath must not be used. |

Signals, output & reference:

| ID | Requirement |
|----|-------------|
| FR-11 | Compute available signals **independently** and display each; surface conflicts explicitly (no invented tie-break). |
| FR-12 | Store **raw observations separately from derived interpretations** so future rule changes can reprocess history (ADR-0015). |
| FR-13 | Represent **Meethi Goli** as an optional symbolic action, never as a cause of the outcome (ADR-0016). |
| FR-14 | Provide reference material (four rules, matrix, cheat sheet, golden principles) and loadable Guru examples (incl. Sunita swara-change). |
| FR-15 | One-tap reset; live, incomplete-input-safe results (never a guessed prediction). |

Remedies capability (ADR-0018/0019):

| ID | Requirement |
|----|-------------|
| FR-16 | Browse remedies by condition; each is **Swara-first** (read current active Swara before acting). |
| FR-17 | Present each remedy's steps and taught duration **exactly as taught** (`GURU TEACHING`), with no added efficacy claims. |
| FR-18 | Show health-safety disclaimers on the Remedies module and every remedy screen, **visually separated** from the teaching (ADR-0019). |
| FR-19 | Offer an optional, opt-in, local-only **personal practice record**; may offer a convenience timer for taught durations. |
| FR-20 | Label all content by provenance — Guru Teaching / Research-Safety Note / Needs Clarification (ADR-0017). |

Daily practice & events (ADR-0020/0021) and proxy (ADR-0012):

| ID | Requirement |
|----|-------------|
| FR-21 | **TODAY** module: show Tithi/paksha, sunrise, wake-up guidance; compare observed sunrise Swara to the expected one **only where taught** (else `NEEDS CLARIFICATION`); never auto-derive an unknown Tithi's Swara. |
| FR-22 | Let the practitioner **manually record** the expected Swara they were taught for a given day. |
| FR-23 | **IMPORTANT EVENTS → Public Speaking**: present the taught three-phase Swara guidance (guidance, not a YES/NO prediction). |
| FR-24 | **My Question / Proxy** mode: capture another person's spontaneous Swara/state; show `Pending` for the YES/NO mapping (not yet taught). |
| FR-25 | Preserve exact taught terms (e.g. **"रम रम"**, count 27, 24 hours) without normalization (ADR-0017 PV-6). |
| FR-26 | Keep **action** intent (act in a chosen Swara: events/remedies) distinct from **observation** intent (spontaneous, never manufactured: prediction) — ADR-0021 EV-0. |

### Phasing

- **Phase 1 (POC, buildable now):** Rule 0 gate + **Independent Room** mode + four-rule engine +
  raw/interpretation split + reference/examples. This is the correctness spine.
- **Phase 2:** other consultation modes and additional signals (breath, addressing, position, behind).
- **Phase 3:** signal aggregation UX and (only once taught) conflict-resolution rules.
- **Remedies track (parallel):** the Remedies module (ADR-0018) + safety framing (ADR-0019) can be
  built independently of the consultation phases, since it shares only the Swara model, provenance,
  and privacy foundations. It has its own catalogue → practice-record increments.

Requirements for all phases/tracks are captured now; the consultation build order is Phase 1 → 3, with
the Remedies track schedulable in parallel.

### Goals

- **Correctness & fidelity first** — exactly reproduce canonical rules; pass all example scenarios.
- **Never invent** — unresolved cases are surfaced as "pending", not guessed.
- **Reprocessable** — raw observations outlive any single interpretation.
- **Zero-friction & offline** — usable live in a few taps.

### Non-goals (see ADR-0010)

Multi-user/accounts; automatic nostril/breath detection; content beyond these teachings;
inventing conflict-resolution or pending rules.

## Consequences

- Scope is broad but **phased**, keeping a shippable Phase-1 POC while capturing the full model.
- The raw/interpretation split (FR-12) is now a first-class requirement, changing the data design
  (ADR-0015) and the privacy stance (ADR-0008).
