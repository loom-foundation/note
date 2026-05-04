---
id: note:dec:4g730rg
name: Conventions as a first-class kind
kind: decision
status: current
decided: 2026-06-12T00:00:00Z
---

A convention is a first-class artifact kind: an agreed, all-or-nothing coordination rule whose content is arbitrary among workable alternatives and binding because agreed.
It carries the uniform opaque identity every kind shares, rides the spine pack, cascades like any other intent, is verifiable, and is exempt from the solution-free rule by kind, because the agreed mechanism is its substance.

## Context

A convention, in Lewis's sense, is an arbitrary but self-sustaining solution to a recurring coordination problem: any of the workable options would serve, and the value lives in everyone holding the same one.
Software practice runs on them: casing schemes, commit formats, layout rules, prose style.

The kind system's guards leave a convention with no home of its own.
The solution-free rule bars a functional or non-functional requirement from naming a mechanism, and a convention's entire content is a mechanism.
A constraint may carry a mechanism only when an external force imposes it, and a self-imposed convention has none; filing it as a constraint would be the leaked solution the rule exists to catch.
A specification commits the design that satisfies a requirement, which fits boundary-observable conventions but not the rules that bind the making of artifacts rather than the system.
A decision record holds the why of a choice, once, not the living rule that is scoped, inherited, and checked.
What remains is prose outside the kind system, a style guide, a contributor document, a methodology meta file, which gives no scope, no cascade, no fit, and no verification: a rule written nowhere it binds.

The single home this pain points to is a kind whose own pain is recorded in the discovery layer: a convention erodes without an authored home, and the value-side artifacts that name that pain and the relief a convention provides cite this kind by id from their own ends.

## Decision

- **A convention is a first-class artifact kind.**
  One coordination rule per artifact, stated declaratively in the present tense; it may name the mechanism, format, or style it fixes.
  It carries no *shall*: a convention binds the making of artifacts by agreement, not the system by obligation.

- **Exempt from the solution-free rule by kind.**
  The arbitrary mechanism is the substance of the agreement.
  The guard on requirements is untouched: a mechanism backed by neither an external force (a constraint) nor a recorded agreement (a convention) remains a leaked solution.

- **Uniform opaque identity.**
  A convention's id is the opaque grammar every kind shares, defined once in [Uniform opaque identity](identity-and-designations.md){id=note:dec:jhgkwja}; no slug id exists.
  A convention's designation lives in its `name`, with further designations in `aliases`; a rename leaves the id untouched and strands no citation, including one held in an immutable surface such as a commit trailer.
  This matters for conventions because sibling scopes legitimately hold same-named conventions with different content, which opaque, scoped ids keep collision-free, and an agent resolves an opaque id without any rename-forwarding discipline.

- **Rides the spine pack.**
  The convention kind is part of the spine pack, the default set a corpus carries when it configures nothing, so it is available wherever the spine is enabled; whether a corpus authors any conventions is the adopter's choice.

- **Body shape.**
  A required lead stating the practice; an optional `## Rationale` for the coordination value where the weighing is not already a decision record; an optional `## Relations` carrying `enacts` to the principle the convention serves, where one grounds it.
  The schema rows are fixed in the spine pack specification.

- **The agreement is the authority.**
  Where alternatives were genuinely weighed, a decision record carries the why and the convention names it through its own `decidedBy`; a lightweight convention may rest on review alone, by Proportionality.

- **Conventions cascade.**
  A convention is intent: stated once at the scope it governs, inherited by the scopes beneath, strengthened silently, and replaced or removed only as a visible, attributable deviation.

- **Conventions are verifiable.**
  A verification may verify a convention; conventions are the most mechanically checkable intent in the model, and a derived lint configuration is the natural downstream view of one.

## Forces and trade-offs

A new kind must clear Earned Substance, and convention does on the three-consumers test that admitted the value proposition: it is referenced (reviews and deviations cite the rule they honor or break), it is the single source that style guides, contributor documents, and lint configurations otherwise restate and drift from (with the kind, those surfaces become derived views), and it is verifiable against, mechanically.

The cascade payoff is the differentiating one: an organization states a convention once, every team inherits it, and the only way out is a loud, attributed, reasoned deviation.
That is the state-a-shared-obligation-once machinery applied to the rules that erode fastest under machine-speed contribution.

Opaque identity costs a readable handle in the id position and buys durability, the same trade every kind already takes; the designation in `name` carries the meaning, refreshed in every reference's link text.

The register invites one abuse: smuggling a requirement in as a convention to dodge the solution-free rule.
The inclusion test in the convention term is the guard: a rule whose content matters intrinsically, rather than by agreement among workable equals, is not a convention.

## Alternatives considered

- **Widen the constraint type to accept a recorded internal agreement as its source.**
  Rejected: it overloads a term the INCOSE lineage reads as externally bound, blunts the leaked-solution guard inside the requirement kind, and leaves practice rules wearing a system-obligation register that does not fit them.

- **Capture conventions as specifications.**
  Rejected as the general home: it fits only boundary-observable conventions, a specification exists to satisfy a requirement, and demanding a requirement-plus-specification pair for a casing rule is unearned ceremony.

- **Keep conventions in methodology meta and adopter style guides.**
  Rejected: prose homes give no scope, no cascade, no fit, and no verification; the erosion pain is that arrangement's signature.

## Driven by

- groundedIn: [Uniform opaque identity](identity-and-designations.md){id=note:dec:jhgkwja}
- groundedIn: [Kind-agnostic substrate and kind packages](substrate-and-kind-packages.md){id=note:dec:w4awceq}
- groundedIn: [Principles as a first-class kind](principles-first-class.md){id=note:dec:eym5t5g}
- groundedIn: [State a shared obligation once](../needs/state-obligation-once.md){id=note:need:257yf29}
- groundedIn: [Scope and inheritance](../requirements/system/scope-and-inheritance.md){id=note:req:96smmcv}
- groundedIn: [Visible, attributable deviation](../requirements/system/visible-attributable-deviation.md){id=note:req:64eknb1}
- groundedIn: [Earned Substance](../principles/earned-substance.md){id=note:principle:yecemfe}
- groundedIn: [Single Source of Truth](../principles/single-source-of-truth.md){id=note:principle:8691937}
- groundedIn: [Proportionality](../principles/proportionality.md){id=note:principle:es0vhzn}

## Worked example

An adopter's convention, in full:

```markdown
---
id: acme:conv:7kx4m2p
name: snake_case field names
kind: convention
status: current
---
API field names are snake_case, in every payload the platform serves.

## Rationale

Either casing would serve; mixed casing serves no one.
One shape to read, one shape to grep, one shape for agents to follow.
```

A review cites it by id; a team that must mirror a vendor's camelCase records a loud, attributed deviation at its own scope; the lint rule that enforces the casing is generated from the artifact, never authored beside it.
When the platform later renames the convention, every citation in immutable history still resolves, because the id never carried the name.
