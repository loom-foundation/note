---
id: note:dec:t4w8k2n
name: Terms and personas as first-class, scoped kinds
kind: decision
status: current
decided: 2026-06-12T00:00:00Z
---

A term and a persona are each a first-class artifact kind in the spine pack, carrying the uniform opaque identity every kind shares and participating in the scope graph and the cascade like other intent.
Each can be named once, referenced and cross-referenced by designation, inherited across scopes, specialized, or disinherited, and can mean different things in sibling scopes without collision.
The model is first-class and scoped; the storage is proportionate.

## Context

An actor and a meaning are each restated across artifacts when they have no kind of their own: a persona spelled into each need's field, a term entered in a flat register.
Both drift, a single-source-of-truth cost, and neither can be scoped: a flat field or a flat register cannot let a company-wide term or persona be inherited and specialized by a team, nor let two teams at the same level use one word for two meanings.

Scoped meaning is already an existing commitment with no mechanism: the terminology already holds that a term's meaning is determined by the context it appears in.
A larger organization with many self-sufficient teams needs exactly this, localized terms and personas that may inherit, decline to inherit, or specialize those defined higher in the hierarchy.

Term and persona are both spine-pack kinds: the spine is the default trace set every corpus carries, and a need's who and a corpus's load-bearing words are part of capturing intent in any sustained body of work, whether a software system, a hardware product, a process, or a methodology like this corpus.
Their identity is the uniform opaque grammar every kind shares, defined once in [Uniform opaque identity](identity-and-designations.md){id=note:dec:jhgkwja}; this decision makes them kinds and gives them scope, and rests on that grammar for how they are identified and referenced.

## Decision

- **Term and persona are first-class kinds.**
  Each is an artifact kind with the same identity, relation, lifecycle, and reference treatment as every other kind, not a line in a register or a string in a field.

- **Both are spine-pack kinds.**
  Term and persona ride the spine pack, the default set a corpus carries when it configures nothing, because a need's who and a corpus's load-bearing terms are part of the basic trace, not an opt-in family.

- **Uniform opaque identity.**
  A term and a persona each carry the opaque id every kind shares; no slug id exists.
  Their designation lives in `name`, with further designations in `aliases`, so they are referenced and cross-referenced by designation while a rename leaves the id untouched.

- **They participate in the scope graph and the cascade.**
  An inner scope inherits the terms and personas in force at the outer scopes that contain it, and may add to, replace, or disinherit them, the deviation visible and attributable.
  Two sibling scopes may define the same designation with different meaning without collision, because identity is opaque and scoped.

- **A reference resolves to the effective one at the referring scope.**
  A reference to a term or persona resolves to the effective artifact at the referring artifact's scope, computed by the cascade, not by a single global lookup.

- **The model is first-class and scoped; the storage is proportionate.**
  A small, single-scope corpus may author its terms compactly in one place and its personas in one place, never use scoping, and pay nothing, the combined register a derived view; a larger corpus splits and scopes them per team.
  The kind, the identity, and the scope participation are fixed here; the storage layout is a specification concern.

- **A need names its persona by reference.**
  A need's `persona` is a reference, or a list of references, to persona artifacts rather than free text.

## Forces and trade-offs

Fixing the kind, identity, and scope participation now while leaving the storage layout to specification is cheap to decide and expensive to retrofit: adding scoped identity to a flat field or register later would rewrite every reference's resolution.
Deciding the model now separates the irreversible choice from the mechanical one.

A flat persona field or a flat term register is lighter for a tiny corpus but structurally cannot scope; the model-versus-storage split keeps the light path available, author compactly with no scoping, while making the scoped path possible, split, inherit, specialize, without a second model.

Opaque identity means a designation a term or persona is cited by may change without breaking a reference: the designation lives in `name` and `aliases`, where it is rewritten freely, and the reference carries the id.

## Alternatives considered

- **Keep persona a free-text field and terms a flat register.**
  Rejected: both drift against Single Source of Truth, and neither can be scoped, which the organization-scale case requires.

- **Make them first-class but global, with no scope participation.**
  Rejected: it dedupes but still cannot express a company-wide term or persona inherited or specialized per team, nor sibling scopes using one designation for two meanings.

- **A readable slug id for terms and personas, on the reasoning that the word or name is the thing.**
  Rejected: it conflates a concept with its designation and re-creates the rename-strands-citations failure; a term and a persona carry the uniform opaque id, with the designation they are cited by held in `name` and resolved by lookup.

- **Force one file per term and per persona on every adopter.**
  Rejected against Proportionality: a small corpus should be able to author compactly, the combined register a derived view; the storage layout is a specification concern, not a fixed obligation.

## Driven by

- groundedIn: [Uniform opaque identity](identity-and-designations.md){id=note:dec:jhgkwja}
- groundedIn: [Kind-agnostic substrate and kind packages](substrate-and-kind-packages.md){id=note:dec:w4awceq}
- groundedIn: [Shared, specific term meaning](../needs/shared-term-meaning.md){id=note:need:w3k8n6p}
- groundedIn: [Shared, scoped persona](../needs/shared-persona.md){id=note:need:p9k4w3n}
- groundedIn: [Scope and inheritance](../requirements/system/scope-and-inheritance.md){id=note:req:96smmcv}
- groundedIn: [Earned Substance](../principles/earned-substance.md){id=note:principle:yecemfe}
