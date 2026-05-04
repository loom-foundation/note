---
id: note:term:63pef7z
name: Substrate
kind: term
status: current
---

The kind-agnostic machinery every Note artifact rides: the file envelope, the identity scheme, the conformance floor, the universal lifecycle, the relation machinery, the term-relation set, the citation surfaces, the conformance profiles, the pack mechanism, and the manifest schema.
The substrate knows no particular Kind; the kinds, their fields, their body sections, and the relation endpoint rows they contribute are supplied by Kind Packages layered on top of it.

What the substrate fixes is invariant across every corpus and every kind: well-formedness, identity, lifecycle, traceability, and checkability can all be evaluated from the substrate specification alone, before any package is consulted.

## Inclusion test

Does it describe machinery that applies regardless of which Kind Package is enabled, such that removing all packages leaves it intact and applicable?
If it names specific kinds, their fields, or their body sections, it belongs in a Kind Package, not in the substrate.

## Relations

- *carries* [Kind Package](kind-package.md){id=note:term:f61fk9g}
- *carries* [Layer](layer.md){id=note:term:qt3b8r8}

## Origin

Oxford: "substrate: an underlying layer or substance, especially the layer on which an organism lives and grows or to which it is attached".

In materials science and biology the substrate is the surface or medium that provides the foundation on which a structure is built or a process occurs, entirely indifferent to what is built on it.
In computing the sense extends to any runtime or platform that underlies an application layer without knowing its contents: a message-bus substrate, a storage substrate, a virtual-machine substrate.
The Note usage follows the materials/biology lineage directly: the substrate is the foundation a Kind Package extends, present regardless of which package is enabled, knowing nothing about the kinds that ride it.
