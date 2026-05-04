---
id: note:req:kdtc9a8
name: Method-defined deterministic context subset
kind: requirement
level: system
type: functional
status: current
---

Note shall ensure that the subset of the corpus relevant to a given artifact and a stated purpose is deterministically derivable from the committed artifacts alone, by a definition the method fixes rather than each tool, so that independent actors deriving the subset for the same artifact and purpose obtain the same subset and what an actor reads is auditable from the corpus.

## Rationale

The companion requirement [Finely addressable intent](finely-addressable-intent.md){id=note:req:fd8k2w4} keeps intent decomposed into independently addressable units and leaves how a subset is computed and delivered to the tool.
This requirement is its complement: it fixes that the *definition* of the relevant subset, which artifacts belong in it for a given artifact and purpose, is the method's, so that delivery remaining the tool's concern does not make the subset itself tool-dependent.
The division is clean: one requirement holds the corpus decomposed and addressable; this one holds the boundary of a relevant subset reproducible and auditable from the files.

Determinism is what lets two actors, or the same actor twice, derive the identical subset for one artifact and purpose, and it is what lets a reviewer check after the fact that an actor read what the method says it should and no more.
Both properties fail at a tool boundary: if each tool defined its own subset, the boundary would vary by implementation and could not be reconstructed from the corpus.

The per-purpose closure rules are specification: which relations are followed for which purpose (implement, verify, review, author) is fixed downstream, not here.
This requirement obliges only that such a definition exist, belong to the method, and yield a deterministic, corpus-derivable subset.

## Relations

- derivedFrom: [Intent retrievable in relevant subsets](../stakeholder/intent-retrievable-in-subsets.md){id=note:req:rt3kw9n}
- delivers: [Context You Can Audit](../../offerings/right-sized-context/gc-context-you-can-audit.md){id=note:gc:x0d9ap2}
- delivers: [Committed Context Only](../../offerings/right-sized-context/pr-committed-context-only.md){id=note:pr:4wekpp6}
