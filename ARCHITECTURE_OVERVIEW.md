# Architecture Overview – Decision-Centric Model System (DCMS)

DCMS is a structural pattern for recording AI/ML decisions as first-class events.

It does not attempt to make models deterministic.
It makes decision recording deterministic.

---

## Core Idea

A decision is:

> An action influenced by a model or policy under specific boundary conditions.

Instead of logging only outputs, DCMS records:

- Who/what acted
- What decision was made
- Under which declared replay boundary
- With which pinned artifacts (e.g., model/policy versions)
- With an integrity hash

---

## Conceptual Layers

1. **Decision Capture**
   - Accept structured events
   - Enforce schema discipline
   - Normalize for hashing

2. **Policy / Runtime (Optional)**
   - Produce verdicts (allow / warn / deny / emit)
   - Attach decision metadata

3. **Replay Boundary**
   - Declare what must be pinned for replay
   - Keep replay definition explicit

4. **Integrity Anchoring**
   - Canonical hashing of decision events
   - Optional chaining or aggregation (implementation-specific)

---

## Design Principles

- Vendor-neutral
- Framework-agnostic
- Storage-agnostic
- Minimal surface area
- Forward extensible

DCMS is a pattern, not a product.
