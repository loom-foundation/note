---
id: note:req:fph0vnr
name: Independently validatable specifications
kind: requirement
level: system
type: functional
status: current
---

Note shall ensure that a specification can be validated against an authority independent of the method's own assertions, so a specification's content is falsifiable by something other than the method itself.

## Rationale

Typing a specification only by a label leaves its content unvalidatable.

Independent validation also makes a specification more reliably authorable by an agent, because an external authority constrains the output (inferred; not yet measured).

For example, an interface description is checked against an independent grammar, an OpenAPI document or a JSON Schema, rather than against Note's say-so.
How a specification declares that authority, and the fallback where no external authority exists, are fixed by the `authority` field the spine pack adds to the specification kind ([Independent authority on specifications](../../decisions/specification-authority.md){id=note:dec:av7k3mq}).

## Relations

- derivedFrom: [Verifiable, independently checkable design](../stakeholder/verifiable-independently-checkable-design.md){id=note:req:vh3k82n}
