---
id: note:term:rqbkaxn
name: Scope
kind: term
status: current
---

The position at which intent becomes load-bearing and below which it is inherited.

The sources an artifact inherits from form a directed acyclic graph, not a single chain, so that a cross-cutting concern can be inherited from more than one source.

A Scope is not necessarily a Context: a cross-cutting scope carries obligations but has no inside or outside boundary.

## Inclusion test

Does it fix where an obligation first applies and what inherits it, rather than what finer obligation decomposes from it?
If so it is a Scope question; if instead it asks what finer obligation decomposes from this one, that is Derivation.

## Relations

- *relates to* [Cascade](cascade.md){id=note:term:5b6cbtr} (is the axis the cascade operates on; cascade composes inherited intent across scope positions)

## Origin

General English (Oxford: "the extent of the area or subject matter that something deals with or to which it is relevant").

The corpus narrows that extent to a position in an inheritance graph: not just how far an obligation reaches but where it becomes load-bearing and from which sources it is inherited, akin to lexical scope in programming, where a name binds at one level and is visible to the levels nested within it.
