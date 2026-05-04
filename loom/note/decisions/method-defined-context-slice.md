---
id: note:dec:pk6jzwy
name: Method-defined context slice
kind: decision
status: current
decided: 2026-06-11T09:30:49Z
---

The semantics of the context slice, what "the intent relevant to a given artifact and a stated purpose" denotes, belong to the method, not to the tool: the method fixes which artifacts a slice contains, and the tool only computes and delivers that slice.

This decision fixes ownership of the slice definition.
It does not fix the closure rules themselves (which relations are followed, for which purposes); those are deferred to a later specification.

## Context

An actor sets out on a task wanting to load only the intent that task needs, working from a small, current, relevant context rather than the whole corpus ([Load only the intent a task needs](../needs/load-only-relevant-intent.md){id=note:need:pv8k2w9}).
A load-bearing facet of that need is that the slice carry no hidden steering: because it is assembled from committed artifacts rather than an opaque retrieval store, no unseen text steers the actor, and context whose provenance the actor cannot verify is exactly the pain the need records ([Acting On Unverifiable Provenance](../needs/load-only-relevant-intent/pain-uncommitted-context-cannot-be-audited.md){id=note:pain:j6gvm9m}).

Two requirements bound the answer and divide cleanly.
[Intent retrievable in relevant subsets](../requirements/stakeholder/intent-retrievable-in-subsets.md){id=note:req:rt3kw9n} obliges that an actor obtain the intent relevant to a task without retrieving the whole corpus.
[Finely addressable intent](../requirements/system/finely-addressable-intent.md){id=note:req:fd8k2w4} holds the corpus decomposed into addressable units and leaves how a subset is computed and delivered to the tool.

What is settled is that a relevant subset must be assemblable and that the corpus stays finely decomposed so it can be.
What is missing is whose definition decides the boundary of that subset: given an artifact and a purpose, which artifacts are in the slice and which are not.
Until that ownership is fixed, "the slice relevant to this task" has no single meaning, and the answer can drift to whatever a particular tool happens to retrieve.

Two principles bind the shape of the answer.
[Single Source of Truth](../principles/single-source-of-truth.md){id=note:principle:8691937} means the definition of the slice has one home; a definition re-derived per tool is the duplication this principle rejects, with each copy free to drift.
[Compute and Report](../principles/compute-and-report.md){id=note:principle:6e7f28k} means a tool computes and reports the slice the method defines; it derives a view from the substrate of record, it does not author the definition of what that view contains.

## Decision

- **The slice semantics belong to the method.**
  Given an artifact and a stated purpose, which committed artifacts constitute the relevant subset is fixed by the method, as a definition deterministically derivable from the corpus.

- **The tool delivers; it does not define.**
  A tool computes and delivers the slice the method defines, and may differ from another tool in performance, packaging, or interface, but not in which artifacts the slice contains for a given artifact and purpose.

- **The definition is auditable from the files.**
  Because the slice is derivable from committed artifacts by a method-fixed definition, a reviewer can reconstruct, after the fact, the subset an actor should have read, and check what it actually read against it.

- **The closure rules are not fixed here.**
  This decision fixes that the slice definition is the method's; which relations are followed for which purpose is a later specification, not part of this choice.
  That later specification is now [The reference closure](../specifications/note/reference-closure.md){id=note:spec:6ntj28w}, which classifies each relation as pull or reference-only, fixes the corpus boundary and scope and group expansion, and versions the rule; it reads `decidedBy` against this decision, so the deferral resolves there without reopening the ownership settled here.

## Forces and trade-offs

- Fixing the slice definition as the method's, rather than letting each tool choose, costs the method a definition it must author and maintain, and costs a tool author the freedom to tune retrieval to a particular model or workflow.
  Accepted: that freedom is exactly what would make the boundary tool-dependent and the slice irreproducible; tools keep every freedom that does not change which artifacts are in the slice.

- Requiring the slice to be deterministically derivable from committed artifacts forecloses retrieval strategies that depend on an opaque store or a non-deterministic ranking.
  Accepted under the no-hidden-steering commitment: a slice an auditor cannot reconstruct from the files is one whose steering lives somewhere the corpus cannot see.

- Deferring the closure rules to a later specification leaves this decision short of a runnable definition.
  Accepted: ownership and the closure rules are separable questions, and settling ownership first lets the closure rules be specified against a fixed contract rather than reopening who owns them.

## Alternatives considered

- **Tool-defined retrieval: each tool computes its own slice by its own heuristic.**
  Rejected: reproducibility is lost, because independent actors using different tools, or the same tool across versions, would read different things for the same artifact and purpose, against [Intent retrievable in relevant subsets](../requirements/stakeholder/intent-retrievable-in-subsets.md){id=note:req:rt3kw9n} taken to its auditable conclusion.
  The no-hidden-steering commitment also fails: the steering would live in the tool's retrieval heuristics, precisely the unverifiable provenance [Acting On Unverifiable Provenance](../needs/load-only-relevant-intent/pain-uncommitted-context-cannot-be-audited.md){id=note:pain:j6gvm9m} records, and the definition would have as many homes as there are tools, against [Single Source of Truth](../principles/single-source-of-truth.md){id=note:principle:8691937}.

- **Similarity-based retrieval over an opaque store (RAG-style embeddings).**
  Rejected: an embedding store is opaque and its ranking non-deterministic, so the slice is neither reproducible across runs nor auditable from the committed artifacts; what steered the actor cannot be read back from the files, again failing the no-hidden-steering commitment.

- **Define nothing (the status quo).**
  Rejected: leaving the slice definition unfixed leaves the boundary wholly tool-dependent by default, which is the tool-defined retrieval case arrived at by omission rather than by choice.

## Driven by

- groundedIn: [Method-defined deterministic context subset](../requirements/system/deterministic-context-subset.md){id=note:req:kdtc9a8}
- groundedIn: [Intent retrievable in relevant subsets](../requirements/stakeholder/intent-retrievable-in-subsets.md){id=note:req:rt3kw9n}
- groundedIn: [Finely addressable intent](../requirements/system/finely-addressable-intent.md){id=note:req:fd8k2w4}
- groundedIn: [Load only the intent a task needs](../needs/load-only-relevant-intent.md){id=note:need:pv8k2w9}
- groundedIn: [Single Source of Truth](../principles/single-source-of-truth.md){id=note:principle:8691937}
- groundedIn: [Compute and Report](../principles/compute-and-report.md){id=note:principle:6e7f28k}
