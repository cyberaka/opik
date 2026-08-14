# ADR-0009: Repository, Hosting & Deployment

- **Status:** Accepted
- **Date:** 2026-08-14
- **Deciders:** POC owner, engineering
- **Tags:** repo, hosting, deployment, process

## Context

The work needs a home and a simple way to view the app. Given the static, no-backend
architecture (ADR-0005) and privacy posture (ADR-0008), hosting is straightforward, but a
few choices should be recorded.

## Decision

### Repository

- **RP-1:** Source of truth is the existing **`opik`** repository, with this knowledge base living
  under the top-level **`swara-vigyan/`** directory (`swara-vigyan/README.md` +
  `swara-vigyan/docs/adr/`). A separate `swara_vigyan_poc` repo was considered but the owner chose
  to keep everything in `opik`; the ADR content and structure are unchanged by that choice.
- **RP-2:** The `swara-vigyan/` tree starts as documentation-only (this ADR set). Application code,
  if built, lands later under the same directory (e.g. `swara-vigyan/app/`), with ADRs remaining in
  `swara-vigyan/docs/adr/`.
- **RP-3: Branching.** Work happens on short-lived feature branches (current:
  `claude/swara-vigyan-room-rules-firsxd`) and is merged via pull request. Commit messages are
  descriptive.

### Hosting & deployment

- **HP-1:** The deliverable is **static files** hostable on any static host or opened
  directly from disk (`file://`) — no server required.
- **HP-2: Hosting options** (to be chosen when code exists, recorded here as candidates):
  - **Local / offline** — open `index.html`; always available, matches offline goal.
  - **Static host (e.g. Netlify / Vercel / Cloudflare Pages / S3)** — simple drag-or-CI deploy,
    works with a private source repo.
  - **GitHub Pages** — note: serving Pages from a **private** repo requires a paid GitHub
    plan; if the repo must remain private and free, prefer a static host or keep it local.
- **HP-3:** Any deployment MUST preserve the no-external-dependency property (ADR-0005 TS-2)
  so the hosted app behaves identically to the offline one.
- **HP-4:** Deployment is manual for the POC; CI/CD is optional and can be added later
  without a new architectural decision (it would not change the artifact).

## Consequences

- **Positive:** Trivial to host and to demo offline; private by default.
- **Negative:** The private-repo + GitHub Pages friction (HP-2) is called out so it isn't
  hit by surprise; a static host sidesteps it.

### Future direction

- **FD-1:** Master Notes v1 names a **future mobile app** as a goal. The durable asset is the
  raw-observation data contract and pure derivation core (ADR-0015), which are UI-agnostic; the web
  POC and a later mobile app can share that core. A move to mobile would be recorded in a new ADR
  and does not change this repo's role as the knowledge base + reference implementation.

## Notes

- If repository creation is performed via tooling with limited permissions, the private repo
  may need to be created once by the owner; subsequent pushes proceed normally.
