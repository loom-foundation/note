---
id: note:req:cm7vq3x
name: Commit-message citation of intent
kind: requirement
level: system
type: functional
status: current
---

Note shall define a citation form by which a commit message references the intent a change realizes, by that artifact's durable identifier, recognizable and resolvable by inspection, so that the commit's reliance on that artifact is subject to staleness detection.

## Rationale

A commit records a change to a body of work, and the question it answers is which change realized which intent: distinct from the in-code comment's question of what governs a unit of implementation now ([In-code citation of intent](in-code-citation-of-intent.md){id=note:req:cffvvdz}).

A commit is the immutable, signable record an auditor trusts as evidence: a comment can be typed by anyone and revised silently, where a commit, once made, is fixed in history and attributable.

So the citation an auditor relies on to trace a change back to the intent it realizes belongs in the commit message, where it cannot later be edited away from the change it describes.

A commit message lives outside the corpus, where the relation-link form a corpus artifact uses cannot apply: a relative path across the corpus boundary is meaningless and does not self-heal, so the durable handle is what such a reference can carry ([Stable, location-independent identity](stable-identity.md){id=note:req:sfmkwmm}, which already anticipates a reference travelling in a commit message).

Once a commit message carries a recognizable, resolvable reference, that reference is a relationship a checker can read, and the commit's reliance becomes subject to the same detection a referenced artifact's text moving already triggers ([Detectable staleness](detectable-staleness.md){id=note:req:46xm59a}).

This requirement obliges that the form exist and be recognizable and resolvable by inspection; the concrete citation grammar, and the recognizer a checker uses, are specification.

Whether such a check runs, and by whom, belongs to the Orchestrating Authority; Note represents the reference and computes over it, and reaches no further.

## Relations

- derivedFrom: [Implementation traceable to intent](../stakeholder/implementation-traceable-to-intent.md){id=note:req:m520064}
- addresses: [Trace Behavior to Intent](../../needs/trust-intent-is-honored/job-trace-behavior-to-intent.md){id=note:job:4pw4tqd}
