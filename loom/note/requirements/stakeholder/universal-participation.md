---
id: note:req:j4kecn7
name: Universal participation
kind: requirement
level: stakeholder
type: constraint
status: current
---

Any actor capable of basic reading and writing, human or AI and including agents in constrained environments such as sandboxes, runners, and small models, shall be able to read and author intent without specialized or privileged tooling.

Furthermore, every check the method defines shall remain performable in principle without specialized or privileged tooling, so that no capability the method relies on is hidden behind a tool.

## Source

See the Source of [Participation without special tools](../../needs/participation-without-special-tools.md){id=note:need:63w7v3e}.

## Rationale

A method that requires specialized tooling to read or write its artifacts raises the capability floor and excludes actors who would otherwise participate.

The obligation has two faces that stand or fall together as one property, no hidden tool dependency: authoring must need nothing privileged, and checking, even when a tool accelerates it, must remain reproducible in principle by an unaided actor, or the method would secretly depend on that tool.

This is also why the method cannot itself hold access control or permission;
that is left to the Orchestrating Authority (see `context.md`).

## Relations

- addresses: [Participation without special tools](../../needs/participation-without-special-tools.md){id=note:need:63w7v3e}
- delivers: [An Agent Contributes With Stock Primitives](../../offerings/works-anywhere/pr-agent-contributes-with-stock-primitives.md){id=note:pr:7ac4wny}
- delivers: [Contribute From the First Minute](../../offerings/works-anywhere/pr-contribute-from-the-first-minute.md){id=note:pr:dhfxzdp}
- delivers: [One Method the Whole Team Can Reach](../../offerings/works-anywhere/pr-one-method-the-whole-team-can-reach.md){id=note:pr:47tnv5g}
