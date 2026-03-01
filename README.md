# Decision-Centric Model System (DCMS)

DCMS is an infrastructure-style pattern for **decision-centric AI/ML systems**: every model decision is treated as a first-class event with structured metadata, replay boundaries, and integrity anchoring.

The goal is to make modern ML/LLM systems **operationally defendable** without turning product teams into compliance teams.

## What this is

DCMS is a reference implementation + evolving spec for:

- **Deterministic decision recording** (append-only events)
- **Policy/runtime outcomes** (allow / warn / deny / emit)
- **Replay boundaries** that define what “replay” means for a decision
- **Evidence references** (content-addressed pointers, not necessarily raw payload storage)
- **Lineage edges**, including the ability to represent rejected alternatives (“negative lineage”)
- **Integrity anchoring** via canonical hashing (and optional chaining)

## Why decision-centric?

In non-deterministic systems (LLMs, stochastic pipelines, tool-using agents), the output alone is not a stable artifact.
A decision-centric approach records the **inputs, constraints, and boundary conditions** that produced a decision so that later you can:

- explain what happened
- reason about drift/regressions
- re-evaluate under new policies
- support incident response and root-cause analysis

## Core event fields (high level)

Events typically include:

- **Identity**: tenant / producer / source, event_id, decision_id
- **Timing**: captured timestamps
- **Actor / Subject**: who/what initiated; what it acted on
- **Outcome**: verdict + confidence + reason (and optional policy identifiers)
- **Replay boundary**: the declared replay mode + pinned artifacts/configs
- **Lineage**: dependency edges + negative lineage commitments
- **Evidence refs**: content URIs + hashes (optional bytes)
- **Observability**: latency and execution path metadata
- **Integrity**: canonical event_hash (optional chain hash)

(Internally, the system enforces required fields and validation gates—e.g., schema version checks, replay_mode validity, integrity hash presence, and negative-lineage completeness.) :contentReference[oaicite:0]{index=0}

## Repository posture

This repository is structured like an infrastructure project:

- specs / contracts (public, slimmed where appropriate)
- reference implementation (runtime + validation)
- examples and tests
- docs focused on engineering usage, not consulting

## Background

This project evolved from independent research and hands-on experimentation in security architecture and AI/ML reliability from 2023–2025, and has been built as a personal engineering effort.

## License

MIT
