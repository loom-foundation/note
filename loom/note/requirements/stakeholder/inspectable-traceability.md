---
id: note:req:sg0npmv
name: Inspectable traceability
kind: requirement
level: stakeholder
type: functional
status: current
---

A reader shall be able to determine, by inspection of the artifacts, how any artifact relates to the intent it serves and to the design and verification that depend on it, so the chain from intent to verification is legible without recourse to a tool.

## Source

See the Source of [Trust and drift visibility](../../needs/trust-intent-is-honored.md){id=note:need:46tkxcn}.

## Rationale

Intent loss compounds silently across the chain from intent to verification when the relationships are not legible.

A reader must be able to see, from the files, how an artifact relates to the intent it serves and to what depends on it, rather than reconstructing those links by guesswork.

This requirement states the legibility property and leaves how relationships are represented and computed to specification;
the separate obligation that staleness and divergence surface by inspection is stated in [Detectable drift](detectable-drift.md){id=note:req:d6m4q7z}.

## Relations

- addresses: [Trust and drift visibility](../../needs/trust-intent-is-honored.md){id=note:need:46tkxcn}
- delivers: [A Condition You Can Point To at Audit](../../offerings/acceptance-up-front/gc-a-condition-you-can-point-to-at-audit.md){id=note:gc:442jkxj}
- delivers: [A Condition the Trace Runs Through](../../offerings/acceptance-up-front/pr-condition-the-trace-runs-through.md){id=note:pr:m50rd6p}
- delivers: [Trace the Chain from the Files Alone](../../offerings/trust-by-inspection/gc-traceability-by-inspection.md){id=note:gc:mfb8amr}
- delivers: [Checks Tied to Obligations](../../offerings/trust-by-inspection/pr-checks-tied-to-obligations.md){id=note:pr:39wh9k2}
