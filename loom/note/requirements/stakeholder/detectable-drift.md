---
id: note:req:d6m4q7z
name: Detectable drift
kind: requirement
level: stakeholder
type: functional
status: current
---

A reader shall be able to detect, by inspection of the artifacts, when a relationship has gone stale or when a dependent has diverged from what it relied on, so that staleness and divergence surface for re-check rather than being discovered only when the running system fails to do what was promised.

## Source

See the Source of [Trust and drift visibility](../../needs/trust-intent-is-honored.md){id=note:need:46tkxcn}.

## Rationale

Legible relationships answer how artifacts relate, but not whether those relationships are still current;
intent and the systems built from it diverge silently as text moves and behavior drifts.

The Need to see drift early is therefore a distinct obligation from [Inspectable traceability](inspectable-traceability.md){id=note:req:sg0npmv}: staleness (a referenced text moved) and divergence (an implementation no longer honors a contract) both surface by inspection.

This requirement states that drift be detectable and leaves how staleness and divergence are detected, and the distinction between them, to specification.

## Relations

- addresses: [Trust and drift visibility](../../needs/trust-intent-is-honored.md){id=note:need:46tkxcn}
- delivers: [Drift Surfaced Early](../../offerings/trust-by-inspection/pr-drift-surfaced-early.md){id=note:pr:cvarqvw}
