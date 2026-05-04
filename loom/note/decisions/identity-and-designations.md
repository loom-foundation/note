---
id: note:dec:jhgkwja
name: Uniform opaque identity
kind: decision
status: current
decided: 2026-06-12T00:00:00Z
---

Every kind uses one identity grammar with no exception: an artifact's id is `namespace:kind-segment:opaque`, the opaque segment unique within its namespace, random where a tool mints it, immutable, and never re-minted by a move.
An artifact carries a `name` field holding its designation, a concise label, and an optional `aliases` list holding additional designations.
A reference always carries the target's id; the visible link text is the target's current name and is refreshed, never load-bearing.
A designation is unique within its namespace at minting, and an ambiguous designation in the effective set at a reading scope is surfaced like a cascade tie.

## Context

A concept and the word that designates it are two things.
The terminology tradition the method rests on (ISO 704 and ISO 1087) treats a concept as having one or more designations, and replacing a designation with a synonym, swapping "Client" for "Customer" while the definition holds, is ordinary terminology work.

The prior identity rule made an exception for the kinds referred to by name, terms and personas, giving them a readable slug in place of an opaque segment, on the reasoning that the word is the thing.
That exception conflates the concept with its designation.
When a designation changes, the slug embedded in the id and in every citation of it begins to lie, which is the precise failure that already moved principles and conventions to opaque ids: a frozen descriptive handle survives a rename and points at a name no longer in use, and a citation held in an immutable surface such as a commit trailer cannot be rewritten to follow.

Two further threads converge here.
The frontmatter field that carried an artifact's human-readable handle was named `title`, yet the rule for it ("a concise label, not a summary") describes a name, not a document title; a persona has a name, and a term is a name.
And once designations are mutable and an artifact may carry more than one, prose lookup of a capitalized term and tool resolution of a handle both need a defined notion of which designation is in force and what makes one unambiguous.

## Decision

- **One id grammar, no exceptions.**
  Every artifact's id is `namespace:kind-segment:opaque`.
  Terms and personas use the same opaque grammar as every other kind; no slug id exists anywhere in the model.
  The id is minted once and never changes; a move or a rename leaves it untouched.

- **The opaque segment.**
  The opaque is a Crockford Base32 string (the digits `0` to `9` and the letters `A` to `Z` minus `I`, `L`, `O`, and `U`), written lowercase and compared case-insensitively.
  It must be unique within its namespace; a tool mints it from a cryptographically secure source and checks it for collision against the corpus, and a sole mint authority may instead allocate opaques another way, for example sequentially with a small registry, as long as they stay unique within the namespace.
  Randomness is the recommended path because it keeps independent authors collision-free with no coordination, which is what lets one namespace span several repositories.
  Its length is configurable per corpus in the manifest, defaulting to seven characters; the configured length applies to newly minted ids and never forces a re-mint of existing ones.

- **The `kind` field is authoritative.**
  The `kind` field states the artifact's kind; the id's kind-segment is fixed from it at minting and the two must agree, a single check rather than a second source of truth.

- **`name` replaces `title`.**
  The frontmatter field is `name`, holding the artifact's designation: a concise label, never a summary of the body, and never repeated as a body heading.
  There is no `title` field; a single field carries the handle, not two.

- **`aliases` carries additional designations.**
  An optional `aliases` list holds further designations of the same concept: a synonym kept during a transition, an abbreviation, a prior name.
  Aliases are for lookup and display only; a reference never targets an alias, and an alias is never the load-bearing part of a citation.

- **References carry ids; link text is refreshed.**
  Every reference carries the target's id as the authoritative part, wherever the reference lives: in body prose or in a frontmatter reference field such as a need's `persona`.
  The visible link text is the target's current name, a convenience a tool refreshes after a rename; if it drifts, nothing breaks, because the id is the citation.

- **Prose lookup resolves against designations.**
  A capitalized word in prose resolves against the names and aliases of the terms and personas in force at the reading scope, the same closed-vocabulary lookup as before, now reading a set of designations rather than a single frozen slug.

- **Uniqueness is checked twice, each at its natural moment.**
  At minting, a designation (a name or an alias) is unique within its namespace; a tool refuses a duplicate outright.
  At resolution, a designation that is ambiguous in the effective set at a reading scope, which inheritance across namespaces can create, is surfaced like a cascade tie, with the cascade's replace operator as the sanctioned resolution.

## Forces and trade-offs

Two costs are named rather than hidden.
A `persona` entry in the citation form is longer than a bare id, and its name label and relative path can drift after a rename or a move until refreshed; the id is the citation and never drifts, and a tool refreshes labels and paths in one mechanical pass.
And the model's one latent designation collision, two distinct concepts both designated "System" (the boundary and the level value), becomes a finding the uniqueness rule forces to the surface: the level value is redesignated, for example "System Level", so that "System" designates exactly one concept.

Against these, the model gains a single identity rule with no special case, a corpus where every kind is rename-proof, a field name that says what it holds, and orthodoxy with the terminology tradition the corpus already cites, where the prior slug exception was the unorthodox part.
Filenames remain readable kebab-case, as they always were; they were never the identity.

## Alternatives considered

- **Keep slug ids for the kinds where the word is the thing (the prior rule).**
  Rejected: it conflates a concept with its designation, contradicts the ISO 704 and 1087 lineage the terminology rests on, and re-creates for terms and personas the rename-strands-citations failure that already removed the exception for principles and conventions.

- **Keep `title` and add `name` beside it.**
  Rejected against Earned Substance: a second field that holds the same concise handle is ceremony, and two fields for one designation invite drift over which is canonical.

- **Make designations globally unique across namespaces.**
  Rejected: namespaces exist precisely so that two corpora, or two scopes, may designate distinct concepts with the same word; global uniqueness would break inheritance across namespaces.
  Uniqueness is per namespace at minting, and cross-namespace ambiguity at a scope is a resolution-time surface, not a minting-time prohibition.

- **Bare id in the `persona` field (no name label or path).**
  Rejected: a bare id leaves the raw file illegible and unnavigable without a resolving step; the reader cannot see who wants the need, nor follow a path to the persona artifact.
  It also places the field outside the citation-integrity check, so a dangling or mismatched reference goes undetected.
  The citation form keeps the raw view legible and navigable while the id remains authoritative and checkable.

- **A dual-key scheme: a human-legible tag beside a tool-minted stable id.**
  Requirements tooling has long paired a hand-chosen semantic tag (`REQ-AUTH-001`), which authors link by, with an auto-generated, refactor-stable machine id underneath, so a tool can re-map references when the tag is renamed.
  Rejected: it keeps the mutable, meaning-bearing key load-bearing at every authoring surface, so the failures this decision removes return through the front door.
  A tag embeds a classification that begins to lie when the artifact's subject drifts; sequential tags demand coordination, invite renumbering for readability, and collide under parallel authoring; and a tag rename still strands every citation held in an immutable surface, where no tool can re-map.
  The machine id underneath rescues only the surfaces a tool can rewrite.
  The benefit sought, a readable, quotable handle, is available without a second authoritative axis: the designation in `name` travels as every reference's visible text, and an adopter who wants a house tag records it as an alias (`aliases: [REQ-AUTH-001]`), resolvable for lookup and display while the opaque id remains the one citation.

## Driven by

- groundedIn: [Single Source of Truth](../principles/single-source-of-truth.md){id=note:principle:8691937}
- groundedIn: [Earned Substance](../principles/earned-substance.md){id=note:principle:yecemfe}
- groundedIn: [Proportionality](../principles/proportionality.md){id=note:principle:es0vhzn}
- groundedIn: [Shared, specific term meaning](../needs/shared-term-meaning.md){id=note:need:w3k8n6p}
- groundedIn: [Reuse established vocabulary before coining new terms](established-vocabulary-first.md){id=note:dec:8f3m5vk}
