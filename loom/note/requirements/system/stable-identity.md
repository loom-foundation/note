---
id: note:req:sfmkwmm
name: Stable, location-independent identity
kind: requirement
level: system
type: functional
status: current
---

Note shall ensure that an artifact can be referenced by a durable handle that does not change when the artifact is moved, renamed, or substantially revised in content or scope;
and that a reference pairs that handle with a human-readable label, so a reference is legible to a person and resolvable by a tool even after reorganization.

## Rationale

Conflating an artifact's identity with its file path, its heading, or its description makes routine refactoring shatter the traceability graph;
worse, an identifier built from the artifact's wording starts to lie when the wording changes.

The durable handle must therefore be distinct from, and need not encode, the artifact's current meaning: a human-readable label travels with each reference and may be rewritten freely, while the handle stays fixed and the navigation link self-heals against it as artifacts move.

A reference carries the label so a reader far from any editor (in prose, a code comment, a commit message) can still read it, and carries the handle so a tool can still resolve it.

The handle's form, and its separation from the label and the navigation link, is specification; this requirement is what makes cross-repository resolution possible ([Cross-repository resolution](cross-repository-resolution.md){id=note:req:dxxvabc}).

## Relations

- derivedFrom: [Inspectable traceability](../stakeholder/inspectable-traceability.md){id=note:req:sg0npmv}
- derivedFrom: [Durable, portable intent](../stakeholder/durable-portable-intent.md){id=note:req:93kczqj}
