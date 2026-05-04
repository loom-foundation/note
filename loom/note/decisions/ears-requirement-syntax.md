---
id: note:dec:p7k3w9n
name: EARS requirement syntax
kind: decision
status: current
decided: 2026-06-03T10:20:36Z
---

Note adopts the Easy Approach to Requirements Syntax (EARS) as the default, profile-selectable convention for constrained requirement phrasing, and Sett provides advisory quality scoring against it as a separate operation.

The method's obligation stays generic: it requires a constrained, checkable phrasing, not EARS specifically.

## Context

Requirements written in free natural language drift toward ambiguity and untestability, especially conditional obligations (on an event, a state, an unwanted situation, or an optional feature), which authors and agents tend to bury in prose.

Note already uses the obligation form ("shall"), which is the ubiquitous EARS pattern, but offers no form for the conditional cases.

EARS is a small, widely adopted set of five patterns that make the trigger and response explicit and machine-checkable; INCOSE and ISO/IEC/IEEE 29148 quality indicators address the broader ambiguity and testability defects, and tools such as DOORS and Jama score requirements against both.

## Decision

- The method obligation is generic ([Constrained, checkable obligation phrasing](../requirements/system/constrained-checkable-phrasing.md){id=note:req:m9w4k7p}): a requirement's obligation, including a conditional one, shall be expressible in a constrained, checkable form.
  The method is not wedded to one syntax.
- EARS is the default convention shipped as a profile: the five patterns (ubiquitous; event-driven WHEN; state-driven WHILE; unwanted-behavior IF-THEN; optional-feature WHERE).
  A profile selects it; the Conformance Core does not require it.
- Sett provides quality scoring against the declared convention and INCOSE-style indicators, its own requirement-quality-scoring requirement on the tool side, as a SEPARATE operation, not a sub-mode of corpus linting, because the inputs, determinism, continuous-integration cadence, and growth path differ.
- The scoring is ADVISORY: Sett reports the score and findings; gating on a low score is the adopter's concern, wired into their own hooks or pipeline.
  Sett does not gate.
- The need and the constrained-phrasing obligation are rooted on Note (the methodology); Sett inherits the scoring as a tool acceleration.

## Forces and trade-offs

- A generic obligation with EARS as a shipped profile, rather than EARS named in the obligation, keeps the method open to a better syntax later while still giving adopters a concrete, proven default today.
- A separate quality operation rather than folding scoring into linting keeps a deterministic graph check apart from a per-requirement, profile-sensitive, eventually model-assisted analysis that runs on a different cadence and grows into a family of checks; the cost is one more operation, accepted because the alternative is a later extraction that breaks adopters' pipelines.
- Advisory rather than gating keeps Sett compute-and-report and leaves the threshold with the adopter, who alone knows their bar; the cost is that Sett ships no enforcement, which is deliberate.

## Alternatives considered

- Mandate EARS as a schema in the Conformance Core.
  Rejected: it over-burdens a prototype and weds the method to one syntax, against proportionality.
- Name EARS directly in the requirement obligation.
  Rejected: it couples the obligation to a single convention; the generic obligation plus a shipped profile achieves the same default without the lock-in.
- Fold quality scoring into the linting operation.
  Rejected on the inputs, determinism, cadence, and growth grounds above.
- Let Sett gate on a low score.
  Rejected: gating is the adopter's, not the tool's; thresholds are contextual, and a non-deterministic check must never silently decide a merge.

## Driven by

- groundedIn: [Constrained, checkable obligation phrasing](../requirements/system/constrained-checkable-phrasing.md){id=note:req:m9w4k7p}
