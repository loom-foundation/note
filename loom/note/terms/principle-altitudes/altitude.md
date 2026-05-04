---
id: note:term:a1h1jre
name: Altitude
kind: term
status: current
---

The classification axis of a Principle: the level at which a weighted commitment operates and the reader it serves, one of Value, Operating, or Authoring.

Authoritative in the optional `altitude` frontmatter field on a Principle artifact; available at every profile ([Principle altitude field](../../decisions/principle-altitude-field.md){id=note:dec:3vg9jdh}).
A principle that operates at more than one altitude records its home altitude, the one that fixes where it is published and read.

## Inclusion test

Does the label answer "at what level does this principle operate and whom does it serve: who we are (Value), how we work (Operating), or how we write the corpus (Authoring)?", rather than what the principle commits to (its content) or how it is balanced against other principles?
If it classifies the operating level of the commitment, it is the Altitude axis.

## Origin

General English ("altitude": the height of an object or region above a level; figuratively, the level at which something operates).

The three altitudes track the established tiers of normative commitment: the values-and-principles split of the Agile Manifesto and the architecture-principle tradition (TOGAF), and the distinction between principles that govern the work and those that govern its own authoring.
"Altitude" is coined as the axis name because the corpus already uses "facet" for the members of a Need or Offering and would collide.
The axis is a field on the one Principle kind rather than a set of kinds, because the three levels share one inbound relation (`enactedBy`) and so are not distinct kinds under the rule that a kind is earned only by a distinct inbound relation ([Atomic facets](../../decisions/atomic-facets.md){id=note:dec:af3k9w2}, [Principle altitude field](../../decisions/principle-altitude-field.md){id=note:dec:3vg9jdh}).
