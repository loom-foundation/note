---
id: note:dec:vg3k34n
name: Kind templates
kind: decision
status: current
decided: 2026-06-10T05:50:54Z
---

Note provides a per-kind authoring template for every artifact kind, generated as a derived view of the file-format specification rather than hand-authored, and hosted in a generated `templates/` directory at the corpus root, so any consumer starts a new artifact from one canonical, ready-to-fill scaffold without keeping a copy of each kind's shape that drifts from the spec.

## Context

The normative shape of every kind, its frontmatter and its body sections in order, is already fixed once, in the common-frontmatter and relation machinery of [The substrate](../specifications/note/substrate.md){id=note:spec:tkhd63e} and the per-kind body-structure tables of [The spine pack](../specifications/note/spine-pack.md){id=note:spec:6kjja5r} and [The discovery pack](../specifications/note/discovery-pack.md){id=note:spec:w6nsgt1}.

That specification is the single source of truth for what each kind looks like.

Authoring from that specification, though, means reading a schema and reconstructing the skeleton by hand every time.

A ready-to-fill template, the frontmatter keys with placeholders, the required section headings in canonical order, and brief fill-in guidance, is a faster and less error-prone starting point, and more than one consumer wants one: a tool that assists authoring, an editor offering per-kind snippets, an agent scaffolding a new file, a person starting from a blank file.

The open question is whether Note should provide such templates, and if so how, without creating a second statement of each kind's shape that drifts from the specification the moment either changes.

## Decision

- **Note provides one authoring template per kind.**
  Each is a scaffold: the kind's frontmatter with placeholders, its required body sections in canonical order, and short fill-in guidance.
- **A template is a derived view of the specification, not authored content.**
  The single source of truth for a kind's shape remains the file-format specification; a template is generated from it and never maintained alongside it, because two statements of one fact drift (Single Source of Truth, Earned Substance).
- **A template is not a first-class artifact.**
  It carries no durable identifier and no `kind`; it is generated output, like a rendered view, not a unit of intent.
- **Templates live in a generated `templates/` directory at the package root**, beside `docs/` and `meta/`, and never under the layer root, which holds authored intent only.
  The directory is marked generated and is regenerated whenever the specification changes, so it cannot fall out of step with the schema it projects.
- **Consumers derive from this one canonical set** rather than each carrying its own copy.
  A reference tool that assists authoring, such as Sett, reads these templates rather than reconstructing the schema independently.
- **The template format and the generation mechanism are specification and tooling**, not fixed here.

## Forces and trade-offs

- Generating templates rather than authoring them keeps a single source of truth: the specification defines a kind once and the template is a projection that cannot disagree.
  The cost is that a template is build output rather than a hand-editable file; that cost is the point, since a hand-editable template is exactly the second source that drifts.
- Hosting the templates in Note, rather than leaving each consumer to derive its own, gives every consumer one canonical scaffold set and removes the divergence that appears when several copies are maintained independently.
  The cost is that the repository carries generated output, bounded by placing it in one clearly-marked generated directory outside the layer root, the same separation the corpus already draws between authored intent and derived views.
- Recording the decision before the generator exists leaves the `templates/` directory empty until the tooling lands.
  Accepted: settling that templates are a generated projection of the spec, owned by Note, is worth doing now so consumers are built against that model rather than against ad-hoc copies.

## Alternatives considered

- **Provide no templates; every consumer reads the specification.**
  Rejected: it leaves each consumer to reconstruct each kind's skeleton, and in practice each then keeps its own hand-made templates, which drift from the specification independently, the precise failure this decision prevents.
- **Hand-author a template set in Note.**
  Rejected against Single Source of Truth and Earned Substance: a hand-maintained template restates each kind's shape, creating a second canonical source that drifts from the specification the moment either side changes.
- **Place the templates under the layer root.**
  Rejected: the layer root holds authored intent, and a generated projection is not intent; mixing the two blurs what is authored and what is derived.
- **Make a template a first-class artifact with an identifier and a kind.**
  Rejected against Earned Substance: nothing references a template as an entity, so the identity buys nothing; it is generated output, not a unit of intent.

## Driven by

- groundedIn: [Single Source of Truth](../principles/single-source-of-truth.md){id=note:principle:8691937}
- groundedIn: [Earned Substance](../principles/earned-substance.md){id=note:principle:yecemfe}
