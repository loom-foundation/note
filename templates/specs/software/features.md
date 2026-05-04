---
id: <namespace>:spec:<opaque>
name: <Name>
kind: specification
status: draft
authority:
  - contracts/features/<feature>.feature
---

This specification identifies the behavioral contract for <capability>, expressed as executable Gherkin scenarios.

## Authority

The behavioral contract is held in a Gherkin file (Cucumber dialect, version 6 or later) at the path declared in `authority`.
The external file governs on any divergence between it and this document.
An implementation's conformance to the scenarios is a separate Verification; it is not asserted here.

The `Rule` keyword is required for grouping scenarios under the business rule they validate.
`Scenario Outline` with `Examples` tables is the prescribed form for combinatorial cases.
Every `Feature` block carries a plain-English description of the user-facing capability.
Every `Rule` block states the business rule it validates, not a technical condition.

## Relations

- satisfies: [<Requirement>](../../requirements/system/<requirement>.md){id=<namespace>:req:<opaque>}
