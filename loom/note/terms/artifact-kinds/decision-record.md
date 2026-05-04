---
id: note:term:met4a44
name: Decision Record
kind: term
status: current
---

A record of a choice and its rationale: the options considered, the forces and trade-offs, and the context, linked to the artifacts the choice shaped.

A Decision Record carries what a Requirement or Specification does not, namely the alternatives that were rejected and why.

The kind is always available; using it is opt-in per the adopted profile.

## Inclusion test

Does it capture *why* a choice was made over named alternatives, rather than *what* the chosen thing must do or how it is designed?

If it restates the requirement or the specification, it is not earning its place as a Decision Record.

A Decision Record is also earned by the choice's weight, not only its register: were real alternatives weighed, would a future reader plausibly re-litigate or silently undo it, and does it bind work beyond the change that carries it?
A choice that fails that test (a routine fix, a reversible detail, a call no one would contest) is recorded in the commit message that carries the change, citing any artifact it touches, not minted as a Decision Record.

## Relations

- *relates to* [Requirement](requirement.md){id=note:term:tr9zna6} (records why a Requirement's content was chosen over alternatives; on the artifact, the Requirement names the Decision through its decidedBy edge)
- *relates to* [Specification](specification.md){id=note:term:9xd6ejd} (records why a Specification's content was chosen over alternatives; on the artifact, the Specification names the Decision through its decidedBy edge)

## Origin

General English (Oxford: a "decision" is "a conclusion or resolution reached after consideration"; a "record" is "a permanent account kept for future reference").

Standardized as the architecture decision record (ADR) in Nygard's pattern and the lightweight context-decision-consequences template that followed it, where the artifact's reason for being is to preserve the rejected alternatives and the forces in play that a requirement or specification discards once the choice is settled.
