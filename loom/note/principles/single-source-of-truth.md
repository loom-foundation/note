---
id: note:principle:8691937
name: Single Source of Truth
kind: principle
status: current
altitude: authoring
---

Each fact lives in exactly one canonical location across the corpus.
Other locations cite by reference; they do not restate.

When duplication is detected, the corpus resolves to the single home and the duplicate is replaced with a cross-reference.

## Why this matters

Two copies of a fact will drift.
When they drift, readers have two contradictory canonical sources and no way to know which is current.

Cross-references are cheap to maintain; drift is expensive to discover, expensive to reconcile, and erodes trust in the corpus.

The cost scales with corpus size and with the number of contributors, including AI agents operating on subsets of the artifact set.

A small repository with one author can tolerate some duplication; a multi-artifact corpus with many contributors cannot.

The risk this principle mitigates is drift between divergent copies of one fact, where no authoritative side remains to adjudicate which is current.

## How to apply

Before adding a fact, identify the layer it belongs to (a term's home in the terminology, an obligation's home in a requirement, a mechanism's home in a specification, a prose convention's home in the prose conventions) and put it there.
From any other location that needs the fact, cite by reference.

The layer-map for this corpus: the meaning of a term lives in its term under `loom/note/terms/`;
the allowed values of a controlled vocabulary and the rule that checks them live in the relevant specification;
the prose conventions live in `meta/prose-conventions.md`, and the discipline for authoring this corpus without leaking its framing into the method lives in `meta/compartmentalization.md`;
the reason a choice was made over alternatives lives in a Decision Record;
an obligation lives in a Requirement and a mechanism lives in a Specification.

When reviewing, check whether any fact appears in two homes; resolve by deleting the secondary copy, not by reconciling both.

Derived views (the coverage matrix, the traceability lattice, the computed inverse of a relation) are regenerated from the files and are never authored as a second source.

## Considered alternative

Co-locate related content for the reader's convenience, repeating definitions where they are used.

Discarded because drift across copies is the actual cost.

Readers are well served by clear cross-references; they are poorly served by silent contradictions.

## Origin

General English: "source" (Oxford: "a place, person, or thing from which something originates or can be obtained") and "truth" (Oxford: "that which is true or in accordance with fact or reality").

Established in database design through Codd's relational model (1970), where each piece of information is stored once and referenced.

Carried into software as DRY (Hunt and Thomas, 1999) and into structured authoring through DITA's canonical-location pattern.
