---
id: note:req:t3rfrc5
name: Derivable tier in force
kind: requirement
level: system
type: functional
status: current
---

Note shall ensure the conformance tier in force for any artifact is derivable from the committed files alone, by resolving the artifact's enclosing scope against the declared profiles, with no per-artifact rigor field stored or required.

## Rationale

A reviewer reading an approved artifact needs to know what discipline it was held to; the answer is already determined by the scope's declared profile, so the method obligates the derivation rather than a stored duplicate that would drift against the declaration.

This is the same no-mirrored-state posture the grouping and effective-intent rules take: declaration once, views derived.

## Relations

- derivedFrom: [Tiered conformance](tiered-conformance.md){id=note:req:bth0rxp}
- decidedBy: [Conformance profiles as pure rigor bundles](../../decisions/conformance-profiles.md){id=note:dec:cf7n2wq}
- delivers: [The Rigor an Artifact Was Held To Is Legible](../../offerings/ceremony-that-scales/pr-required-rigor-legible-on-the-artifact.md){id=note:pr:a5b6drw}
