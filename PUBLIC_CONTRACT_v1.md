# Public Contract v1 – Decision Event (Slim Reference)

This document describes a minimal, public-facing reference contract
for representing AI/ML decisions as structured events.

It intentionally omits advanced internal fields and extensions.

This is a reference surface — not a complete production schema.

---

## Design Goals

The contract is designed to:

- Represent AI decisions as structured, replay-aware events
- Separate outcome from execution environment
- Preserve forward extensibility
- Allow integrity anchoring
- Remain vendor-neutral

---

## Minimal Decision Event Structure

```json
{
  "schema_version": "dcms.event.v1",
  "event_id": "uuid",
  "decision_id": "uuid",

  "producer": {
    "namespace": "string",
    "source": "string"
  },

  "timestamps": {
    "captured_at": "epoch_ms",
    "occurred_at": "ISO8601"
  },

  "decision_type": "string",

  "actor": {
    "type": "user | system | service",
    "id": "string"
  },

  "subject": {
    "type": "resource | model | tool",
    "id": "string"
  },

  "outcome": {
    "verdict": "allow | warn | deny | emit",
    "confidence": "float (0.0–1.0)",
    "reason": "string"
  },

  "replay_boundary": {
    "mode": "signal | partial | full",
    "artifacts": {
      "model_version": "string",
      "policy_version": "string"
    }
  },

  "evidence_refs": [
    {
      "content_uri": "string",
      "content_hash": "sha256:..."
    }
  ],

  "integrity": {
    "event_hash": "sha256:..."
  }
}
