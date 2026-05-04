---
id: note:dec:4tzn3av
name: The default spine pack
kind: decision
status: current
decided: 2026-06-12T00:00:00Z
---

The method's default built-in pack is the spine pack: the sharp, V-model-shaped trace spine and the kinds that anchor it.
Its kinds are need, requirement, specification, decision, verification, acceptance-criterion, term, persona, convention, principle, and context.
It is the strongly recommended default; a corpus that configures nothing is on the spine pack, and it is the kind set against which every other configuration is a deliberate addition.
The discovery kinds, the risk kind, and the plan pack are not in the spine; they ride separate packs, designed or deferred.

## Context

A sustained body of work, whether a software system, a hardware product, a process, or a methodology like this corpus, needs one kind set it can adopt without choosing, and that set has to be the one most efforts earn.
The substrate carries no kind ([Kind-agnostic substrate and kind packages](substrate-and-kind-packages.md){id=note:dec:w4awceq}), so a corpus that names no pack would have no legal kinds at all unless one pack is the default; this decision fixes which pack that is and which kinds it holds.

The kind set that most efforts earn is the trace spine: a want is recorded, an obligation answers it, a design commits to satisfy the obligation, and a check confirms the design holds.
That spine is the need-to-requirement-to-specification-to-verification chain the systems-engineering tradition draws as a V, and it is what the research and the corpus already call the sharp trace spine.
Around it sit the kinds that make the spine usable: the recorded choices that shaped it, the rules and quality conditions that bind it, the boundary and the vocabulary that make it legible, and the principles that justify it where no specific rule yet bears.

The kinds a product-discovery effort leans on, jobs and pains and gains and the value that answers them, are a different and optional emphasis; they ride the discovery pack, not the spine.
Holding them out of the default keeps the default honest: a corpus on the spine pack carries the kinds nearly every effort uses and none it would have to read past.

## Decision

- **The spine pack is the default.**
  A corpus that names no pack in its manifest is on the spine pack.
  It is the strongly recommended default, the kind set the method presents first, and the floor every other pack adds to rather than replaces.

- **The trace spine: need, requirement, specification, verification.**
  These four kinds are the V-model-shaped chain the pack is named for.
  A need records a want; a requirement is the obligation that addresses it; a specification commits the design that satisfies the requirement; a verification is the executable check that confirms the design or the obligation holds.
  This is the spine a regulated systems-engineering effort leans on, and the chain the trace views are computed over.

- **The rule and quality kinds: decision, convention, acceptance-criterion.**
  A decision records a choice that shaped the spine and the why behind it.
  A convention is an agreed coordination rule that binds the making of artifacts ([Conventions as a first-class kind](conventions-first-class.md){id=note:dec:4g730rg}).
  An acceptance-criterion is the solution-free condition, authored with its requirement, that defines what acceptable means for a requirement or need ([The acceptance-criterion kind](acceptance-criterion-kind.md){id=note:dec:sxv0tq9}); it attaches to the spine through `qualifies` and is the criterion a verification checks.

- **The boundary and vocabulary kinds: context, term, persona.**
  A context is the holistic boundary statement that fixes what is in and out of scope.
  A term defines a word the corpus uses with one specific meaning, and it underpins the whole spine, because every other kind is written in terms the corpus has defined.
  A persona names a class of actor a need is wanted by.
  These kinds carry no obligation themselves; they make the obligations legible.

- **The transverse anchor: principle.**
  A principle is a foundational commitment that guides judgment where no specific rule yet bears and from which a class of obligations follows ([Principles as a first-class kind](principles-first-class.md){id=note:dec:eym5t5g}).
  It is transverse: it cuts across the spine rather than sitting at one link of it, and a requirement reaches it through `enacts`.

- **value-proposition is not in the spine.**
  The value proposition's only required relation is `expresses`, whose target is an offering, and an offering is a discovery kind; a spine-only corpus would hold a value proposition whose required relation has no legal target.
  By the pack-closure rule, the value proposition belongs in the pack that holds the offering, which is the discovery pack ([Offering, fit, and the value proposition](offering-fit-and-value-proposition.md){id=note:dec:cjqwsxt}), not the spine.

- **Risk and the plan pack are not in the spine.**
  The risk kind is designed but deferred from this version ([The risk kind](risk-kind-deferred.md){id=note:dec:ge1r86x}), and the plan pack (task and `dependsOn`) is deferred entirely ([The plan pack](plan-pack-deferred.md){id=note:dec:p1peaam}).
  Neither sits in the spine; each lands as its own addition when first needed, touching nothing the spine already holds.

## Forces and trade-offs

The spine carries eleven kinds, which is more than a minimal floor of need and requirement alone, but each earns its place at the point of reference and in its relations: the chain needs all four trace kinds to close, the rule kinds carry the choices and conditions that bind the chain, the boundary and vocabulary kinds make it legible, and the principle anchors it.
A smaller default would force most adopters to add a pack on day one, which defeats the purpose of a default.

Holding the discovery kinds out costs a product-discovery effort one line of configuration to turn the discovery pack on.
This is accepted: the discovery emphasis is a real but optional one, and welding its kinds into the default would make every spine-only corpus read past kinds it does not use, against Proportionality.

Acceptance-criterion is in the spine rather than deferred because the alternative ships a verification kind whose semantics must later be re-cut, a semantic break a pre-release method can avoid now and never again.

## Alternatives considered

- **A minimal default of need and requirement only, with everything else opt-in.**
  Rejected: it under-serves nearly every adopter, who would add the trace and rule kinds immediately, so the configuration cost it avoids reappears on day one for almost everyone.

- **A maximal default that also carries the discovery kinds.**
  Rejected: it forces a kind set on adopters who do not earn it and re-creates the value-proposition-without-an-offering closure violation the pack model exists to prevent; the discovery kinds ride their own pack.

- **Defer the acceptance-criterion kind and keep it folded into verification in the default.**
  Rejected: deferral ships a conflated verification whose later un-conflation is a semantic break; the kind is carved out now, in the spine, while the cost is a section in a decision rather than a re-cut of every verification authored in the meantime.

## Driven by

- groundedIn: [Kind-agnostic substrate and kind packages](substrate-and-kind-packages.md){id=note:dec:w4awceq}
- groundedIn: [Proportionality](../principles/proportionality.md){id=note:principle:es0vhzn}
- groundedIn: [Earned Substance](../principles/earned-substance.md){id=note:principle:yecemfe}
- groundedIn: [Ceremony sized to the stakes](../needs/right-sized-ceremony.md){id=note:need:p7ekr3c}
- groundedIn: [Adopt without being stranded by the method's own evolution](../needs/adopt-without-being-stranded.md){id=note:need:x4zqfws}
