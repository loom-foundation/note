---
id: note:dec:cjqwsxt
name: Offering, fit, and the value proposition
kind: decision
status: current
decided: 2026-06-12T00:00:00Z
---

The discovery pack carries two value-side kinds: the offering, a value map that addresses a need, and the value proposition, the authored, customer-facing pitch that `expresses` an offering.
The correspondence between an offering's relievers and creators and a need's pains and gains is the fit, the derived set of `relieves` and `creates` edges, never authored.
Both kinds live in the discovery pack: the value proposition's only required relation, `expresses`, targets an offering, so a spine-only corpus must not hold it.
The value layer sits beside the spine, opt-in and adopted need by need, and it is additive: the spine stays valid whatever packs are enabled, and the layer's purpose is the realization trace that makes an authored pitch an inspectable claim, traced to built, checked obligation.

## Context

A sustained body of work that captures the value it offers, whether a software system, a hardware product, a process, or a methodology like this corpus, needs to separate three things the Value Proposition Canvas tradition tends to blur.

The Canvas calls the offering side the "Value Map", but "map" reads as the mapping between the two sides, which is the fit, so the offering and the correspondence collapse into one word.
Mainstream usage, from the 1988 coinage onward, uses "value proposition" for the offer itself, while the Canvas uses it for the achieved fit, so the term carries two meanings at once.
And the Canvas's third value-map element, "Products and Services", is the actual product or service, which the method already has as the System.

Three things are therefore separated: the structured value (the offering), the computed correspondence to the need (the fit), and the authored claim about that value (the value proposition).

These are discovery-pack kinds, held out of the spine by the pack-closure rule.
A value proposition's only required relation is `expresses`, whose target is an offering; an offering is a discovery kind; so the value proposition cannot be valid in a corpus that lacks the offering.
Both kinds therefore sit in the same pack, the discovery pack, where the offering it expresses also lives, and a spine-only corpus holds neither.

## Decision

- **The value map is the `offering` kind.**
  It is benefit-led, `addresses` a need, and is composed of its Pain Reliever and Gain Creator facets ([Atomic facets](atomic-facets.md){id=note:dec:af3k9w2}).
  It carries no discriminator field; polarity lives in the facet kinds.

- **The `value-proposition` kind is the authored pitch.**
  It is optional, benefit-led, and `expresses` an offering, and it is the single source product copy, marketing, and sales restate.
  By default the value proposition is the computed fit; a statement is authored only when the pitch is worth capturing.
  The pitch is also the artifact's `name`.
  The body opens with the pitch as the unheaded lead (one sentence, ending with a period); the story and fit essence follow under `## The case`.
  No trailing repeated pitch line.

- **The fit is a derived view, not a kind.**
  The fit is the set of `relieves` (reliever to pain) and `creates` (creator to gain) edges; an uncovered pain or an orphan reliever is a reportable gap.
  The value proposition is the claim; the fit is the evidence that substantiates it.
  A reliever or creator that no requirement `delivers` is a third reportable gap: value offered that no obligation yet realizes, a pitch writing a promise the system has not committed to.

- **Both kinds are in the discovery pack.**
  The offering and the value proposition ride the discovery pack together, with the facet kinds they are composed of and matched against.
  Pack closure requires it: the value proposition reaches an offering through its required `expresses`, so it cannot belong to a pack the offering is absent from.

- **The spine stands on its own; a pack only adds.**
  Enabling the discovery pack never invalidates a spine relation: a `requirement addresses need` edge is legal on every need, offering or no offering, because the core corpus must stay valid independent of any opt-in pack.
  The pack adds the value-side trace; it never rewires the spine's.

- **The value layer's purpose is the realization trace, adopted need by need.**
  A need is *raw* or *propositioned*.
  A raw need carries no offering; its requirements may reach its facets directly (`relieves` a pain, `creates` a gain, `addresses` a job) as the lightweight fit shortcut.
  A propositioned need has an offering that `addresses` it: the offering's relievers and creators carry the fit, and requirements `delivers` them, closing the chain that makes the pitch inspectable, a value proposition `expresses` the offering, the offering's facets relieve and create the need's facets, requirements deliver those facets, specifications satisfy the requirements, and verifications confirm them, so a pitched claim traces to built, checked obligation.
  Fit exclusivity is per facet: once an offering's reliever or creator covers a pain or gain, the direct requirement shortcut on that same facet is retired to the offering path, so the fit is never claimed twice; the need-level `addresses` edge is untouched by this.
  Need-level coverage is read as a labeled union, obligations serving the need directly and obligations delivering its offering's facets, told apart: a direct edge beside a complete delivers chain is redundant and reported, and an obligation outside the pitched value (a constraint, a non-functional floor) keeps the direct edge as its honest home, surfaced as exactly that, information for the owner, never an error.
  The layer is adopted one need at a time, so a corpus may leave most needs raw and propose value only where the pitch and the fit are worth the machinery.

- **Relations.**
  A facet `partOf` its need or offering; a pain-reliever `relieves` a pain; a gain-creator `creates` a gain; an offering `addresses` a need; a value proposition `expresses` an offering; a requirement `delivers` a pain-reliever or gain-creator, or, for a facet no offering covers, `relieves` a pain or `creates` a gain directly; and a requirement `addresses` the need it serves on the spine, whatever the need's state.

- **The System provides the offering.**
  The Canvas's "Products and Services" maps to the System, the system-of-interest under design (a product, a service, or any arrangement achieving a purpose), defined by its requirements and specifications.
  This provider relationship, stated here only in prose, is now encoded by the `system` kind and its `provides` edge ([The system-of-interest provides the value](system-of-interest-provides-value.md){id=note:dec:swar6np}).

- **Verification targets what a check establishes.**
  Conformance to a design or contract verifies the specification; a direct obligation check verifies the requirement; the requirement is met transitively through `satisfies` and `verifies`.

## Forces and trade-offs

Reclaiming "value proposition" for the pitch and naming the offer side "offering" trades a little recognizability ("value proposition" is the household phrase for the offer) for precision: the three concepts no longer share a word, and the term reads true, since the value proposition is the claim where an offering meets a need.

Keeping the value proposition optional, with the fit computed by default, keeps the floor light: a corpus gets coverage and gaps from the fit without authoring a pitch.

Adopting the value layer need by need, rather than corpus-wide, keeps the raw path cheap: a need whose requirements address its facets directly carries no offering and no proposition, and the offering machinery is earned only where a need is genuinely propositioned.
This is Proportionality applied to the value layer: the cost falls on the needs that earn an offering, not on every need.

Holding both kinds in the discovery pack costs a value-capturing effort one line of configuration to enable the pack, the same cost the facet kinds carry, and for the same reason: an effort that captures only its trace spine should not hold value kinds it does not use.

Dropping the exclusivity the pack first shipped with, which disallowed `requirement addresses need` once an offering intervened, follows from the additive rule.
The exclusivity mediated the spine where the intent was only ever to trace realization; it left an obligation outside the pitched value, a regulatory constraint or a non-functional floor, with no honest home; it made enabling an opt-in pack retroactively invalidate previously legal spine edges; and it coupled the durable justification trace to the most repackaging-prone artifacts in the corpus.
The one concern it did answer, that obligations could discharge against a need invisibly to the offering's coverage story, is answered instead by the labeled union view, which surfaces the direct channel rather than banning it, consistent with coverage gaps being surfaced and made decidable rather than closed for the reader ([See and decide on coverage gaps](../needs/see-and-decide-on-coverage-gaps.md){id=note:need:7kp2v9d}).

## Alternatives considered

- **Keep the Canvas name "Value Map".**
  Rejected: "map" conflates the offering with the fit, the exact ambiguity this decision removes.

- **Name the offer side "Solution".**
  Rejected: "solution" is overloaded in requirements engineering (the whole answer, value and thing together) and is plainer than precise; "offering" (Kotler's market offering) names the value cleanly.

- **Name the build "Solution" too.**
  Rejected: the thing under design is already the System, an existing, more general concept; "product", "service", and "solution" are prose synonyms for it.

- **Leave the value proposition as the computed fit only, not a kind.**
  Rejected: the pitch is worth capturing as an authored, citable, reusable asset, which a computed view cannot be; the fit substantiates the captured claim.

- **Place the value proposition in the spine pack with a relaxed `expresses` relation.**
  Rejected: a spine-only corpus would then hold a value proposition whose required relation reaches an offering it cannot have, the exact closure violation the pack model forbids; the value proposition belongs in the pack that holds the offering.

- **Make the value layer a corpus-wide setting rather than a per-need choice.**
  Rejected: it forces every need into the same path, either taxing simple needs with offerings they do not earn or barring a propositioned need where one is wanted; adopting the layer need by need keeps each need on the path that fits it.

- **Exclusive mediation: disallow `requirement addresses need` once an offering intervenes (the rule as first shipped).**
  Rejected on re-examination against the intent it was meant to implement.
  Its strongest defense is real: with both channels legal, an obligation can discharge against a need outside the offering's coverage story, and a facet-level check alone can never see a need-level edge; the labeled union view answers that by surfacing the direct channel rather than banning it.
  What the ban cost was worse: an obligation outside the pitched value had no legal home short of fabricating a reliever for value never offered; enabling an opt-in pack retroactively invalidated legal spine edges, against the promise that moving up a level never strands what came before; and the stability of the justification trace became hostage to offering repackaging.
  The rule's true intent, that a pitch be substantiated by trace all the way to checked obligation, is carried by the realization chain and its gap readings, not by exclusivity.

- **Value-proposition body: value-first opening paragraph with the distilled pitch as the closing line.**
  Rejected: the pitch is the artifact's designation and the first thing a reader meets; burying it at the end of an opening paragraph makes the strongest line the easiest to miss.
  The current rule places the pitch as the unheaded lead and the story under `## The case`.

## Driven by

- groundedIn: [Kind-agnostic substrate and kind packages](substrate-and-kind-packages.md){id=note:dec:w4awceq}
- groundedIn: [Atomic facets](atomic-facets.md){id=note:dec:af3k9w2}
- groundedIn: [Earned Substance](../principles/earned-substance.md){id=note:principle:yecemfe}
- groundedIn: [Articulate value offered](../needs/articulate-value-offered.md){id=note:need:9w2k4pt}
