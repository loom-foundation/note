---
id: note:dec:eym5t5g
name: Principles as a first-class kind
kind: decision
status: current
decided: 2026-06-12T00:00:00Z
---

A principle is a first-class artifact kind: a named, weighted commitment that guides judgment across the corpus, carrying the uniform opaque identity every kind shares and cited by its designation.
It is a transverse normative anchor, not a node on the need-to-requirement spine: a requirement or a convention names the principle it `enacts`, the inverse `enactedBy` a derived view, and a specification reaches a principle transitively through the requirement it satisfies.
A principle is adopted to mitigate a risk or realize a gain the corpus cares about, and in doing so it guides judgment where no specific rule yet bears.

## Context

A sustained body of work accumulates a small set of foundational commitments that guide judgment where no specific rule yet bears, and from which a class of obligations follows.
The work may be a software system, a hardware product, a process, or a methodology like this corpus, and a principle plays the same role in each.

Each such commitment is adopted to mitigate a named risk or realize a named gain, and it is the single home for a recurring rationale that the requirements, conventions, and decisions describing the work would otherwise re-derive, with drift, across the artifacts that share it.

A commitment of that kind is, distinct from its neighbors, a weighted value balanced against others: Dworkin's principle rather than his rule.
It is not a single obligation satisfied or violated with no middle, which is a requirement or a convention; not a persona's problem, which is a need; and not a single recorded choice, which is a decision.
It is the positive value those others rest on.

For a commitment to play that role, an obligation must be able to name it, and its coverage must be checkable.
A value an obligation can cite is one that can be reported as enacted by nothing once the corpus has stopped enacting it, so a dead commitment can be pruned rather than left to mislead.
A rationale that lives only as prose has no identity to name, no inverse to compute, and nothing to prune against.

## Decision

- **A principle is a first-class artifact kind.**
  A named, weighted commitment that guides judgment and grounds a class of obligations across the corpus.

- **Uniform opaque identity.**
  Its id is the opaque grammar every kind shares (`note:principle:yecemfe` for Earned Substance), defined once in [Uniform opaque identity](identity-and-designations.md){id=note:dec:jhgkwja}.
  A principle's name is one label among several for the commitment ("Single Source of Truth", "SSOT", and "No Duplication of Content" name the same one), so the designation lives in `name` and `aliases` while the id stays fixed, and a rename strands no citation held in an immutable surface such as a commit trailer.

- **Transverse anchor, not a spine node.**
  A principle is not derived from a need and does not obligate the product.
  It is an orthogonal normative anchor that requirements, conventions, and decisions align with and cite.

- **Purpose: mitigate a risk or realize a gain.**
  A principle is adopted because it mitigates a risk (Single Source of Truth mitigates drift) or realizes a gain, and in doing so it grounds a class of obligations and guides judgment where no specific rule yet bears.
  Its `## Why this matters` records that risk or gain.

- **The `enacts` relation, sourced from requirement and convention only.**
  A requirement or a convention names the principle it `enacts`, authored on that dependent end; the inverse `enactedBy` is a derived view, never authored.
  A specification carries no `enacts`: it reaches a principle transitively, through the requirement it satisfies, so the principle a design serves is read along the satisfy edge rather than restated on the specification.
  A decision expresses its alignment through its own `## Driven by`.
  The relation is advisory and its coverage is asymmetric: a principle that no obligation enacts and that grounds no decision is a candidate for pruning, a value the corpus no longer references, while an obligation that enacts no principle is information, not a defect.

- **Body.**
  A principle carries a lead statement, then `## Why this matters` (the rationale and the risk it mitigates or gain it realizes), `## How to apply` (the litmus and guidance), a recommended `## Considered alternative`, an optional `## Relations`, and a profile-gated `## Origin`.
  This mirrors the established architecture-principle template, Name, Statement, Rationale, Implications (TOGAF), with an added Origin.

- **Principles cascade as obligations.**
  A principle inherits across the scope graph through the same three operators every obligation-shaped kind uses: an `add` is the safe, silent strengthening, and a `replace` or `disinherit` is the loud, attributable, rationale-bearing deviation ([Scope and cascade](../specifications/note/scope-and-cascade.md){id=note:spec:1r673tc}).

- **Rides the spine pack.**
  The principle kind is part of the spine pack, the default set a corpus carries when it configures nothing, so the kind is available wherever the spine is enabled.
  The typed `enacts` relation discipline, authored on the dependent end and checked, is what the strict rigor profile expects; kind availability is the pack axis, and rigor is the profile axis, kept apart.

- **Out of scope, separate threads.**
  The typed pairing of a principle to the risk it mitigates, and the question of promoting an external document or policy to an artifact, are independent threads, not settled here.

## Forces and trade-offs

A new kind must earn its place, and Earned Substance sets the bar higher for adding than for not adding.
A principle clears it: an obligation references it, it is the single source a recurring rationale is restated from, and its coverage is checkable the moment the `enacts` relation is typed.
The cost is one more kind; the return is a durable identity for a citation that would otherwise break on a move, and a coverage signal for a value the corpus has quietly stopped enacting.

Treating a principle as a transverse anchor rather than a spine node introduces a second class of first-class artifact, spine versus anchor, a modeling subtlety the corpus had to name.
It is bought back by honesty: a principle is cited and balanced, not derived, and forcing it onto the spine would misrepresent it.

Narrowing the `enacts` sources to requirement and convention, and reading a specification's principle along its satisfy edge, keeps the relation authored exactly once on the nearest obligation: a design that satisfies a requirement inherits the requirement's principle rather than re-asserting it, so the same value is not stated twice on two ends of one chain.

Opaque identity means a rename never re-mints: the designation is rewritten freely in `name` and every reference's link text refreshes against it while the id stays fixed.

## Alternatives considered

- **Keep `realizes` as the verb (the architecture-modeling reuse).**
  Rejected: established-vocabulary-first sets a burden of proof on any coinage, and discharging it here favors `enacts`.
  The established `realizes` carries UML interface-implementation baggage and collides conceptually with the value layer's delivers-and-creates family, so the same verb would read two ways in one corpus.
  `enacts` (Oxford: to put into practice, to make into law) is the more precise dictionary fit for putting a principle into practice, and reading true is what the relation grammar asks of a verb, so the coinage earns its place against the canonical reuse.

- **Keep principles as prose under `meta/`.**
  Rejected: a prose principle has no durable identity for an obligation to name, so the relation cannot be typed or checked and a citation breaks on a move.
  The value a corpus pays the kind for, a stable citation and a checkable coverage signal, is exactly what prose cannot give.

- **A readable slug id, the prior word-is-the-thing scheme.**
  Rejected: a principle is cited by its designation, but the designation is a label for the commitment rather than the thing itself, so a slug records today's label and lies on a rename, stranding citations in artifacts that cannot be edited.
  A principle carries the uniform opaque id, the designation held in `name`.

- **Source `enacts` from specifications too.**
  Rejected: a specification reaches its principle through the requirement it satisfies, so authoring `enacts` on the specification as well would state one value twice along a single chain, against Single Source of Truth.

- **A first-class kind on the derivation spine.**
  Rejected: a principle is not derived from a need and does not obligate the product; placing it on the spine misrepresents its role.

- **A `Value` layer above principle, the Agile values-over-principles split.**
  Rejected against Earned Substance: a second layer earns nothing unless a corpus genuinely derives its principles from a smaller set of higher values, which is not the case here.

## Driven by

- groundedIn: [Reuse established vocabulary before coining new terms](established-vocabulary-first.md){id=note:dec:8f3m5vk}
- groundedIn: [Kind-agnostic substrate and kind packages](substrate-and-kind-packages.md){id=note:dec:w4awceq}
- groundedIn: [Uniform opaque identity](identity-and-designations.md){id=note:dec:jhgkwja}
- groundedIn: [Trust and drift visibility](../needs/trust-intent-is-honored.md){id=note:need:46tkxcn}
- groundedIn: [Single Source of Truth](../principles/single-source-of-truth.md){id=note:principle:8691937}
- groundedIn: [Earned Substance](../principles/earned-substance.md){id=note:principle:yecemfe}

## Worked example

Single Source of Truth is `note:principle:8691937`, an artifact under `principles/`.

Its `## Why this matters` records the risk it mitigates: drift between divergent copies of one fact.

A system requirement that enacts it, [Typed, checkable relations](../requirements/system/typed-relations.md){id=note:req:yb1xez2}, which obliges a single authored home for each relation, names the principle:

```
## Relations

- enacts: [Single Source of Truth](../principles/single-source-of-truth.md){id=note:principle:8691937}
```

The inverse, the set of obligations that enact Single Source of Truth, is a derived view.
If that set is ever empty, the principle is enacted by nothing and becomes a candidate for pruning, the falsifiable anti-rot signal a first-class principle buys that a prose paragraph cannot.
