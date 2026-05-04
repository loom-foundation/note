---
id: note:dec:w4awceq
name: Kind-agnostic substrate and kind packages
kind: decision
status: current
decided: 2026-06-12T00:00:00Z
---

The method factors into a kind-agnostic substrate and a small set of kind packages (packs) that ride it.
The substrate is the universal machinery that knows nothing of any particular kind; a pack declares a coherent set of kinds, their fields, their body sections, and the relation endpoints they contribute.
A corpus names its enabled packs in its manifest, which is authoritative for what a checker validates.
The method ships built-in, method-defined packs only, at this decision the spine pack (default) and the discovery pack, since joined by the governance, record, and compliance packs through their own decisions; no adopter-authored pack mechanism and no author-facing vocabulary aliasing are offered.

## Context

A sustained body of work, whether a software system, a hardware product, a process, or a methodology like this corpus, captures its intent in artifacts of several kinds: a want, an obligation, a recorded choice, a defined term.
Which kinds are worth carrying is not universal.
A regulated systems-engineering effort leans on a sharp need-to-verification trace; a product-discovery effort leans on jobs, pains, gains, and the value that answers them; many efforts want neither in full.
A method that fixes one maximal kind set forces every Adopter to read past the kinds their context does not earn, and it cannot present itself to an Adopter with an entrenched kind-system as a recognition of what that Adopter already does.

The method already factors two of its three configuration concerns out of the kind definitions.
Rigor is factored into conformance profiles; the subject-versus-authoring split is factored into compartments.
The kinds themselves remained welded into a single format specification, so that adding, deferring, or regrouping a kind meant surgery on the one document that defines every kind at once, and kind availability was tangled into the rigor axis (the heaviest profile both raised rigor and switched on whole families of kinds).
Completing the factoring, kinds into packs, is the move this decision records.

The cost of the split lands at once: a pack mechanism to specify, a configuration axis for which packs are enabled, and kind-legality that is no longer readable from an artifact plus a single fixed kind list, because it now depends on which packs a corpus enabled.
The benefit, recognition for an Adopter with an established vocabulary of work products, serves Adopters the method has not yet met.
This decision keeps the split's first version disciplined so the cost stays small and the membrane is proven internally before it is ever opened to a third party.

## Decision

- **The substrate is kind-agnostic.**
  It carries the file envelope, the immutable identity scheme, the universal lifecycle, the typed-relation mechanism (a relation authored once on the dependent end, its inverse a derived view, the hierarchical edges acyclic), scope and cascade, the citation surfaces, and the guarantee that well-formedness is checkable from the files alone with no special tool.
  The substrate knows no kind: it does not name need, requirement, or term, and it fixes no kind-specific field or section.

- **A pack is a declarative selection of kinds.**
  A pack declares which kinds exist, each kind's id kind-segment, its required and optional frontmatter fields, its required and optional body sections, and the relation endpoints it contributes to the verb catalogue.
  One substrate carries many packs.
  A checker reads the enabled packs and validates kinds, fields, sections, and links from the files alone.

- **The manifest is authoritative.**
  A corpus declares its enabled packs in its manifest, alongside the other configuration the manifest already homes (the method version, the conformance profile, the vocabulary map, and the scope block).
  Everything that affects validation is read from the manifest; a directory layout may mirror configuration for navigation but never overrides it.

- **Built-in packs, method-reserved tokens.**
  The method ships the **spine** pack and the **discovery** pack, since joined by the **governance**, **record**, and **compliance** packs, each added by its own decision ([The governance pack](governance-pack.md){id=note:dec:59ptf2z}, [The record pack](record-pack.md){id=note:dec:hjv67df}, [The compliance crosswalk pack](compliance-crosswalk-pack.md){id=note:dec:ve053yf}).
  Their tokens are short, unnamespaced, and reserved by the method, so that the same token names the same kind set in every corpus.
  A corpus that configures nothing is on the spine pack.

- **A pack is closed over its relation endpoints.**
  Every verb row a pack declares has all of its endpoint kinds available whenever that pack is enabled, so an enabled pack can never produce an artifact whose required relation has no legal target.
  A kind whose only required relation reaches a kind in another pack belongs in that other pack.

- **A pack adds; it never subtracts.**
  Enabling a pack contributes kinds and endpoint rows, and it may discipline the vocabulary it itself introduces, but it never invalidates an artifact or an edge that is legal without it: the substrate and the spine stay valid whatever packs are enabled, so moving up a level never strands what came before.
  Where a pack's richer path supersedes a bare edge, the overlap is surfaced by report, never made ill-formed.
  The discovery pack's fit rule as first shipped broke this, outlawing a legal spine edge once an offering intervened, and was re-cut to additive form; the repair and its reasoning are recorded with the pack ([Offering, fit, and the value proposition](offering-fit-and-value-proposition.md){id=note:dec:cjqwsxt}).

- **Shared verbs are factored by contribution.**
  A verb whose endpoints span packs is not owned by one pack; each pack declares the endpoint rows it adds, and the effective verb catalogue for a corpus is the union of its enabled packs' rows.
  The verb's name, direction, and derived inverse are fixed by the substrate's relation grammar; a pack contributes endpoints, never new relationship semantics.

- **One job per configuration axis.**
  Kind availability lives only in packs.
  The conformance profile carries rigor only; it no longer switches kinds on or off.
  A kind is therefore gated by exactly one axis, the pack, removing the residue of a model where the heaviest profile also enabled the richest kinds.

- **No open pack mechanism, no author-facing aliasing, in this version.**
  The pack mechanism is specified, because the format specification splits along it, but no adopter-authored pack surface is offered and no mechanism lets an author rename a canonical kind or verb token.
  Opening the mechanism to third-party packs, and any house-vocabulary front-end, are recorded as deliberate non-goals of this version, so the door stays visibly open without the surface existing.

## Forces and trade-offs

Kind-legality is no longer a single fixed prior: a reader resolves it from the artifact plus the manifest's enabled packs rather than the artifact plus one kind list.
Keeping the packs built-in and closed bounds this cost, because the legal kinds in any corpus are still drawn from a set the method itself defines and publishes, not from an arbitrary adopter document a tool would have to fetch and trust.
The membrane between substrate and pack is real work to specify, paid once; it buys a format specification that splits cleanly into a substrate spec and one spec per pack, each checkable in isolation.

A fourth configuration axis (packs, beside profile, scope, and the vocabulary map) is one more thing an adopter sets and a tool reads.
The default absorbs most of the cost: an adopter who configures nothing gets the spine pack, the recommended profile, a single scope, and canonical tokens, and never sees the axes.

The closed, built-in stance is the cheapest reversible position.
Opening the mechanism later is an additive change; retracting an opened mechanism later would break every corpus that authored against it.

## Alternatives considered

- **One maximal kind set welded into the format specification.**
  Rejected: it forces every Adopter to carry kinds their context does not earn, cannot present the method as recognition to an Adopter with its own kind-system, and leaves kind availability tangled with rigor.

- **An open pack mechanism with Adopter-authored packs in the first version.**
  Rejected: with open packs, kind-legality and verb-legality stop being readable from an artifact plus the method's own specification; they require resolving an Adopter document, which erodes the no-special-tool floor and the shared priors an agent depends on, for a benefit no current Adopter is asking for.
  Recorded as a deliberate non-goal, to be opened only when a real second adopter demands it.

- **A house-vocabulary front-end that renames canonical kind and verb tokens for authors.**
  Rejected here: a two-vocabulary corpus breaks the property that a kind or verb token means the same thing in every corpus of the method, which is what makes a corpus safe to read cold.
  Display and input normalization is handled separately and at the tool layer by the vocabulary map, with committed files holding canonical tokens only.

- **Naming the default pack `standard`.**
  Rejected: it collides with the `standard` conformance profile, so one token would name two different axes.
  The default pack is the sharp trace spine, so `spine` names it plainly; the profile names are already in use, so the unsettled side renames.

## Driven by

- groundedIn: [Earned Substance](../principles/earned-substance.md){id=note:principle:yecemfe}
- groundedIn: [Proportionality](../principles/proportionality.md){id=note:principle:es0vhzn}
- groundedIn: [Single Source of Truth](../principles/single-source-of-truth.md){id=note:principle:8691937}
- groundedIn: [Compute and Report](../principles/compute-and-report.md){id=note:principle:6e7f28k}
- groundedIn: [Ceremony sized to the stakes](../needs/right-sized-ceremony.md){id=note:need:p7ekr3c}
- groundedIn: [Adopt without being stranded by the method's own evolution](../needs/adopt-without-being-stranded.md){id=note:need:x4zqfws}
- groundedIn: [Checkable well-formedness and identity](../requirements/system/checkable-well-formedness.md){id=note:req:sp8g0my}
- groundedIn: [File-native capture](../requirements/system/file-native-capture.md){id=note:req:mgdg9q0}
