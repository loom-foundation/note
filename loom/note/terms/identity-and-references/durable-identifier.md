---
id: note:term:24hmw8y
name: Durable Identifier
kind: term
status: current
---

The immutable, opaque handle for an artifact, minted once at creation and never changed regardless of where the artifact moves, what it is renamed to, or how its content evolves.

The form is `namespace:kind-segment:opaque`: the namespace (ownership scope), the kind-segment fixed by the artifact's Kind at minting, and a short randomly generated meaningless string over a human-friendly alphabet (Crockford Base32 by default, seven characters, checked for collision before use).
The same opaque grammar serves every kind uniformly; no kind carries a slug in place of the opaque segment.
The id encodes no meaning and survives any reorganization of the corpus tree.

The human-readable designation lives in the `name` field (and optionally `aliases`), not in the identifier.
A reference to an artifact carries the Durable Identifier as the load-bearing part; the visible link text is the target's current name, refreshed after any rename without breaking the citation.
A re-leveling or re-scoping of an artifact never changes its id, because level and scope are separate fields.

## Inclusion test

Does it survive a move, a rename, and a substantial change of content or scope unchanged, and can a human cite it in prose or a code comment without it becoming stale?
If it changes on any of those events, it is a location or a label, not an identifier.

## Relations

- *relates to* [Namespace](namespace.md){id=note:term:x494sn0} (scoped by; a Durable Identifier is qualified by the namespace that makes it globally unique)
- *relates to* [Reference](reference.md){id=note:term:evt67dx} (carried in; a Reference pairs the Durable Identifier with a navigable link)

## Origin

Oxford: an identifier is "a sequence of characters used to identify or refer to a program or an element, such as a variable or a set of data, within it".

The "durable" qualifier marks the design commitment that the handle outlive every change to where the artifact sits and what it says.
The designation (the name the corpus authors chose) is explicitly kept separate from the identity, which is the split that allows renaming without breaking any citation.

The lineage is the persistent-identifier tradition of scholarly and web infrastructure, where a name is deliberately decoupled from a location so that citation survives relocation (the DOI system, ISO 26324, and the URN/URI split between identity and resolution).
