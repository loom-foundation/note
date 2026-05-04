---
id: note:req:cffvvdz
name: In-code citation of intent
kind: requirement
level: system
type: functional
status: current
---

Note shall define a citation form by which a file outside the corpus references an artifact by its durable identifier, recognizable and resolvable by inspection, so that the citing file's reliance on that artifact is subject to staleness detection.

## Rationale

A unit of implementation lives outside the corpus, where the relation-link form a corpus artifact uses cannot apply: a relative path across the corpus boundary is meaningless and does not self-heal, so the durable handle is what a cross-file reference can carry.

A durable, location-independent handle is what makes such a reference possible: it survives the artifact being moved, renamed, or revised, so a reference written once in a far-off file still resolves ([Stable, location-independent identity](stable-identity.md){id=note:req:sfmkwmm}).

Once a file outside the corpus carries a recognizable, resolvable reference, that reference is a relationship a checker can read, and the citing file's reliance becomes subject to the same detection a referenced artifact's text moving already triggers ([Detectable staleness](detectable-staleness.md){id=note:req:46xm59a}).

This requirement obliges that the form exist and be recognizable and resolvable by inspection; the concrete citation grammar, and the recognizer a checker uses, are specification.

Whether such a check runs, and by whom, belongs to the Orchestrating Authority; Note represents the reference and computes over it, and reaches no further.

## Relations

- derivedFrom: [Implementation traceable to intent](../stakeholder/implementation-traceable-to-intent.md){id=note:req:m520064}
