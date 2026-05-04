---
id: note:req:p2w8j5q
name: Computable citing units of an artifact
kind: requirement
level: system
type: functional
status: current
---

Note shall ensure that, from an artifact, the units outside the corpus that cite it, the files and the commits carrying its durable identifier, are computable from the files as a derived view.

## Rationale

The forward citation resolves from a citing unit to the artifact it names ([In-code citation of intent](in-code-citation-of-intent.md){id=note:req:cffvvdz}; [Commit-message citation of intent](commit-message-citation-of-intent.md){id=note:req:cm7vq3x}).

The reverse question, from an artifact which units cite it, is what a reader asks to see what depends on an obligation before changing it, and what an auditor asks to find the changes that claim to realize an intent.

This is the inverse of an authored citation, and an inverse is a derived view, never authored, computed from the citations already present in the files ([Inspectable traceability](../stakeholder/inspectable-traceability.md){id=note:req:sg0npmv}).

It reaches across the corpus boundary because the citations do: a citation lives in a source file or a commit message outside the corpus, so the units it gathers are those files and commits, not corpus artifacts.

This requirement obliges the reverse view be computable; how it is computed and presented is specification.

Computing the view is reporting, not deciding: it surfaces what cites an artifact and judges nothing, consistent with the System computing and reporting a derived view ([Representation, not enforcement](representation-not-enforcement.md){id=note:req:agncpcc}).

## Relations

- derivedFrom: [Inspectable traceability](../stakeholder/inspectable-traceability.md){id=note:req:sg0npmv}
