---
id: note:req:fd8k2w4
name: Finely addressable intent
kind: requirement
level: system
type: functional
status: current
---

Note shall keep intent decomposed into independently addressable units, each retrievable on its own by durable identifier and locatable by its scope and its group, so that the subset relevant to a task can be assembled without retrieving unrelated intent.

## Rationale

Selective retrieval is only possible if intent is decomposed finely and each unit is addressable.

The decomposition rests on intent being one artifact per file ([Artifacts are Markdown with YAML frontmatter](../../decisions/artifact-file-format.md){id=note:dec:pxnjmcd}) with a location-independent identifier ([Requirement levels](../../decisions/requirement-levels-and-identity.md){id=note:dec:nc2yrf4}), placed in the scope graph ([Scope and inheritance](scope-and-inheritance.md){id=note:req:96smmcv}) and grouped for navigation ([Grouping of artifacts](artifact-grouping.md){id=note:req:n6w4k9t}).

This requirement holds the corpus to staying decomposed finely enough that a relevant subset is a small set of whole artifacts, not an excerpt; how a subset is computed and delivered is the tool's concern and specification.

## Relations

- derivedFrom: [Intent retrievable in relevant subsets](../stakeholder/intent-retrievable-in-subsets.md){id=note:req:rt3kw9n}
- delivers: [Grounded in Stated Intent](../../offerings/right-sized-context/pr-grounded-in-stated-intent.md){id=note:pr:qj473b0}
- delivers: [Stated Once, Loaded Once](../../offerings/right-sized-context/pr-stated-once-loaded-once.md){id=note:pr:3jk1je5}
