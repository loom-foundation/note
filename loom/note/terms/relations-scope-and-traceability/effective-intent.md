---
id: note:term:b0f7xzp
name: Effective Intent
kind: term
status: current
---

The intent in force at a given Scope, computed by walking the Scope graph and applying the cascade, with conflicts between comparable sources resolved by proximity and genuine ties surfaced rather than silently merged.

Effective Intent is always a derived view; it is never stored as a second source of truth while the corpus is live.

(Materialization is the one deliberate exception, and it severs the link and records provenance.)

## Inclusion test

Was it computed from authored artifacts and the cascade, rather than authored directly?
If authored directly as a standalone fact, it is either a Materialized artifact (with provenance) or a Single-Source-of-Truth violation.

## Relations

- *contrasts with* [Materialization](materialization.md){id=note:term:3yted77} (always a derived view, never stored while the corpus is live; Materialization is the deliberate exception)

## Origin

A coinage of this corpus, pairing "effective" in its general-English sense (Oxford: "actual rather than official or theoretical") with Intent: the intent that is actually in force at a Scope once the cascade is applied, as opposed to any single authored fragment of it.

The construction echoes "effective rate" or "effective permissions" in computing, where a final value is resolved from layered sources rather than read off one of them.
