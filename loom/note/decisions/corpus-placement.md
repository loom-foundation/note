---
id: note:dec:q2v7nk3
name: Adopter corpus placement
kind: decision
status: current
decided: 2026-06-12T00:00:00Z
---

An adopter who brings the method into their own repository places the corpus, by default, under a single `loom/` umbrella at the repository root, with each Layer nested beneath it (`loom/note/`, `loom/plan/`, `loom/guild/`).
A reader or a tool finds the corpus through a two-step discovery algorithm: read `loom.md` at the repository root if it is present and follow its `root:` field; otherwise use `loom/`.
Placement stays non-normative: identity and resolution are location-independent, and the authoritative scope lives in frontmatter, so a move never breaks a reference.
Recognized fallbacks are carried forward for repositories the default does not suit: a hidden `.loom/` with the same internal layout for a brownfield repository, and bare placement recognized wherever a Layer's manifest sits, by the layer-root rule.

## Context

The method already fixes that every artifact is one Markdown file with frontmatter, that identity is a durable opaque id and the directory layout is a derived convenience ([Uniform opaque identity](identity-and-designations.md){id=note:dec:jhgkwja}), and that every read and author operation is possible with no special tool ([Universal participation](../requirements/stakeholder/universal-participation.md){id=note:req:j4kecn7}; [File-native capture](../requirements/system/file-native-capture.md){id=note:req:mgdg9q0}).
It leaves open where an adopter puts the corpus inside their own repository, and how a reader or a tool finds it.

The corpus is no longer a single body of intent.
It is a set of Layers, each a coherent concern riding the one substrate, with note live, plan deferred, and guild reserved ([The layer model](loom-layers.md){id=note:dec:p13e5ay}).
A placement that named only the intent corpus cannot anchor a whole-system tree of several Layers; the umbrella that holds them is the anchor an adopter and an agent reach for.

Because identity and resolution are location-independent, the question is navigation, not correctness: a reference resolves wherever the file sits, so this decision recommends conventions and recognizes alternatives rather than making location load-bearing.
What it must add is a deterministic way to find the umbrella, including the case where a repository cannot place it at the obvious spot, so a tool and an unaided reader agree on which tree is the corpus.

## Decision

- **Default home: the `loom/` umbrella, Layers nested beneath.**
  At the repository root, a single `loom/` directory holds the enabled Layers, each in its own subdirectory: `loom/note/` for the live intent Layer, `loom/plan/` for the deferred plan Layer, `loom/guild/` for the reserved roles Layer.
  Each Layer holds its own manifest and its own kind subdirectories beneath its root.
  One umbrella entry at the adopter's root anchors the whole system, and a free corpus view (`ls loom/note/decisions/`) reads without a tool.

- **Two-step discovery, stated as an algorithm.**
  A reader or a tool finds the corpus by two steps in order:
  1. If `loom.md` is present at the repository root, read it and follow its `root:` field to the umbrella's location.
  2. Otherwise, use `loom/` at the repository root.
  Step one is the override for a repository that cannot place the umbrella at `loom/`; a tool or agent that skips it indexes the wrong tree in exactly the collision case the override exists for, so the steps run in order, the explicit override first.

- **Placement stays non-normative; scope is authoritative in frontmatter.**
  Identity and resolution are location-independent, so a move never breaks a reference and multiple placements may coexist in one repository, all equivalent to a tool.
  Directory containment may mirror the Scope DAG as a reading convenience, but the authoritative scope is recorded in frontmatter, and the directory tree expresses at most the single structural parent; cross-cutting and multi-parent edges are always carried by id ([Scope and inheritance](../requirements/system/scope-and-inheritance.md){id=note:req:96smmcv}).

- **A layer-root is wherever a Layer's manifest sits.**
  The unit of placement is the layer-root, defined as the directory holding that Layer's manifest ([The layer model](loom-layers.md){id=note:dec:p13e5ay}).
  The recommended `loom/<layer>/` nesting is the navigational mirror of an enabled Layer, never the switch; the manifest is authoritative for whether a Layer is enabled and for everything that affects validation ([Kind-agnostic substrate and kind packages](substrate-and-kind-packages.md){id=note:dec:w4awceq}).
  Bare placement, a layer-root that sits somewhere other than under `loom/`, is recognized by this rule alone.

- **Recognized fallbacks for repositories the default does not suit.**
  Because placement is non-normative, an adopter may instead use, and a tool indexes identically:
  - **Hidden `.loom/`** with the same internal Layer layout, for a brownfield repository that cannot take a visible root entry.
    One directory, named for the method, holding the same `note/`, `plan/`, and `guild/` Layers it would hold when visible.
  - **Bare placement**, a layer-root that sits outside any `loom/` umbrella, recognized through the layer-root rule because the manifest, not the location, is what enables the Layer.

- **A tool keeps its own space, never a Layer.**
  A tool's generated and operational state lives in the tool's own hidden directory, never under `loom/` and never inside a Layer; the corpus is the adopter's primary work product and stays out of the tool's space.

## Forces and trade-offs

- The `loom/` umbrella over a per-Layer scatter gives an adopter and an agent one whole-system anchor: the place to look for the entire body of work, intent and plan and roles together, rather than three unrelated entries.
  The cost is one root entry, held to exactly one by the single umbrella.

- A two-step discovery algorithm over a fixed location keeps the umbrella findable even where a repository cannot place it at `loom/`, at the cost that a tool must check for `loom.md` before falling back.
  Accepted: the explicit `root:` override is the only way a brownfield or otherwise constrained repository can move the umbrella without breaking discovery, and skipping the check is precisely the failure that indexes the wrong tree.

- Keeping placement non-normative, with the manifest authoritative and containment a mere mirror, preserves location-independence so a move never breaks a reference.
  The cost is that the tree shows only the spanning tree of the Scope DAG, so multi-parent and cross-cutting edges must be read from frontmatter or reconstructed by a tool.

## Alternatives considered

- **A content-named intent directory as the default, naming only the intent corpus.**
  Rejected: it anchors one Layer, not the whole system, and offers no umbrella for the plan and guild Layers that ride the same substrate.
  The whole-system anchor an adopter and an agent reach for is the umbrella, so the umbrella is the default.

- **Folder presence as the rule for what is enabled (the folders are the list).**
  Rejected: it cannot express a non-normative placement and would declare no Layer enabled wherever the umbrella is absent, including a corpus that places its Layers outside `loom/`.
  The manifest is the switch and the layer-root rule recognizes bare placement; the folder is the mirror.

- **A fixed `loom/` location with no override.**
  Rejected: a repository that cannot take a `loom/` entry at the root, a brownfield tree or one with a conflicting directory, would have no way to relocate the umbrella and stay discoverable.
  The `loom.md` `root:` override is the first discovery step precisely so the umbrella can move without breaking the algorithm.

- **Making directory location normative (path determines scope).**
  Rejected: it trades away location-independence, so a move would break resolution; containment stays a convenience with frontmatter authoritative.

- **Putting the corpus under the tool's hidden directory.**
  Rejected: it conflates the method's primary work products with the tool's disposable output and ties the corpus to one tool.
  The corpus never lives in a tool's space.

## Worked example

This project applies the override step: a `loom.md` at the repository root carries `root: corpus/note/loom`, pointing discovery at the umbrella inside the Note package, whose note-layer root is `corpus/note/loom/note/`.
The override keeps the whole Note method (corpus, docs, and licensing) self-contained in one subtree of a repository that hosts more than one Loom instance; the Sett corpus nests its own layer at `corpus/sett/loom/note/`, recognized through the layer-root rule.
An adopter starting fresh uses the `loom/` umbrella at the repository root and needs neither the override nor the rule.

## Driven by

- groundedIn: [The layer model](loom-layers.md){id=note:dec:p13e5ay}
- groundedIn: [Kind-agnostic substrate and kind packages](substrate-and-kind-packages.md){id=note:dec:w4awceq}
- groundedIn: [Uniform opaque identity](identity-and-designations.md){id=note:dec:jhgkwja}
- groundedIn: [Single Source of Truth](../principles/single-source-of-truth.md){id=note:principle:8691937}
- groundedIn: [Proportionality](../principles/proportionality.md){id=note:principle:es0vhzn}
- groundedIn: [Adopt the method on a system that already exists](../needs/brownfield-adoption.md){id=note:need:b3k9w2t}
- groundedIn: [Adopt without being stranded by the method's own evolution](../needs/adopt-without-being-stranded.md){id=note:need:x4zqfws}
- groundedIn: [Scope and inheritance](../requirements/system/scope-and-inheritance.md){id=note:req:96smmcv}
- groundedIn: [Universal participation](../requirements/stakeholder/universal-participation.md){id=note:req:j4kecn7}
- groundedIn: [File-native capture](../requirements/system/file-native-capture.md){id=note:req:mgdg9q0}
