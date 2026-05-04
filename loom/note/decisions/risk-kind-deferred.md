---
id: note:dec:ge1r86x
name: The risk kind
kind: decision
status: current
decided: 2026-06-12T00:00:00Z
---

The method defines a **risk** kind for a recorded threat to the work, with a closed **`treatment`** field whose value is one of `open`, `mitigating`, `mitigated`, `accepted`, `transferred`, or `avoided`; optional `likelihood` and `consequence` fields beside a coarse `exposure`; and the verb **`mitigates`**, authored from a requirement or a decision onto the risk it addresses (inverse `mitigatedBy`, derived).
The design is settled here, but the kind does not land in this version: it is in neither the spine pack nor the discovery pack, and it lands later as a small built-in pack or a spine addition when a corpus first needs it.

## Context

A sustained body of work, whether a software system, a hardware product, a process, or a methodology like this corpus, carries threats to its own success that are neither wants nor obligations nor recorded choices: a dependency that may not arrive, a regulation that may change, a capacity that may not hold.
A risk register is the established artifact for these, and its defining job is to show, for each threat, not just that it exists but what is being done about it.

The kind is genuinely useful, but its cost to land now is unearned against the kinds a corpus needs from the first day.
The deciding design question is the `treatment` field, and it turns on an audit distinction a risk register exists to make.
A model that rides a risk's openness on its lifecycle status plus the absence of an inbound edge cannot distinguish a consciously **accepted** risk, one a responsible party examined and chose to carry, from an unexamined **open** one, one no one has looked at yet.
Both would read as a live risk with no mitigation attached, yet they are opposite states: the first is a discharged decision, the second is an outstanding gap.
That is the exact distinction an auditor reads a register to find, and a regulated reviewer named its absence the single blocker to a pilot.
A closed `treatment` field records the distinction directly, so the design settles it now rather than shipping the gap later.

## Decision

- **A risk is a first-class kind, designed now.**
  A risk is a recorded threat to the work: an uncertain event or condition that, if it occurs, sets back a need, an obligation, or a design.
  Its id kind-segment and required frontmatter are fixed when the kind lands; the design below is the settled shape it lands as.

- **A closed `treatment` field.**
  Every risk carries a `treatment` field whose value is one of a closed set: `open` (recorded, not yet acted on), `mitigating` (a response is under way), `mitigated` (the response has reduced the exposure), `accepted` (a responsible party has examined the risk and chosen to carry it), `transferred` (the exposure has been moved to another party, by insurance or contract), and `avoided` (the work was changed so the risk no longer applies).
  The field is closed because its job is to make the consciously accepted risk legible as such, distinct from the unexamined open one, which a status-plus-edge model cannot do.

- **Optional `likelihood` and `consequence` beside a coarse `exposure`.**
  A risk may carry an optional `likelihood` and an optional `consequence`, the two factors a register weighs, and a coarse `exposure` that summarizes them.
  All three are optional: a corpus that wants only a flat list of threats and their treatment pays nothing for the finer grading, and a corpus that wants a graded register authors the factors it needs.

- **The verb `mitigates`.**
  A requirement or a decision reaches a risk through `mitigates`, authored on the requirement or the decision (the dependent end), naming the risk it addresses.
  Its inverse is `mitigatedBy`, a derived view, so a risk reads off the obligations and choices raised to answer it without authoring the edge twice.

- **The kind is deferred from this version.**
  The risk kind is not enabled in either built-in pack: it is absent from the spine pack and from the discovery pack, so no corpus on this version's defaults carries it.
  It lands later as a small built-in pack of its own, or as a spine addition, at the version where a corpus first needs a register.

## Forces and trade-offs

Deferring the kind is safe because landing it is purely additive: a new kind and a new verb, touching nothing that already exists.
No current kind's fields, sections, or relations change when risk arrives; no artifact authored against this version becomes ill-formed; the spine and discovery packs are unaffected.
The only cost of the deferral is that a corpus needing a register before the kind lands tracks its threats outside the model until then, which is the same position every adopter is in for any kind a later version adds.

Settling the design now, rather than deferring it undesigned, costs one decision record and buys the closed `treatment` field before the kind ships.
The alternative, leaving the openness distinction to a later design pass, risks shipping the status-plus-edge model whose audit gap is the precise failure a register exists to prevent; recording the resolution here forecloses that.

Holding the grading fields optional keeps the kind proportionate: a coarse list of threats with their treatment is a complete, useful register, and the likelihood-consequence-exposure machinery is earned only by a corpus that grades.

## Alternatives considered

- **Land the risk kind in this version.**
  Rejected against Earned Substance: a register is not a first-day need for most adopters, and the kinds a corpus cannot start without are the ones this version's packs carry; risk is a clean later addition with no cost to its absence, so it waits until a corpus earns it.

- **Defer the kind undesigned, settling its shape only when it lands.**
  Rejected: the `treatment` design turns on an audit distinction (accepted versus open) that is easy to miss under a status-plus-edge model and fatal to miss in a register, so the cheapest place to settle it is now, in the deferral record, before any later pass is tempted to ship the gap.

- **Ride a risk's openness on lifecycle status plus the absence of an inbound `mitigates` edge, with no `treatment` field.**
  Rejected: a status of current plus no mitigation reads identically for a consciously accepted risk and an unexamined open one, collapsing the exact distinction a register is read to find; the closed `treatment` field records it where status and edges cannot.

## Driven by

- groundedIn: [Kind-agnostic substrate and kind packages](substrate-and-kind-packages.md){id=note:dec:w4awceq}
- groundedIn: [Proportionality](../principles/proportionality.md){id=note:principle:es0vhzn}
- groundedIn: [Earned Substance](../principles/earned-substance.md){id=note:principle:yecemfe}
- groundedIn: [Compute and Report](../principles/compute-and-report.md){id=note:principle:6e7f28k}
