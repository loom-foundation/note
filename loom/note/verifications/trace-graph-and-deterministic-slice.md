---
id: note:ver:tr4c3sg
name: Trace graph and the deterministic slice
kind: verification
status: current
method: analysis
---

This verification confirms that the corpus's relationships are legible and computable from the files alone: the trace graph reconstructs from the authored relations, the reference closure of any selection is deterministic under the closure specification's rules, intent stays decomposed into addressable units locatable by scope and group, personas and terms resolve by their named-once definitions, and the value layer's claims are expressible and linked.
The check is a static pass over the committed files ([The reference closure](../specifications/note/reference-closure.md){id=note:spec:6ntj28w}); it computes and reports findings only, and the verdict belongs to the Orchestrating Authority.

## Criteria

A pass requires that:

- from any artifact, every relationship it holds and every artifact that depends on it is readable off the authored edges and their derived inverses, with no relationship recoverable only from prose;
- the reference closure of a sampled selection, computed twice in different traversal orders under the classification the closure specification fixes, yields the same set both times, with cross-corpus targets reported as boundary markers rather than members;
- every unit of intent is one artifact in one file with a durable id, locatable by its enclosing scope and its directory group, so a relevant subset is a set of whole artifacts rather than excerpts;
- the members of any group directory are enumerable as a set, and no mirrored group field exists to drift against the directory;
- every persona reference in a `persona` field and every capitalized designation in sampled prose resolves to exactly one artifact in force at the reading scope;
- every value-proposition `expresses` an offering and every offering `addresses` a need, so the authored value-claim links to the intent it pitches;
- every `provides` edge is authored on a system-of-interest and resolves to an offering, value-proposition, pain-reliever, or gain-creator, no provision edge is authored on a value artifact, and the derived provision view of a sampled offering expands coarse claims to facets with overlap surfaced as shared provision;
- the coverage view derives from the files alone: every unaddressed need, unanswered pain or gain, undelivered reliever or creator, and unverified current requirement is enumerable with the direction it points, and no such gap invalidates an artifact or blocks a check.

A pass is zero failures across the corpus.

## Procedure

By analysis.
A static reader builds the relation graph from every `## Relations` and `## Driven by` bullet and every reference-bearing frontmatter field, derives the inverse views, and confirms each derived inverse traces to exactly one authored edge.
It computes the closure of a fixed sample of selections (an artifact, a scope, a group) twice with different visit orders and compares the resulting sets, recording boundary markers separately.
It enumerates each kind directory and group, verifies one-artifact-per-file and id addressability, and resolves every persona citation and a sample of capitalized designations against the names and aliases in force.
The reader only reads; it executes nothing, so the check is reproducible by anyone with the repository.

## Evidence

A run produces a report: the edge and inverse counts, the per-selection closure sets and their equality, the group enumerations, and any unresolvable designation or missing value-layer link.
The report is kept with the run by the Orchestrating Authority; it is not stored in this artifact.

## Relations

- verifies: [Inspectable traceability](../requirements/stakeholder/inspectable-traceability.md){id=note:req:sg0npmv}
- verifies: [Intent retrievable in relevant subsets](../requirements/stakeholder/intent-retrievable-in-subsets.md){id=note:req:rt3kw9n}
- verifies: [Method-defined deterministic context subset](../requirements/system/deterministic-context-subset.md){id=note:req:kdtc9a8}
- verifies: [Finely addressable intent](../requirements/system/finely-addressable-intent.md){id=note:req:fd8k2w4}
- verifies: [Grouping of artifacts](../requirements/system/artifact-grouping.md){id=note:req:n6w4k9t}
- verifies: [A corpus navigable by group](../requirements/stakeholder/groupable-corpus.md){id=note:req:h3k8w2m}
- verifies: [Unambiguous, related term meaning](../requirements/stakeholder/unambiguous-related-term-meaning.md){id=note:req:c5k9w2h}
- verifies: [Named-once, scoped persona](../requirements/stakeholder/shared-scoped-persona.md){id=note:req:c8w5k2h}
- verifies: [Expressible value proposition](../requirements/stakeholder/expressible-value-proposition.md){id=note:req:3pk9w2v}
- verifies: [Attributable, versioned provision](../requirements/stakeholder/attributable-versioned-provision.md){id=note:req:atr7vpn}
- verifies: [Authored provision claims with derived coverage](../requirements/system/authored-provision-claims.md){id=note:req:pr0vc74}
- verifies: [Actionable, non-blocking coverage view](../requirements/stakeholder/actionable-coverage-view.md){id=note:req:c0vg4pd}
