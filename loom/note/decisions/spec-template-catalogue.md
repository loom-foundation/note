---
id: note:dec:tmp8cat
name: The authored spec-template catalogue
kind: decision
status: current
decided: 2026-07-02T12:02:33Z
---

`templates/specs/` hosts an authored, optional catalogue of domain specification templates: copy-paste starting points a software adopter fills in, mints an id for, and owns.
It is distinct from the generated per-kind scaffolds the kind-templates decision reserves, and this decision is its record; the generated reservation narrows to the per-kind set.

## Context

[Kind templates](kind-templates.md){id=note:dec:vg3k34n} fixed `templates/` as a generated directory, a projection of the file-format specification, empty until tooling lands.
The tree then gained twenty hand-authored specification templates under `templates/specs/`, with a README that distinguishes itself from that decision, carries a two-tier authority model and a domain catalogue, and was covered by no decision of its own.
The readiness review flagged the contradiction; the owner's call is to keep the catalogue and decide it in.

## Decision

- **`templates/specs/` is authored content.**
  Domain templates and their README are convenience documentation: no durable ids, no `kind`, not units of intent, copied out and owned by the adopter.
- **The generated reservation narrows to the per-kind scaffolds.**
  The root of `templates/` remains reserved for the generated per-kind set, still empty until the tooling lands, exactly as the kind-templates decision fixed; the two live side by side without contradiction.
- **The catalogue restates, never governs.**
  Its authority model (independently validated against a machine-readable contract, or review-gated house prose) is commentary on the `authority` field whose rules stay canonical in the spine pack and the specification-authority decision; on divergence the canonical homes win and the catalogue is corrected.
- **The catalogue is domain convenience, not method surface.**
  It is software-first by design; an effort specifying hardware, a process, or a methodology ignores it and writes its own, and no conformance rule ever references it.

## Forces and trade-offs

Carrying authored templates costs a drift surface: twenty files that could fall out of step with the spec-authoring rules they embody.
Accepted: each template carries a real domain's authority pattern (which contract governs, what stays house prose), which a generated projection of kind shape cannot carry, and the README routes every governing rule back to its canonical home.

The kind-templates decision rejected hand-authoring as a restatement of kind shape; the catalogue is not that.
It restates no kind's frontmatter or section order, so the single-source argument that killed hand-authored kind templates does not apply to it.

## Alternatives considered

- **Delete the catalogue pre-release.**
  Rejected by the owner: it is real, wanted work; the defect was the missing record, not the content.
- **Move it out of the corpus package.**
  Rejected: it serves adopters of this method and travels correctly with the package's documentation; a separate home would orphan it from the specs it teaches.
- **Make each template a first-class artifact.**
  Rejected for the same reason the kind-templates decision gave: nothing cites a template as an entity, so identity buys nothing.

## Driven by

- amends: [Kind templates](kind-templates.md){id=note:dec:vg3k34n}
- groundedIn: [Earned Substance](../principles/earned-substance.md){id=note:principle:yecemfe}
- groundedIn: [Proportionality](../principles/proportionality.md){id=note:principle:es0vhzn}
