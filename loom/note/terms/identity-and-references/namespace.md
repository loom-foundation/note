---
id: note:term:x494sn0
name: Namespace
kind: term
status: current
---

The ownership boundary that makes identifiers globally unique without a central registry.
A corpus declares its namespace once, in its manifest, and uses it consistently; an opaque is unique within the namespace, so distinct namespaces never collide and one namespace may span several repositories of one system ([The multi-root corpus](../../decisions/multi-root-corpus.md){id=note:dec:0n14gqx}).

The recommendation is to anchor it to something already globally registered (a domain or repository URL you control), because that removes collisions for free.

This corpus declares the `note` namespace; the method's reference tool keeps its own corpus in a sibling repository under a separate `sett` namespace, because the methodology and the tool are versioned independently.
Identifiers read, for example, `note:need:jwvn9b7` and `sett:req:x5z0v7s`.

## Inclusion test

Is the chosen anchor something the corpus owner controls, so that two independent corpora cannot mint the same identifier by accident?

If anyone could mint the same string, it is not a safe namespace.

## Origin

General English (Oxford: "a set of characters or symbols used to identify and refer to a group of related elements within a computer system, application, etc.").
The term is standard in computing, where a namespace is a context that disambiguates names so that the same local name can be reused without collision (XML namespaces, C++ and language module namespaces, DNS).

This corpus follows that lineage but resolves uniqueness by anchoring the namespace to something already globally registered rather than to a central registry.
