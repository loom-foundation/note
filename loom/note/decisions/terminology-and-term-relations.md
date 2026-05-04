---
id: note:dec:s9k4w7n
name: Terminology with typed term-relations
kind: decision
status: current
decided: 2026-06-12T00:00:00Z
---

Note's controlled vocabulary keeps the name "terminology" and carries typed relationships between terms, drawn from a closed, ISO 704-grounded set, authored once on the dependent end with the inverse and any diagram derived.
A term is referenced from another artifact by capitalization and closed-vocabulary lookup, with an explicit reference available where ambiguity earns the weight.
A term carries the uniform opaque identity every kind shares, and term lookup resolves a designation, a capitalized word, against the names and aliases of the terms and personas in force at the reading scope.

## Context

A load-bearing term is recorded once, with its definition and its relationships to other terms.
Two questions follow: how the relationships between terms are typed and kept from drifting, and how a term is referenced and resolved from inside a need or a requirement.

The relationships between terms are the substance the terminology tradition the method rests on already names.
ISO 704 and ISO 1087 give the generic, partitive, and associative concept relations, and a relationship held in two places, a hand-drawn diagram and the prose beside it, drifts with no authoritative side to adjudicate.
Authoring each relationship once and deriving the rest is the single-source-of-truth discipline applied to the term graph.

A term's identity is not a separate scheme.
Every kind, term included, uses one opaque identity grammar with no exception, defined once in [Uniform opaque identity](identity-and-designations.md){id=note:dec:jhgkwja}.
A term is the clearest case the terminology tradition makes for that grammar: a concept and the word that designates it are two things, so a term carries an opaque id and a `name` holding its designation, and replacing a designation with a synonym is ordinary terminology work that leaves the id untouched.

## Decision

- **The capability keeps the name "terminology".**
  The word "ontology" is not adopted: it implies the OWL, RDF, and SHACL stack, overstates the formality, and is already a competing tool's framing.
  "Concept system" (ISO 704) names the structure in prose where one is needed; an ontology or SKOS form survives only as an optional downstream export, never the source.

- **Relationships between terms are typed from a closed set.**
  The set is grounded in ISO 704's concept relations: `is a` (generic), `is part of` (partitive), `carries`, `scopes`, `contrasts with`, `is a value of`, and `relates to` (associative), alongside the structural verbs the substrate already defines, reused where they read true between terms.
  A hierarchical relation (`is a`, `is part of`) is acyclic.

- **Each relationship is authored once, on the dependent end.**
  The inverse and any per-cluster diagram are derived views, reconciled by a check, never authored separately.
  This is the single-authoritative-representation rule lifted from artifact relations to the term graph.

- **A term is referenced in three ways.**
  Capitalization invokes the defined sense; the closed vocabulary makes "is this a defined term?" a lookup for humans, agents, and tools; and an explicit reference, the same form used to cite any artifact, is available where a collision or ambiguity makes it worth the weight.

- **A term carries uniform opaque identity.**
  A term's id is the opaque grammar every kind shares; no slug id exists.
  The term's designation lives in its `name` field, with further designations in `aliases`, and a rename leaves the id untouched and strands no citation held in an immutable surface such as a commit trailer.

- **Term lookup resolves a designation.**
  A capitalized word in prose is a designation, resolved against the names and aliases of the terms and personas in force at the reading scope, the closed-vocabulary lookup reading a set of designations rather than a single frozen slug.
  An ambiguous designation in the effective set is surfaced like a cascade tie.

## Forces and trade-offs

Developing Note's own typed-term-relations on the substrate's existing relation machinery, rather than adopting a formal ontology, keeps the no-special-tool floor and manual parity: a term and its relations are legible and checkable by an unaided reader of one file, and no unused inference is bought.
The cost is no off-the-shelf reasoner, which Note does not want.

Resolving a term by designation rather than by a frozen slug is what lets the word a term is cited by change without breaking the citation.
The designation lives in `name` and `aliases`, where it is rewritten freely; the reference carries the opaque id, so a synonym swap, the ordinary terminology move, costs nothing downstream.

Authoring each relationship once and deriving the diagram removes the diagram-versus-prose drift; the cost is that the diagram is generated rather than hand-drawn, which is the intended outcome.

## Alternatives considered

- **Adopt a formal ontology (RDF, OWL, and SHACL via a triplestore), as a competing tool does.**
  Rejected: it breaks the no-special-tool floor and manual parity, and buys open-world inference Note does not use; the typed relations Note wants live at the thesaurus level, not the formal-ontology level.

- **Name the capability "ontology".**
  Rejected: it implies that stack, overstates the formality, and collides with a competing tool's framing.

- **A readable slug id for terms, on the reasoning that the word is the thing.**
  Rejected: it conflates a concept with its designation, against the ISO 704 and 1087 lineage this terminology rests on, and re-creates the rename-strands-citations failure for the kind that is renamed most readily.
  A term carries the uniform opaque id; the designation it is cited by lives in `name`, and lookup resolves the designation rather than a frozen slug.

- **Keep relationships in both the diagram and the prose.**
  Rejected: it is the double-authoring that drifts, the problem this decision removes.

## Driven by

- groundedIn: [Uniform opaque identity](identity-and-designations.md){id=note:dec:jhgkwja}
- groundedIn: [Reuse established vocabulary before coining new terms](established-vocabulary-first.md){id=note:dec:8f3m5vk}
- groundedIn: [Shared, specific term meaning](../needs/shared-term-meaning.md){id=note:need:w3k8n6p}
- groundedIn: [Stated-once, typed, checkable term-relations](../requirements/system/typed-term-relations.md){id=note:req:n8w4k6m}
- groundedIn: [Single authoritative term-relation](../requirements/system/single-authoritative-term-relation.md){id=note:req:k4w7n9t}
- groundedIn: [Single Source of Truth](../principles/single-source-of-truth.md){id=note:principle:8691937}
