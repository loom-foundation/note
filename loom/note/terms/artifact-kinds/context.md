---
id: note:term:ddcqz2b
name: Context
kind: term
status: current
---

A problem-space statement of the system's boundary: the external entities it interacts with, what crosses the boundary, and what is explicitly out of scope.

A Context scopes the Needs and Requirements beneath it; it states no persona's job, no obligation, and no design.

## Inclusion test

Does it fix what is inside the system, what is outside, and what crosses the boundary, without stating a persona's job, an obligation, or a mechanism?

If it states a problem a persona has, it is a Need; if an obligation, a Requirement; if a design commitment, a Specification.

## Relations

- *scopes* [Need](need.md){id=note:term:x4vqdj1}
- *scopes* [Requirement](requirement.md){id=note:term:tr9zna6}
- *scopes* [Specification](specification.md){id=note:term:9xd6ejd}
- *relates to* [Scope](../relations-scope-and-traceability/scope.md){id=note:term:rqbkaxn} (composed along the Scope graph; a Subsystem inherits its supersystem's Context and narrows it)

## Origin

General English (Oxford: "the circumstances that form the setting for an event").

Standardized as the system boundary in ISO/IEC/IEEE 29148, as the context diagram in structured analysis (DeMarco; Gane and Sarson) and in Jackson's Problem Frames, and as the system-context view in the C4 model, where the outermost view fixes the system and the external entities it touches before any internal detail.

Distinct from a Bounded Context in Domain-Driven Design, which bounds a model and its language rather than a system's external entities and ports; and from the Orchestrating Authority, which is the runtime and governance sense of "context", not the boundary.
