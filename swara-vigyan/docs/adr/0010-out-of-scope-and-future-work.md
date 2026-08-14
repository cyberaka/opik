# ADR-0010: Out of Scope, Pending Rules & Future Work

- **Status:** Accepted (revised for Consolidated Master Notes v1)
- **Date:** 2026-08-14
- **Deciders:** POC owner (practitioner / product), engineering
- **Tags:** scope, roadmap, pending, disclaimer

## Context

To stay focused and honest, it matters to record what the product is **not**, and — critically for
this domain — **what the Guru has not yet taught** so the app never invents it. This ADR
consolidates non-goals, pending rules, roadmap, and disclaimer framing.

## Decision

### Explicitly out of scope

- **OS-1:** User accounts, authentication, roles, multi-practitioner support.
- **OS-2:** Any backend/database or off-device sync (local opt-in log only, ADR-0008).
- **OS-3:** Automatic detection of the active nostril or breath phase (always entered manually).
- **OS-4:** Swara Vigyan content beyond these teachings (other systems, panchang, etc.).
- **OS-5:** Full multi-locale switching (structure kept ready per CT-3; ships bilingual only).
- **OS-6:** **Inventing** any prediction where the Guru's rule is not known — see Pending below.
- **OS-7:** Native mobile app in the POC (web only; mobile is future, ADR-0009 FD-1).
- **OS-8:** Aggregating conflicting signals into a single verdict (ADR-0014).
- **OS-9:** Encoding Meethi Goli color/object/timing as causal or outcome-mapped (ADR-0016).
- **OS-10:** Presenting remedies (ADR-0018) as medical treatment, making efficacy/diagnosis claims,
  or editing the teaching to add/soften claims (ADR-0019, ADR-0017).

### Pending — rules to learn from the Guru (must NOT be invented)

These resolve to a `Pending` state in the app (ADR-0014) until taught, then get their own ADR:

- **PD-1:** Priority/resolution when multiple signals **conflict**.
- **PD-2:** **Behind + Chandra (LEFT)** result (only Behind+Surya is taught).
- **PD-3:** **Sabha** reading when the questioner is on the **Khali** side (exact rule).
- **PD-4:** Consultation/prediction rule when **Sushumna** is active.
- **PD-5:** Swara-**transition timing** rules.
- **PD-6:** How interpretation changes with **different question types**.
- **PD-7:** How to **combine Saguna/Nirguna with Bhara/Khali**.
- **PD-8:** General **exceptions / special cases**.
- **PD-9:** **Meethi Goli** selection rules (any color/object/timing ↔ Swara relation).

Remedies (ADR-0018) — marked `NEEDS CLARIFICATION` (ADR-0017) until confirmed:

- **PD-10:** **Low-BP exact duration** (High-BP is taught as 5–10 min; Low-BP repeated the pattern
  without an explicit duration).
- **PD-11:** Exact durations for the water remedies (fever / cold) were not specified.
- **PD-12:** Any additional conditions, contraindications, or refinements the Guru teaches later.

Daily practice & new modes (v2 — ADR-0020/0012):

- **PD-13:** The complete **Tithi → Chandra/Surya mapping** for all Tithis (only Krishna Paksha
  Navami → Surya is taught).
- **PD-14:** Morning rule — **which foot** to place down first when leaving the bed.
- **PD-15:** Morning rule — **how** to place the foot.
- **PD-16:** Morning **intention / मनोवांछित** technique.
- **PD-17:** The exact method for **self-prediction after mastery**.
- **PD-18:** Proxy mode — exact mapping of the **proxy's Swara/state → YES/NO** (ADR-0012 Mode F).
- **PD-19:** Further applications/rules of the **"रम रम"** beejakshara beyond those taught.

(Mirrors ADR-0014's pending list and ADR-0017's `NEEDS CLARIFICATION`; keep them in sync.)

### Roadmap (each adopted item gets its own ADR)

- **FW-1:** Build order per ADR-0001 phasing — Phase 1 Independent Room + core; Phase 2 other modes
  + signals; Phase 3 signal-aggregation UX and (once taught) conflict resolution.
- **FW-2:** Opt-in local consultation log UI (view/export/delete) over the ADR-0015 schema.
- **FW-3:** Full localization / language switcher.
- **FW-4:** PWA install + offline service worker.
- **FW-5:** Teaching mode (guided practice/quizzes over rules and modes).
- **FW-6:** Mobile app sharing the pure derivation core (ADR-0009 FD-1).
- **FW-7:** Ruleset-version migration tooling to reprocess history when pending rules are taught
  (ADR-0015 DA-4).
- **FW-8:** **TODAY** module — Tithi/sunrise/wake-up practice (ADR-0020), incl. optional astronomical
  sunrise/tithi lookup as a clearly-labelled `RESEARCH NOTE` convenience.
- **FW-9:** **IMPORTANT EVENTS** module — public-speaking guidance (ADR-0021); extensible to other
  taught event practices.
- **FW-10:** **My Question / Proxy** prediction mode (ADR-0012 Mode F) once the proxy→YES/NO mapping
  is taught, and a **PRACTICE JOURNAL** over the ADR-0015 schema.

### Disclaimer & framing (required)

- **DC-1:** The app MUST present a brief disclaimer: it is a **study/assistance tool** for the
  Swara Vigyan tradition and **not** medical, legal, financial, or professional advice; decisions
  remain the user's responsibility.
- **DC-2:** It assists the practitioner in applying a traditional method faithfully; it does not
  claim scientific validation of outcomes.
- **DC-3:** Where the tradition prescribes restraint (Rule 0 not met, or a Pending case), the app's
  honest "do not predict / pending" output is a feature, not a limitation.

## Consequences

- A clear boundary plus an explicit pending list prevents scope creep **and** fabricated rules,
  keeping the app trustworthy as the teaching grows.
- Each future/pending item is gated behind its own ADR, preserving the decision trail (ADR-0000).
