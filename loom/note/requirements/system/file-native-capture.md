---
id: note:req:mgdg9q0
name: File-native capture
kind: requirement
level: system
type: constraint
status: current
---

Note shall ensure that every reading and authoring operation it defines can be performed by an actor using only basic reading and writing, without any specific tool.
No operation Note defines shall depend on a particular tool being installed or invoked.

## Rationale

This is the load-bearing restriction behind portability and universal participation.

If any defined operation needed a tool, the method would inherit that tool's availability as a precondition, and the floor would no longer be plain reading and writing.

The concrete substrate (plain-text files) is a specification concern.

## Relations

- derivedFrom: [Durable, portable intent](../stakeholder/durable-portable-intent.md){id=note:req:93kczqj}
- derivedFrom: [Universal participation](../stakeholder/universal-participation.md){id=note:req:j4kecn7}
- delivers: [Plain-Text Substrate](../../offerings/intent-you-own/pr-plain-text-substrate.md){id=note:pr:xzpv4p0}
- delivers: [An Agent Contributes With Stock Primitives](../../offerings/works-anywhere/pr-agent-contributes-with-stock-primitives.md){id=note:pr:7ac4wny}
- delivers: [Contribute From the First Minute](../../offerings/works-anywhere/pr-contribute-from-the-first-minute.md){id=note:pr:dhfxzdp}
