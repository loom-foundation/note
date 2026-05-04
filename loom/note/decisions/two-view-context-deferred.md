---
id: note:dec:ctx2vw7
name: The two-view Context split is deferred until wanted
kind: decision
status: current
decided: 2026-07-02T10:44:22Z
---

The split of a Context into a business view and a technical view is no longer profile-gated: it is deferred until an adopter wants it, and it arrives then as a manifest or scope-level opt-in.
This amends the Context model, whose gate named a profile no profile carries.

## Context

The [Context model](context-model.md){id=note:dec:b7w3k9n} made a single boundary statement the default and gated the business-and-technical split behind a profile opt-in.
No profile (bare, standard, strict) carries that knob: the profiles are rigor bundles, fixed as such, and a presentation split is not rigor, so the gate pointed at a carrier that does not exist and an adopter wanting the split had nothing to declare.

## Decision

- The two-view split is deferred, explicitly, until an adopter wants it; no profile gates it.
- When taken up, it arrives as a manifest or scope-level opt-in, specified in the substrate's manifest section then, not now.
- The single boundary statement remains the default and the dogfooding corpus keeps its one Context.

## Forces and trade-offs

Deferral costs the split's would-be adopter a wait it cannot shorten by declaring anything.
Accepted: no such adopter exists yet, the phantom gate cost every reader comprehension now, and parking the knob in the profiles would have made the strictest corpora split their Contexts whether or not two audiences exist.

## Alternatives considered

- **Name `strict` as the carrying profile.**
  Rejected: profiles bundle rigor, and a two-audience presentation choice is orthogonal to rigor; coupling them taxes strict corpora with ceremony their audiences may not need.
- **Specify the manifest opt-in now.**
  Rejected: surface authored ahead of any adopter wanting it, against Proportionality and Earned Substance.

## Driven by

- amends: [Context model](context-model.md){id=note:dec:b7w3k9n}
- groundedIn: [Conformance profiles as pure rigor bundles](conformance-profiles.md){id=note:dec:cf7n2wq}
- groundedIn: [Proportionality](../principles/proportionality.md){id=note:principle:es0vhzn}
