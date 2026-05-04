---
id: note:term:f61fk9g
name: Kind Package
kind: term
status: current
---

A declarative selection of Kinds: a named, self-contained module that specifies which kinds exist within it, each kind's id kind-segment, its required and optional frontmatter fields beyond the common envelope, its required and optional body sections in canonical order, and the relation endpoint rows it contributes to the verb catalogue.
A corpus enables one or more packages in its manifest; the effective kind set is the union of the enabled packages' declared kinds.

## Inclusion test

Does it name a closed set of kinds together with each kind's id segment, fields, body sections, and relation endpoint rows, such that a checker can validate kind-legality and field conformance from the package declaration alone?
If it only selects a profile or a vocabulary, it is not a Kind Package.

## Origin

Oxford: "package: a set of proposals or terms offered or agreed as a whole".

In software, a package is a declared module of related definitions, the unit of enabling or disabling a coherent set of capabilities: npm packages, Python packages, and IDE plugin packs all share the pattern of a named, versioned, self-contained declaration that a consumer opts in to.
Nearer still is the methods-engineering lineage: OMG's SPEM 2.0 packages a selectable body of method content as a Method Package, delivered as a Method Plugin, the direct ancestor of a pack that carries a methodology's kinds.
The Note usage follows that lineage: a Kind Package is the declared module whose enabling makes a set of kinds legal in a corpus, keeping kind availability configurable rather than fixed in a global enum.
