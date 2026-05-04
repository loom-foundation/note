---
id: note:dec:yy8j83d
name: The system/Context overlap is deferred to allocation
kind: decision
status: current
decided: 2026-06-23T10:49:45Z
---

A design panel and an adversarial review examined whether the system-of-interest should be one artifact or two (merging the value-provider `system` node into the boundary `Context`, deriving provision away so neither is authored, or linking the two with an explicit edge) and found that none earns its place: the question is mis-posed.
The overlap a multi-system corpus shows between its `system` artifacts and its `Context` artifacts is a symptom of the deferred requirement allocation, not an independent defect, so [The system-of-interest provides the value](system-of-interest-provides-value.md){id=note:dec:swar6np} is retained unchanged and the system-to-Context relationship is resolved when allocation is taken up.

## Context

[The system-of-interest provides the value](system-of-interest-provides-value.md){id=note:dec:swar6np} added a discovery-pack `system` kind carrying a `provides` edge, and recorded two open questions this decision answers.
Its first observed that the `system` kind and the [Context](context-model.md){id=note:dec:b7w3k9n} kind overlap: a Context is authored once per System or Subsystem boundary, a service included, and a `system` is authored once per system-of-interest when more than one must be told apart, so a multi-system corpus authors both for each service, with no edge between them and two counting rules that can disagree: "itself the sign the node is mis-modeled".
Its fifth asked whether to author `provides` at all, or instead derive provision from the code scan that must run anyway, and deferred that to a proper deliberation.
This is that deliberation.

A sharper form of the overlap appears in a service-oriented product spread across repositories.
A service's `provides` edge runs from a node scoped inside its own narrowed boundary up to value scoped in the enclosing product's boundary, often in another repository, so provider and provided value sit at different scope levels and in different repositories.
That cross-level provision is allocation, a subsystem realizing an obligation of the system that encloses it, and `swar6np` deferred the `allocatedTo` edge that would carry it.

## Decision

- **The status quo is retained.**
  `swar6np` stands unchanged: a `system` node, authored only when more than one system-of-interest must be told apart, carrying an optional `provides` edge, with the single-system case keeping the system implicit in its one Context.
  Neither merging the `system` into the Context, nor deleting it in favor of derivation, nor adding a system-to-Context edge is adopted now.

- **The question "one artifact or two" is mis-posed.**
  Each candidate restructuring fails on a different axis, and each failure points at another candidate: a link between a count-invariant `system` and its Context becomes a rigid one-to-one pairing that argues for merging; a merged node forces a boundary that narrows downward and a provision that points upward onto one artifact; deriving provision away leaves a product-level value with no way to say which sibling provides it.
  The cycle closes on one place: the cross-level provision each is wrestling with is requirement allocation, which is deliberately deferred.
  The overlap is a symptom of that deferral, not a defect to be fixed ahead of it.

- **The non-edge between a `system` and its Context is not a single-source-of-truth violation.**
  The two artifacts make non-overlapping claims (one states a boundary, the other names provided value) so no fact is stored twice and nothing can drift between them.
  The single-source crack `swar6np` set out to close was the provider relationship carried by no edge, which `provides` already closes; an absent edge between non-overlapping artifacts is an open question, not a duplication.

- **The relationship is resolved downstream, with allocation.**
  When `allocatedTo` is taken up, that decision fixes where the provider-and-boundary relationship attaches (to the `system` node, or to the Context and scope) and the overlap resolves as a consequence, with a typed link earned at that point only if one is needed.

- **Deriving provision away is rejected as the answer to the fifth open question.**
  Provision computed from the code scan alone collapses the authored-claim-and-computed-evidence split `swar6np` rests on, the same split that keeps a value proposition an authored asset rather than only the computed fit.
  It also rests on the in-code and in-commit `@intent` citations, whose `Satisfies` and `Refs` keys are advisory and never checked, so the signal is unreliable exactly where a product-level offering must be attributed to one of several siblings.

## Forces and trade-offs

None of the three restructurings is proportionate to the defect.
The defect is a deferred open question on a kind that is optional and discovery-only.
The merge would re-mint the id of every Context in every corpus and widen the spine with a kind that is inert until the discovery pack loads; the derivation would trade an optional kind for a hard dependency on an unbuilt tool and on citation keys the method declares advisory; the link would tax every single-system discovery corpus with a node it gains nothing from, inverting the "common case pays nothing" that `swar6np` was careful to preserve.
The status quo is the only option whose blast radius matches the stakes.

The cost of waiting is that the overlap stays a known, recorded open question, and a multi-system author still has no crisp answer to "which systems do I list in this repository".
This is accepted: the question's triggering context (adoption beyond the dogfooding corpus, or the allocation decision itself) is not yet present, and resolving it now, on a kind this young, would commit the method to a structure before the force that should shape it has arrived.

## Alternatives considered

- **Merge: one system-of-interest node that subsumes the Context, promoted to the spine.**
  Rejected.
  It would re-mint the id of every Context artifact in every corpus, including spine-only corpora that never enable discovery; it re-creates the closure violation the pack model exists to prevent, a spine kind that is problem-space-only until the discovery pack makes it carry value; and its stated rationale, that a Context has no relations section, argues that neither kind should carry `provides`, not that the two should be fused.
  It also reads "a system-of-interest is individuated by its boundary" as "a system-of-interest is identical to its boundary", which the [System](../terms/system-and-boundary/system.md){id=note:term:0jbwfkm} term does not support.

- **Derive: delete the `system` kind and compute provision from the scan.**
  Rejected, as recorded in the decision above: it is the strong form of `swar6np`'s fifth open question, and it loses on the authored-claim-versus-computed-evidence split and on the advisory, never-checked citation keys it would have to trust.

- **Link: keep both artifacts and add a typed system-to-Context edge.**
  Not adopted now, though it is the least-broken of the three: it is the only one whose cross-pack mechanics hold, a discovery-to-spine edge being already precedented by the way an offering `addresses` a spine need.
  But it over-fixes, taxing the common single-system case with a mandatory node, and its claimed benefit (making the cross-level allocation computable by walking from a system through its Context's narrowing to the enclosing system) relies on narrowing being a traversable edge, when narrowing is a boundary comparison the cascade deliberately refused to reify.
  It is a candidate output of the allocation decision, not an input to be settled ahead of it.

## Reopening conditions

- Requirement allocation (`allocatedTo`) is taken up, or an adopter beyond the dogfooding corpus needs per-product allocation: re-pose the relationship with allocation as the frame and the linking edge a candidate output.
- A concrete case appears where a `system` and its Context store the same fact and silently diverge: the non-edge becomes a real single-source-of-truth violation, and the linking edge becomes the proportionate fix.
- The `provides` audit is built and proves untrustworthy without binding a system to its repository and a version to its commits: the forcing artifact is a deployment-manifest Record, not a change to the system-to-Context modeling.
- A real adopter cannot answer "which systems do I list in this repository" before allocation lands: the "node is mis-modeled" reading is confirmed on its own, and the count rule is revisited toward authoring one system per bounded scope.

## Driven by

- amends: [The system-of-interest provides the value](system-of-interest-provides-value.md){id=note:dec:swar6np}
- groundedIn: [Context model](context-model.md){id=note:dec:b7w3k9n}
- groundedIn: [Earned Substance](../principles/earned-substance.md){id=note:principle:yecemfe}
- groundedIn: [Proportionality](../principles/proportionality.md){id=note:principle:es0vhzn}
- groundedIn: [Single Source of Truth](../principles/single-source-of-truth.md){id=note:principle:8691937}
