---
id: note:dec:mf3k9w2
name: The corpus manifest
kind: decision
status: current
decided: 2026-06-12T00:00:00Z
---

A corpus declares its corpus-level configuration in a manifest at its layer-root.
The manifest is configuration, not intent: it carries no durable id and no kind, because nothing needs, verifies, or references it as an artifact.
Its field set is `methodVersion`, required; `namespace`, the corpus's namespace and the identity-space boundary, required; `opaqueLength`, the optional opaque id length, default seven; `profile`, the conformance profile; `packs`, the enabled kind packages; the `vocabulary` map; the scope block; and, on a multi-root corpus's root manifest, `roots`, the member repositories that compose it.
The manifest is authoritative for everything that affects validation: a directory layout may mirror its declarations for navigation, but never overrides them.

## Context

A corpus has to declare facts about itself that no single artifact owns: which version of the method it targets, how much rigor it adopts, which kinds it carries, what house words it fronts the method's tokens with, and how its scopes relate.
These are corpus-level facts, and they have one home.

The manifest is that home, and it must be readable without any tool, by the no-special-tool floor ([File-native capture](../requirements/system/file-native-capture.md){id=note:req:mgdg9q0}; [Universal participation](../requirements/stakeholder/universal-participation.md){id=note:req:j4kecn7}).
A tool's own operational state, its caches and locks and fetch sources, lives in the tool's hidden space; the manifest is the corpus's space and is read whether or not the tool is present.

The substrate split sharpens what the manifest must carry and what authority it holds.
Kind availability is now configured by the enabled packs, rigor by the profile, vocabulary by the map, and scope by the scope block, and the substrate fixes that the manifest is authoritative for all of it: everything that affects validation is read from the manifest, and a folder layout mirrors but never overrides it ([Kind-agnostic substrate and kind packages](substrate-and-kind-packages.md){id=note:dec:w4awceq}).
This decision records that the manifest is the configuration home, names its field set, and keeps the ratified framing that the manifest is configuration and not intent content.

## Decision

- **The manifest is configuration, not intent.**
  The manifest carries no durable id and no `kind`, because it is corpus configuration, not an intent artifact: nothing needs it, verifies it, or references it as an entity.
  This is the Earned Substance reasoning that keeps a plain group overview out of the kind system; a manifest earns no first-class identity.

- **The manifest is authoritative for validation.**
  Everything that affects what a checker validates is read from the manifest.
  A directory layout may mirror the manifest's declarations for navigation, a layer-root folder reflecting an enabled Layer for instance, but the mirror never overrides the manifest: where the folder and the manifest disagree, the manifest governs.

- **The field set.**
  The manifest carries:
  - **`methodVersion`** (required): the single version string for the method version the corpus targets.
    It is required; a corpus always declares the version it is written against.
  - **`namespace`** (required): the corpus's namespace, the identity-space prefix every artifact's id carries, declared once and the same across every repository the corpus spans.
  - **`opaqueLength`** (optional, default seven): the length of the opaque id segment minted in this corpus, set once on a multi-root corpus's root manifest and sized for the whole namespace.
  - **`profile`**: the conformance profile the corpus adopts, the rigor bundle evaluated against.
  - **`packs`**: the enabled kind packages, which fix the kinds the corpus may carry.
  - **the `vocabulary` map**: the optional house-term-to-canonical-token map for display and input normalization.
  - **the scope block**: the per-scope identity and parent edges that build the cascade graph.
  - **`roots`** (optional, on a multi-root corpus's root manifest): the member repositories that compose the corpus, each carrying its own manifest under the same namespace ([The multi-root corpus](multi-root-corpus.md){id=note:dec:0n14gqx}).

- **It is tool-agnostic and read without a tool.**
  The manifest is plain, readable text an unaided actor or any downstream tool reads without the method's tool.
  It is distinct from a tool's own operational configuration, which holds the tool's fetch sources, resolved-version lock, and cache; that state is the tool's space, and the manifest is the corpus's.

- **It sits at the layer-root.**
  A Layer's manifest sits at that Layer's layer-root, and its presence there is what makes the Layer's placement recognizable ([The layer model](loom-layers.md){id=note:dec:p13e5ay}; [Adopter corpus placement](corpus-placement.md){id=note:dec:q2v7nk3}).
  A scope within the corpus may carry its own manifest at its scope root, declaring the scope block and any per-scope configuration, with the layer-root manifest setting the default.

## Forces and trade-offs

Making the manifest authoritative for validation gives every configuration axis, version, profile, packs, vocabulary, and scope, one home a checker reads, rather than scattering them across folder conventions a tool would have to infer.
The cost is that a reader cannot always tell a corpus's configuration from its directory tree alone and must read the manifest; accepted, because the folder is a mirror and a mirror that could override its source would be a second source of truth.

Keeping the manifest configuration rather than a first-class artifact holds the kind system to things that are needed, verified, or referenced.
A manifest is none of those: it is read by a checker as configuration, not cited by an artifact as intent, so giving it an id and a kind would be ceremony the model does not earn.

Keeping `methodVersion` required guarantees every corpus declares the version it is written against, so a tool and an agent always know which method version's rules to apply.
The cost is one obligatory field; accepted, because a corpus with no declared version cannot be validated against a known rule set.

Placing the manifest in the corpus rather than in a tool's space keeps the configuration readable without the tool, at the cost of two configuration locations: the tool-agnostic manifest, what the corpus targets, and the tool's own operational state, how the tool fetches and caches.
The split is honest: one is a method declaration, the other is tool operation.

## Alternatives considered

- **A first-class manifest kind with a durable id.**
  Rejected against Earned Substance: nothing needs, verifies, or references the manifest as an entity; it is configuration, not intent, so a durable id would be unearned ceremony.

- **Put the configuration in a tool's own operational file.**
  Rejected: that file is the tool's space, and these declarations must be readable without the tool; a corpus declares its own version, profile, packs, vocabulary, and scope whether or not any tool is present.

- **Let the directory layout be authoritative, with the manifest a convenience.**
  Rejected: a folder that overrode the manifest would be a second source of truth for what a checker validates, and a move or a mislabeled folder could then silently change a corpus's legal kinds.
  The manifest governs; the folder mirrors.

- **Omit `methodVersion` and infer the version from the tooling.**
  Rejected: a corpus that does not declare its target version cannot be validated against a known rule set, and inferring the version from whichever tool happens to read it ties the corpus's meaning to that tool.
  The version is a required corpus-level declaration.

## Driven by

- groundedIn: [Kind-agnostic substrate and kind packages](substrate-and-kind-packages.md){id=note:dec:w4awceq}
- groundedIn: [The layer model](loom-layers.md){id=note:dec:p13e5ay}
- groundedIn: [Single Source of Truth](../principles/single-source-of-truth.md){id=note:principle:8691937}
- groundedIn: [Earned Substance](../principles/earned-substance.md){id=note:principle:yecemfe}
- groundedIn: [File-native capture](../requirements/system/file-native-capture.md){id=note:req:mgdg9q0}
- groundedIn: [Universal participation](../requirements/stakeholder/universal-participation.md){id=note:req:j4kecn7}
