# ADR-0005: Application Architecture & Tech Stack

- **Status:** Accepted (revised for Consolidated Master Notes v1)
- **Date:** 2026-08-14
- **Deciders:** engineering, POC owner
- **Tags:** architecture, tech-stack

## Context

The POC has a small, self-contained domain (ADR-0004), a single user (ADR-0001), no
server-side data needs, and a strong privacy preference (ADR-0008). It must be usable
offline during a consultation and easy to host from a private repository. This ADR fixes
the architecture and technology.

## Decision

### Architecture

- **AR-1: Client-side only.** The POC is a static, single-page application. There is **no
  backend, no API, and no database.** All logic runs in the browser.
- **AR-2: Pure domain core.** The signal/rule engines (ADR-0004, ADR-0013) are isolated,
  dependency-free modules (pure functions) so they can be unit-tested independently of the UI.
- **AR-3: Clear layering — raw → derivation → presentation** (aligns with ADR-0015):
  1. **Raw observations** — captured facts per mode (nostril-at-moment, sides, breath phase,
     addressing order, readiness), with **no derived conclusions** stored.
  2. **Derivation (domain)** — pure functions computing independent signals and the four-rule
     transition from raw observations + a `ruleset_version`; no DOM access.
  3. **Presentation** — Rule 0 gate, mode selection, observation capture, per-signal display and
     conflict/pending surfacing (ADR-0014), room diagram, reference, examples.
- **AR-5: Reprocessability.** Because derivation is pure and raw facts are stored separately, any
  history can be re-derived when the ruleset advances (ADR-0015). Derived verdicts are never the
  source of truth.
- **AR-6: Mobile-app direction.** The POC is a responsive web app, but the raw-observation schema
  and pure derivation core are designed to be **portable to a future mobile app** (the notes'
  stated goal). The data contract (ADR-0015), not the web UI, is the durable asset.
- **AR-7: Module map.** The product is organized into modules over the shared domain/derivation core:
  ```text
  SWARA VIGYAN
  ├── TODAY              (Tithi, sunrise, expected Swara, wake-up — ADR-0020)
  ├── SWARA OBSERVATION  (Chandra/Surya, Saguna/Nirguna — ADR-0002/0013)
  ├── PREDICTION         (Independent Room, Shared, Sabha, Remote, Behind, My-Question/Proxy — ADR-0012)
  ├── REMEDIES           (headache/BP/fever/cold/constipation/pain/charged-wool — ADR-0018)
  ├── IMPORTANT EVENTS   (Public Speaking — ADR-0021)
  └── PRACTICE JOURNAL   (opt-in local records over the ADR-0015 schema)
  ```
  Modules are thin presenters; all rules live in the pure core (AR-2/AR-3) so they stay testable and
  reprocessable (AR-5).
- **AR-4: Offline-capable.** The app must fully function with no network after first load
  (no runtime external requests). A service worker/PWA manifest is optional for the POC
  but the app MUST NOT depend on any network call to compute a prediction.

### Technology

- **TS-1: Vanilla HTML + CSS + JavaScript**, no framework, no build step for the POC.
  Rationale: the app is tiny; a framework and toolchain would add more weight and setup
  than they save, and "open `index.html` and it works" is the simplest hosting/offline story.
- **TS-2: No third-party runtime dependencies / CDNs.** Everything is self-contained so the
  app works offline and leaks nothing to third parties (supports ADR-0008). If any asset is
  needed (icons/fonts), it is inlined or bundled locally.
- **TS-3: Static hosting compatible.** Output is a folder of static files hostable on any
  static host or opened directly from disk (see ADR-0009).

### Testing

- **TS-4:** The domain core has automated unit tests covering all ADR-0004 acceptance and
  derived cases. Because the core is framework-free, tests can run in a minimal runner
  (browser-based or a lightweight Node script) without a heavy toolchain.

## Consequences

- **Positive:** Minimal moving parts; instant startup; trivially private and offline;
  nothing to deploy but static files.
- **Positive:** The pure engine + layering keeps correctness isolated and testable.
- **Negative:** Vanilla JS means more manual DOM wiring than a framework; acceptable at
  this size. If scope grows substantially (ADR-0010), a framework + build step can be
  revisited via a superseding ADR.

## Alternatives considered

- **React/Vue + bundler** — more ergonomic for large UIs, but overkill here and adds a
  build/deploy toolchain and dependencies that conflict with the offline/no-CDN goal.
- **Server-rendered app** — unnecessary; there is no shared or persisted data and it would
  add hosting and privacy burden.
