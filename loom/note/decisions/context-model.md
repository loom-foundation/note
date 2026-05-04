---
id: note:dec:b7w3k9n
name: Context model
kind: decision
status: current
decided: 2026-06-03T19:00:11Z
---

A Context, the system boundary, is inherited and narrowed monotonically down the scope graph: a subsystem may narrow the boundary it inherits, never widen it, and a widening is a visible, attributable deviation.

Context is kept strictly separate from Scope and Cascade: they are different graphs over the same artifacts and share only the cascade mechanism, and a Scope is not necessarily a Context: a Context is authored once per scope that has a distinct inside and outside, never for a cross-cutting scope or a boundary-less leaf.

A single boundary statement is the default; splitting it into a business view and a technical view is a profile-gated opt-in.

## Context

The Context kind left three questions open: whether a Context cascades and how; whether Context should be kept distinct from Scope and the Cascade or folded into them; and whether a boundary should be a single statement or always split into a business view and a technical view.

Each had a cheap wrong answer (independent restatement that drifts, one concept that masquerades as another, a heavy split mandated everywhere), so the model is ratified here before the boundary format is specified.

## Decision

- **A Context cascades by monotonic narrowing.**
  A subsystem inherits its supersystem's Context and may only narrow it (drop external entities, tighten what crosses the boundary), never widen it.
  A widening is a visible, attributable deviation, treated like the removal of an inherited obligation ([Visible, attributable deviation](../requirements/system/visible-attributable-deviation.md){id=note:req:64eknb1}).
  Narrowing a boundary is the same operation as a cascade strengthening, so the cascade keeps one mental model, not two.
  For a boundary the loud direction is widening, the inverse of the rule for an obligation, where the loud direction is removal: narrowing exposure (dropping an external entity, tightening what crosses) makes the system smaller and is the safe, silent strengthening, while widening exposure is the visible, attributable deviation.
  This does not collide with the cascade rule that a removed obligation is always loud ([Cascade conflict resolution](cascade-conflict-resolution.md){id=note:dec:9c4tk2n}).
  A Context and the obligations that constrain what crosses it are separate graphs (below), so narrowing a Context never removes an obligation; disinheriting an obligation that governed a now-dropped crossing is a distinct act on the cascade and stays loud.
- **A Context is authored once per scope that has a boundary.**
  A scope that is a System or a Subsystem (an organization, an application, a service) has its own Context and narrows what it inherits; a cross-cutting scope (a security, privacy, or residency domain) and a leaf component with no boundary of its own author none, and each reads the inherited effective Context.
  This is neither one Context per project (too coarse for a monorepo of several apps) nor one per component (too fine); the test for whether a scope gets its own Context is whether it stands as a coherent whole with an inside distinct from its environment (a System or a Subsystem), not a cross-cutting concern that spans systems or a leaf that is not decomposed further.
- **Context is strictly separate from Scope and Cascade.**
  Context (a black box with ports: inside, outside, what crosses) and Scope (the position in the inheritance graph) are different graphs over the same artifacts; they share only the cascade mechanism, not the concept.
  In particular, a Scope is not necessarily a Context: a cross-cutting scope (a security, privacy, or residency domain) carries obligations but has no inside or outside boundary, and forcing it to have one would make one concept masquerade as the other.
- **One boundary by default; the business and technical split is profile-gated.**
  A single boundary statement is the conformance floor.
  A scope may turn on a two-view split (a business or domain boundary and a technical or system boundary) where actors and value exchanges are load-bearing, typically at the top scopes that face Legal, Finance, or external parties.
  The split is dead weight at a leaf service and shall not be mandated there.

## Forces and trade-offs

- Monotonic narrowing makes a widened boundary impossible to introduce silently: the only way to take on more than the parent allows is a loud deviation, which is where audit attention belongs.
  The cost is that a genuinely re-scoped subsystem, which is rare, must record a deviation rather than restate freely; accepted, because silent restatement is the drift failure by construction.
- Strict separation keeps two honest concepts from collapsing into a leaky one.
  The cost is that a reader holds both graphs; mitigated because they share the single cascade mechanism, so only the concepts differ, not the machinery.
- Profile-gating the split keeps the floor light and lets the heavy model be earned.
  The cost is a profile knob, accepted because it is the same tier mechanism the Context kind already implies ([Tiered conformance](../requirements/system/tiered-conformance.md){id=note:req:bth0rxp}).

## Alternatives considered

- **State each subsystem boundary independently, with no cascade.**
  Rejected: independent restatement is the drift failure by construction; two boundaries that should agree will diverge with no signal.
- **Inherit then fully override.**
  Rejected: it is independent restatement with latency, and it permits silent widening, which monotonic narrowing exists to prevent.
- **Fold Context into Scope as one concept.**
  Rejected: a cross-cutting scope has no boundary; conflating them forces an obligation domain to masquerade as a boundary, or a boundary to masquerade as a scope.
- **Always present two boundary views.**
  Rejected against proportionality: the business and technical split earns its keep at top scopes but is dead weight at a leaf service (tokens in, ledger events out).

## Driven by

- groundedIn: [Visible, attributable deviation](../requirements/system/visible-attributable-deviation.md){id=note:req:64eknb1}
- groundedIn: [Cascade conflict resolution](cascade-conflict-resolution.md){id=note:dec:9c4tk2n}
- groundedIn: [Tiered conformance](../requirements/system/tiered-conformance.md){id=note:req:bth0rxp}
