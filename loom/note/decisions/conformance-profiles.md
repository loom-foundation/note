---
id: note:dec:cf7n2wq
name: Conformance profiles as pure rigor bundles
kind: decision
status: current
decided: 2026-06-12T00:00:00Z
---

A conformance profile is a pure rigor bundle: it says how much discipline a scope applies, and nothing about which kinds the scope may carry.
The method names three profiles on one rigor axis: `bare`, the floor; `standard`, full per-kind bodies and a decision record per design choice; and `strict`, the opt-in disciplines of term rigor, typed term relations, EARS phrasing, verifications, and specification authority.
Adoption is monotonic: raising a scope's profile never invalidates an artifact that was valid under a lighter one.
Kind availability lives only in packs, never in a profile, so each axis does exactly one job.

## Context

A sustained body of work, whether a software system, a hardware product, a process, or a methodology like this corpus, adopts the method at a level of rigor sized to its stakes ([Ceremony sized to the stakes](../needs/right-sized-ceremony.md){id=note:need:p7ekr3c}).
A high-stakes effort wants term inclusion tests, EARS-phrased requirements, and verifications on its obligations; a small or early effort wants a valid envelope and a lead and little more.
The profile is how a scope declares that level, and tiered conformance fixes that a corpus has a minimal core with every other discipline opt-in, additive, and overridable per scope ([Tiered conformance](../requirements/system/tiered-conformance.md){id=note:req:bth0rxp}).

The substrate split changes what a profile may carry.
Kind availability is now the pack axis: which kinds a corpus may carry is fixed by its enabled packs, and the manifest is authoritative for that ([Kind-agnostic substrate and kind packages](substrate-and-kind-packages.md){id=note:dec:w4awceq}).
A profile that also switched kinds on would gate the same kinds the pack axis gates, with no precedence rule between them.
The discipline this decision applies is one job per axis: the profile carries rigor only, the pack carries availability only, so a kind is gated by exactly one axis and a reader resolves each concern from one place.

## Decision

- **A profile is a pure rigor bundle.**
  A profile says how much discipline a scope applies and nothing about which kinds exist.
  Kind availability is the pack axis exclusively; the profile never switches a kind on or off.

- **Three profiles on one rigor axis.**
  - **`bare`**, the floor: a well-formed envelope, the common required frontmatter, the per-kind required frontmatter, and a lead.
    Enough to be a valid corpus, and where an early or brownfield scope starts.
  - **`standard`**: full per-kind bodies, and a decision record for each design choice.
    Real traceability without the heaviest rigor.
  - **`strict`**: term inclusion tests and Origins, typed term relations, EARS phrasing on requirements, verifications expected on current requirements, and an independent-authority declaration on specifications.
    The opt-in disciplines, layered on top of `standard`.

- **One job per axis.**
  A profile gates rigor; a pack gates kind availability.
  Nothing in a profile turns a kind on, and nothing in a pack raises rigor.
  A kind is therefore reached through exactly one axis, its pack, and a discipline is reached through exactly one axis, its profile.

- **Adoption is monotonic.**
  Raising a scope's profile never invalidates an artifact that was valid under a lighter one: each profile is a superset of the disciplines below it, so a `bare`-valid artifact stays valid at `standard` and a `standard`-valid artifact stays valid at `strict`.
  A scope may raise or lower its profile freely; the monotonic ordering guarantees a raise only ever adds obligations, never breaks existing artifacts.

- **The profile is per scope.**
  The manifest sets the corpus default, and any scope may declare its own profile, adopting more or less rigor than its parent.
  A monorepo gives a brownfield app `bare` and a mature service `strict`, each at its own scope.

## Forces and trade-offs

Separating rigor from availability removes the one place the old model gated the same kinds twice.
With kind availability on the pack axis and rigor on the profile axis, no precedence rule is needed between them, because they never gate the same thing: a reader asking which kinds exist reads the packs, and a reader asking how much rigor applies reads the profile.
The cost is that an adopter sets two axes where one knob once looked simpler; the default absorbs it, since a corpus that configures nothing gets the spine pack and the recommended profile and never sees either axis.

Three points on one rigor axis name the common rigor levels without a fourth preset.
A scope that wants some but not all of the `strict` disciplines is served by the per-scope freedom and the monotonic ordering, not by a new bundle.

Keeping adoption monotonic lets a scope climb the rigor ladder over time without a migration: raising the profile adds checks, and every artifact valid below stays valid above.
The cost is that each profile must be a true superset of the one below, which is the property that makes the climb safe.

## Alternatives considered

- **A profile that bundles both rigor and kind availability (the prior model).**
  Rejected: with availability now on the pack axis, a profile that also switched kinds on would gate the same kinds the packs gate, with no precedence rule between the two axes.
  One job per axis removes the overlap: the profile carries rigor, the pack carries availability.

- **Gate the discovery kinds and the principle layer through the heaviest profile.**
  Rejected: the kinds the old heaviest bundle switched on, the offering and value-proposition layer and the principle layer, are now the discovery and spine packs, reached through the pack axis.
  A profile gating them would re-tangle availability into rigor, the exact knot this split undoes.

- **A general a-la-carte profile beside the three presets.**
  Rejected: the three presets are points on one rigor axis, and per-scope freedom with the monotonic ordering already lets a scope sit at any of them; a free-form subset profile adds a configuration surface the rigor axis does not need.

- **Naming the top profile `full`.**
  Rejected: `full` implies the lighter profiles are incomplete rather than deliberately lighter; `strict` names the actual differentiator, which is rigor.

## Driven by

- groundedIn: [Kind-agnostic substrate and kind packages](substrate-and-kind-packages.md){id=note:dec:w4awceq}
- groundedIn: [Tiered conformance](../requirements/system/tiered-conformance.md){id=note:req:bth0rxp}
- groundedIn: [Proportionality](../principles/proportionality.md){id=note:principle:es0vhzn}
- groundedIn: [Ceremony sized to the stakes](../needs/right-sized-ceremony.md){id=note:need:p7ekr3c}
