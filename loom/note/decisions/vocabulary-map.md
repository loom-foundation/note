---
id: note:dec:wn3xsjw
name: The manifest vocabulary map
kind: decision
status: current
decided: 2026-06-12T00:00:00Z
---

A corpus may declare an optional `vocabulary` map in its manifest that maps a house term to a canonical token, unique in both directions, for the method's statuses and verbs.
The map is display and input normalization only: committed files, including commit trailers and code comments, carry canonical tokens exclusively.
The work splits across the method and a tool: the method declares the map and the canonical-only invariant in its substrate, and a tool corpus carries the requirements to honor it, rendering house terms, normalizing input on receipt, warning, and never writing an alias to a file.
The lifecycle stage set and its transitions are fixed; stage names ride the same map, and a pack may narrow a kind's stage set but never widen it.

## Context

An Adopter often arrives with an entrenched vocabulary for the same concepts the method tokenizes: a status it calls "in-progress" where the method writes `draft`, a relation it reads as "implements" where the method writes `enacts`.
Forcing the Adopter to abandon its words at the point of authoring is friction the method does not need to impose, because the friction is at the surface, not in the model.

The substrate forecloses the deeper move.
It offers no author-facing aliasing of canonical kind or verb tokens, because a two-vocabulary corpus breaks the property that a token means the same thing in every corpus of the method, which is what makes a corpus safe to read cold ([Kind-agnostic substrate and kind packages](substrate-and-kind-packages.md){id=note:dec:w4awceq}).
What remains open is a narrower, safe surface: a map that lets a house word appear to a person while the file on disk still carries the canonical token, so the shared-priors guarantee holds for every reader and agent that opens the committed file.

Two things have to be settled.
First, where the map is declared and what it normalizes, since a map that lived in a tool's space would be invisible to every other tool and to an unaided reader.
Second, the boundary between the method, which declares the map and the invariant, and a tool, which performs the rendering and normalization, since the method enforces nothing and a tool computes and reports.

## Decision

- **An optional `vocabulary` map in the manifest.**
  A corpus may declare a `vocabulary` map among the manifest's configuration, beside the method version, the profile, the enabled packs, and the scope block.
  The map is optional; a corpus that declares none uses canonical tokens throughout and pays nothing.
  It maps a house term to a canonical token for the method's statuses and verbs, and the mapping is unique in both directions, so a house term names exactly one canonical token and a canonical token is fronted by at most one house term.

- **Display and input normalization only.**
  The map governs what a person sees and what a tool accepts on input, never what a file stores.
  Committed files carry canonical tokens exclusively, and that invariant extends past the corpus to every committed surface: commit trailers and code comments carry canonical tokens only.
  A house term is a front-end word, never a value written to a file.

- **The method declares; a tool honors.**
  The method, Note, declares the `vocabulary` map and the canonical-only invariant in its substrate.
  The tool corpus carries the requirements to act on it: render house terms where a person reads, normalize a house term to its canonical token on receipt, warn where input does not resolve, and never write a house term to a file.
  This is the method-states-the-rule, tool-honors-it split, consistent with the way permission and enforcement stay with the tool and its authority while the method computes and reports ([Compute and Report](../principles/compute-and-report.md){id=note:principle:6e7f28k}).

- **The agent rule: read first, translate on receive, write canonical.**
  An agent reads the map before authoring, translates a house term to its canonical token at the moment of receiving input, and writes the canonical token to the file.
  The map is the first thing read and the last thing applied is canonical, so nothing a house term touches reaches a committed surface.

- **Lifecycle stages ride the same map.**
  The lifecycle stage set and the transitions among the stages are fixed by the substrate, not configurable.
  The stage names are tokens like any other, so a house term may front a stage name through the same `vocabulary` map.
  A pack may narrow the stage set available to one of its kinds, never widen it; the map renames a stage, it never adds or drops one.

- **`vocabulary` and `aliases` are two distinct mechanisms, named apart.**
  **`vocabulary`** is the manifest map: house words for the method's own tokens, the statuses and verbs, declared once for the corpus and normalized away before a file is written.
  **`aliases`** is an artifact-level designation list: other names for the *thing* an artifact denotes, a synonym or a prior name of that one concept, carried on the artifact itself ([Uniform opaque identity](identity-and-designations.md){id=note:dec:jhgkwja}).
  One renames the method's vocabulary for display; the other records additional designations of a single artifact.
  They are never the same surface and never collapse into one.

## Forces and trade-offs

The map buys an Adopter their own words at the surface without buying the coherence tax of a two-vocabulary corpus.
Because the file on disk always holds the canonical token, every reader and every agent that opens a committed file reads the same token it would read in any other corpus of the method, so the shared-priors guarantee that lets a corpus be read cold is preserved exactly.
The cost is borne entirely at the tool layer, where the rendering and normalization live, and falls to zero for a corpus that declares no map.

Requiring the map to be bidirectionally unique closes the ambiguity a many-to-one map would open, where a canonical token fronted by two house terms could not be rendered deterministically and a house term mapping to two tokens could not be normalized.
The cost is that an Adopter with two informal words for one concept must pick one as its house term; that is the price of a deterministic round-trip, and it is small.

Declaring the map in the manifest rather than in a tool's space keeps it readable without the tool, so the canonical-only invariant and the house mapping are both visible to an unaided reader and to a second tool.
A map hidden in one tool's configuration would be invisible to every other reader, which is the failure the manifest's tool-agnostic home exists to prevent.

## Alternatives considered

- **Author-facing aliasing that renames canonical tokens in the file.**
  Rejected at the substrate: a two-vocabulary corpus on disk breaks the property that a token means the same thing in every corpus, the shared-priors guarantee an agent depends on ([Kind-agnostic substrate and kind packages](substrate-and-kind-packages.md){id=note:dec:w4awceq}).
  The map normalizes at the surface and writes canonical, so the file never carries the house word.

- **Declare the map in the tool's own configuration.**
  Rejected: a map living in one tool's space is invisible to every other tool and to an unaided reader, so the house-to-canonical mapping and the canonical-only invariant could not be read without that one tool.
  The manifest is the tool-agnostic home the declaration needs.

- **A many-to-one or otherwise non-unique map.**
  Rejected: without uniqueness in both directions, rendering and normalization stop being deterministic, since a canonical token fronted by two house terms has no single rendering and a house term naming two tokens has no single normalization.
  Bidirectional uniqueness keeps the round-trip exact.

- **Fold the house-vocabulary map into the artifact-level `aliases` list.**
  Rejected against Single Source of Truth: `aliases` records additional designations of one artifact's concept, while `vocabulary` renames the method's shared tokens for the whole corpus; collapsing them would make one list mean two different things and lose the per-corpus, declare-once home the map needs.
  The two mechanisms stay named apart.

## Driven by

- groundedIn: [Kind-agnostic substrate and kind packages](substrate-and-kind-packages.md){id=note:dec:w4awceq}
- groundedIn: [Single Source of Truth](../principles/single-source-of-truth.md){id=note:principle:8691937}
- groundedIn: [Compute and Report](../principles/compute-and-report.md){id=note:principle:6e7f28k}
- groundedIn: [Adopt without being stranded by the method's own evolution](../needs/adopt-without-being-stranded.md){id=note:need:x4zqfws}
