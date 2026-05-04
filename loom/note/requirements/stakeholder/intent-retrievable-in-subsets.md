---
id: note:req:rt3kw9n
name: Intent retrievable in relevant subsets
kind: requirement
level: stakeholder
type: functional
status: current
---

An actor shall be able to obtain the intent relevant to a task, addressed at the grain of the individual artifact, the scope, or the group, without retrieving the whole corpus, so that it works from a small, current, relevant context.

## Source

See the Source of [Load only the intent a task needs](../../needs/load-only-relevant-intent.md){id=note:need:pv8k2w9}.

## Rationale

The corpus is already decomposed into addressable units, one artifact per file with a durable identifier, organized by scope and by group, which is what makes a relevant subset assemblable at all.

This obligation states that intent must be retrievable in such subsets, and leaves how the corpus stays finely decomposed, and how a subset is computed and delivered, to the system requirements.

A smaller relevant context is the methodology's structural answer to the degradation of attention over a long context, and to the cost of loading more than a task needs.

## Relations

- addresses: [Load only the intent a task needs](../../needs/load-only-relevant-intent.md){id=note:need:pv8k2w9}
- delivers: [Reasoning Sharp and Efficient](../../offerings/right-sized-context/gc-reasoning-sharp-and-cheap.md){id=note:gc:dcgy5df}
- delivers: [Obligations Ride in the Slice](../../offerings/right-sized-context/pr-obligations-in-the-slice.md){id=note:pr:0d8rpg8}
- delivers: [Task-Scoped Slices](../../offerings/right-sized-context/pr-task-scoped-slices.md){id=note:pr:j625vdn}
