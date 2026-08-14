# ADR-0003: Room Layout & Perspective Convention

- **Status:** Accepted (revised for Consolidated Master Notes v1)
- **Date:** 2026-08-14
- **Deciders:** POC owner (practitioner / product), engineering
- **Tags:** domain, convention, ui

> **Scope note:** The *perspective convention* below (LEFT/RIGHT = practitioner's view) is
> **global** — it applies in every consultation mode (ADR-0012). The specific *room layout* with a
> fixed right-side entrance is specific to **Mode A — Independent Room**; other modes (Shared
> Chamber, Sabha, Remote, Behind) have their own geometry and may have no meaningful entrance.

## Context

"Left" and "right" are ambiguous unless a fixed reference frame is chosen: the visitor's
left is the practitioner's right. Because the entire method depends on correctly reading
entry and seating *sides*, the reference frame must be pinned once and enforced everywhere
— in copy, in the diagram, and in the engine. This ADR records the physical room setup and
the perspective convention.

## Decision

### Perspective convention (invariant)

> **All LEFT / RIGHT references in this product are from the PRACTITIONER's perspective.**

- CR-1: Every label, diagram, and stored value that mentions left/right MUST be from the
  practitioner's point of view.
- CR-2: The UI MUST make this explicit to the practitioner (a stated convention near the
  inputs and on the room diagram), to avoid the visitor-vs-practitioner mix-up.

### Physical room setup

- The practitioner sits with their **back to the wall**.
- In front of them are **two seating positions**: practitioner's **LEFT chair** and
  practitioner's **RIGHT chair**.
- The **entrance is on the practitioner's RIGHT side**; visitors enter from there.

```text
                    FRONT OF ROOM
        ┌─────────────────────────────┐
        │    LEFT           RIGHT      │
        │    CHAIR          CHAIR      │
        │      ○              ○        │
        │                             │ ← ENTRANCE
        │                             │ ← PERSON ENTERS
        │            YOU              │
        │       (Practitioner)        │
        │             ◎               │
        ├─────────────────────────────┤
        │          BACK WALL          │
        └─────────────────────────────┘
```

### Requirements

- CR-3: The app MUST render a room diagram matching this layout, including the entrance
  on the practitioner's right.
- CR-4: The diagram SHOULD visually annotate each chair with its current Bhara/Khali
  polarity once the active nostril is chosen (see ADR-0006), reinforcing the conversion.
- CR-5: **The rule engine MUST NOT hard-code entry to the right.** Although this specific
  room has its entrance on the right (so in practice entry is usually from the right), the
  engine treats *entry side* as an independent observed input. This keeps the engine
  faithful to the general four-rule framework and reusable for rooms with a different
  entrance. The fixed entrance is a property of the *diagram/room*, not of the *logic*.

## Consequences

- One reference frame removes an entire category of user error and reviewer confusion.
- Keeping entry as a free input (CR-5) means the four rules remain fully general and every
  matrix cell is reachable, even though the depicted room biases entry to the right.

## Alternatives considered

- **Hard-coding entry = RIGHT** to match this room exactly — rejected: it collapses the
  four-rule model, makes two rules unreachable, and couples logic to one room's geometry.
- **Visitor-perspective labels** — rejected: the source teaching and the practitioner's
  live observation are both practitioner-centric.
