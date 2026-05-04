---
id: note:term:qt3b8r8
name: Layer
kind: term
status: current
---

A coherent body of artifacts riding one Substrate for a single concern.
A corpus may enable multiple layers independently; each layer is anchored at a layer root, the directory where that layer's manifest sits.

The method names three layers: the note layer (intent artifacts), the plan layer (task and dependency artifacts, deferred), and the guild layer (role and coordination artifacts, reserved).
Any one of these may be present or absent without affecting the others; the substrate machinery is shared, the concerns separated.

## Inclusion test

Does it collect artifacts that share a single concern (intent, planning, roles) under one manifest and one layer root, riding the same substrate machinery?
If instead it gathers artifacts that span multiple concerns under one manifest, it is a corpus, not a layer.

## Relations

- *carries* [Note](note.md){id=note:term:6yb8hnm}

## Origin

Oxford: "layer: a sheet, coating, or thickness of material, typically one of several, covering a surface or body".

In software architecture, layering is the discipline of separating concerns into stacked, independently-evolvable tiers, each with a defined responsibility and a defined interface to adjacent layers.
The usage here borrows the separation-of-concerns sense: each layer is an independently deployable concern riding a shared substrate, analogous to how an application layer and a persistence layer share a runtime but hold different responsibilities and may evolve at different rates.
