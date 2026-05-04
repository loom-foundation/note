---
id: note:dec:td3jw2y
name: Typed decision edges
kind: decision
status: current
decided: 2026-06-12T00:00:00Z
---

A decision relates to the rest of the corpus through typed, checkable edges rather than a free-phrased prose list.
A decision authors two edges on its own end: `groundedIn`, naming a need, requirement, decision, or principle it rests on or is justified by, and `amends`, naming a still-current prior decision it modifies in place.
The reverse relationship, that a decision determined the content of a requirement, specification, or convention, is authored on that artifact as `decidedBy` (inverse `decides`), not on the decision.
The decision graph carries only these endpoints; a relationship to any other kind is prose, not a typed edge.

## Context

The decision is the densest relationship in the corpus: a recorded choice rests on needs and requirements, builds on prior decisions, honors principles, and shapes the obligations and designs that follow it.
That density was carried in a `## Driven by` section written as free prose, each line a sentence ("rests on", "serves", "shapes", "honors") that a reader could follow but a checker could not.
The corpus's other relationships are typed, authored once on the dependent end, with derived inverses; the decision's were the one dense relationship left unchecked.

Typing them exposes two questions the prose hid.
First, direction: some lines name an artifact the decision rests on, and others name an artifact the decision shaped, which are opposite directions and, under the authored-once rule, belong on opposite ends.
Second, range: the prose named targets of every kind, including terms and facets a decision merely refines in passing and specifications a decision determines, so the endpoint set has to say which of these are decision edges and which are prose.

## Decision

- **`groundedIn`: a decision rests on its justification.**
  Authored on the decision, `groundedIn` names a need, requirement, decision, or principle that justifies or constrains the choice.
  Its inverse is `grounds`, a derived view.
  This one edge carries every "rests on", "relies on", "serves", and "honors" the prose drew: a decision resting on a prior decision's machinery, or honoring a principle as its justification, is `groundedIn` that decision or principle.

- **`amends`: a decision modifies a still-current decision in place.**
  Authored on the amending decision, `amends` names a still-current prior decision whose content this one modifies in place.
  Its inverse is `amendedBy`, a derived view.
  It is reserved for genuine in-place modification and is distinct from `supersedes`, which retires a decision wholesale and is frontmatter, not a relation.

- **`decidedBy`: an obligation, design, or rule names the decision that determined it.**
  When a decision determines the content of a requirement, a specification, or a convention, that relationship is authored on the requirement, specification, or convention as `decidedBy`, naming the decision; its inverse is `decides`, a derived view.
  It is authored on the determined artifact, never on the decision, because that artifact is the dependent end: it is the thing the decision shaped.
  `decidedBy` reaches a decision from a requirement, a specification, or a convention, the three kinds whose content a decision fixes.

- **The decision graph is closed over these endpoints.**
  A decision's typed edges target only needs, requirements, decisions, and principles (through `groundedIn` and `amends`).
  A relationship from a decision to a kind outside that set is not a typed edge.
  A decision that refines a term's recorded attribute, or that touches a single facet, states that in its prose where it bears; it does not author a typed edge to a term, a facet, or any other kind.
  A decision's relationship to a specification is carried by the specification's `decidedBy`, so it too is never an edge on the decision.

- **`shapes` is retired from the decision graph.**
  The loose `shapes` verb, which pointed from a decision at an artifact it influenced, is removed.
  Its meaning is carried by `decidedBy` authored on the shaped artifact, in the correct direction.

- **`## Driven by` is the typed list.**
  A decision's `## Driven by` section is a bullet list of its `groundedIn` and `amends` edges, one per line, each in the reference-link form carrying the target id.
  Prose that names no typed edge, a deferral to a later specification, a clarifying contrast, does not belong in the typed list; it lives in the decision's body where it bears.

## Forces and trade-offs

Typing the densest relationship makes the decision graph checkable: every edge resolves to a real artifact of a legal kind, and the inverse views (what grounds a need, what a decision amends, what a decision decides) are computed rather than hand-maintained.
The cost is that the corpus's existing free-phrased Driven-by sections are retyped, each line classified to an edge and direction, with the reverse-direction lines moving to `decidedBy` on the artifact they shaped.

Holding `groundedIn` to four target kinds keeps the decision graph the spine-and-rationale graph it is, rather than letting it sprawl to every kind a decision mentions.
A decision that genuinely rests on a term's definition, or that turns on one facet, loses nothing: the relationship is real but it is rationale, and it reads as prose in the body, which is where rationale already lives.

## Alternatives considered

- **Keep the narrow endpoints first proposed (`groundedIn` to need or requirement only; `decidedBy` from requirement only).**
  Rejected: counted against the corpus, that endpoint set cannot carry the decision-to-decision and decision-to-principle relationships the existing records already hold, nor the specifications and conventions a decision determines, so the retyping would stall on the first dozen records.
  `groundedIn` widens to include decision and principle; `decidedBy` widens to include specification and convention.

- **Keep `## Driven by` as free prose.**
  Rejected: it leaves the corpus's densest relationship the one relationship a checker cannot follow, so an inverse view of what a decision grounds or amends cannot be computed and a citation of a retired artifact cannot be caught.

- **Admit a typed decision edge to terms, facets, and any other kind a decision mentions.**
  Rejected against Earned Substance: most such mentions are rationale, not dependency, and admitting them turns the decision graph into a record of every passing reference, diluting the edges that carry the spine.

## Driven by

- groundedIn: [Typed, checkable relations](../requirements/system/typed-relations.md){id=note:req:yb1xez2}
- groundedIn: [Single authoritative representation per relationship](../requirements/system/single-authoritative-relation.md){id=note:req:s5fh0e8}
- groundedIn: [Single Source of Truth](../principles/single-source-of-truth.md){id=note:principle:8691937}
- groundedIn: [Compute and Report](../principles/compute-and-report.md){id=note:principle:6e7f28k}
- groundedIn: [Earned Substance](../principles/earned-substance.md){id=note:principle:yecemfe}
