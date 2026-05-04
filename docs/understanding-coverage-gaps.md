# Understanding coverage gaps

How to read the gaps in a body of intent: what each direction of gap means, which ones are ripe to act on, and why the method surfaces them rather than forcing them closed.
Coverage has two sides.
On the build spine, a Systems Engineer reads the gaps along the V-model chain (need to requirement to specification to test): a requirement that nothing implements, an obligation that nothing tests, or an implementation that traces back to no requirement ([Tell where the V is incomplete](../loom/note/needs/see-and-decide-on-coverage-gaps/job-tell-where-the-v-is-incomplete.md){id=note:job:mmj6f76}).
On the discovery side, a Product Owner reads the gaps between needs and offerings: a need with no offering, an offering that does not relieve every pain it claims, or offered value that no requirement yet delivers.
This is orientation and applied guidance, not normative text; the binding model lives in [The spine pack](../loom/note/specifications/note/spine-pack.md){id=note:spec:6kjja5r} for the build spine, and in [The discovery pack](../loom/note/specifications/note/discovery-pack.md){id=note:spec:w6nsgt1} and [Offering, fit, and the value proposition](../loom/note/decisions/offering-fit-and-value-proposition.md){id=note:dec:cjqwsxt} for the discovery side; the need both answer is [See and decide on coverage gaps](../loom/note/needs/see-and-decide-on-coverage-gaps.md){id=note:need:7kp2v9d}, and the offering that serves it is [Coverage you can act on, not a checklist to clear](../loom/note/offerings/coverage-you-can-act-on.md){id=note:offering:5kw7nq4}.

## Coverage made decidable, not forced closed

A corpus accumulates intent: needs, the requirements and specifications that follow them, the tests that check them, and the offerings that answer the needs.
The gaps between these artifacts are where the interesting decisions live.

The method's job is to surface every gap and make it decidable, with each gap's direction distinguished, rather than auto-resolve it.
Both sides are read the same way, off the edges between artifacts: the build spine from the `addresses`, `satisfies`, `derivedFrom`, and `verifies` chain; the discovery side from the `relieves` and `creates` edges that form the fit between an offering and a need, and from the `delivers` edges that show which requirements realize the offered value ([The spine pack](../loom/note/specifications/note/spine-pack.md){id=note:spec:6kjja5r}, [The discovery pack](../loom/note/specifications/note/discovery-pack.md){id=note:spec:w6nsgt1}).
Because both are computed from the edges, a missing link or an uncovered pain falls out as a reading, not as an authored defect.
That is what lets a gap be shown without being closed: the method shows the gaps and ranks them, but it does not decide them.
A surfaced gap is information, not an instruction; coverage is steered by the person who owns the work, never cleared on the tool's command ([Coverage you can act on, not a checklist to clear](../loom/note/offerings/coverage-you-can-act-on.md){id=note:offering:5kw7nq4}).

## Coverage gaps on the spine (the core pack)

The spine is the chain every obligation travels: need to requirement to specification to test, with the code that realizes the specification.
A Systems Engineer walks that chain and wants to see exactly where a link is missing ([Tell where the V is incomplete](../loom/note/needs/see-and-decide-on-coverage-gaps/job-tell-where-the-v-is-incomplete.md){id=note:job:mmj6f76}).
A coverage gap here points three ways, and each way means something different.

### A requirement that nothing implements

A requirement is written, but no specification or code realizes it.
It has a `satisfies` edge missing on its design side: nothing satisfies it, nothing builds it.
On paper it looks done; the missing build only shows up much later, when someone goes looking for the part that should have been there ([An obligation has no design](../loom/note/needs/see-and-decide-on-coverage-gaps/pain-an-obligation-has-no-design.md){id=note:pain:7pg4p7y}).

### An obligation that nothing tests

A requirement or specification is in place, but no verification covers whether it is actually met.
It has no `verifies` edge pointing at it: nothing checks it.
It passes review by looking finished, then fails in the field, where the missing test would have caught it first ([An obligation has no test](../loom/note/needs/see-and-decide-on-coverage-gaps/pain-an-obligation-has-no-test.md){id=note:pain:ettzaw3}).
Looking finished and being verified are two different things, and this gap is the distance between them.

### An implementation, specification, or test that traces back to no requirement

A specification, a piece of code, or a test traces to nothing on the requirement side: no `satisfies`, no `derivedFrom`, no `verifies` reaching a requirement.
It is work no one asked for, hiding among the work that was asked for ([An implementation traces to no requirement](../loom/note/needs/see-and-decide-on-coverage-gaps/pain-an-implementation-traces-to-no-requirement.md){id=note:pain:8rdzdep}).
This is building with no why, surfaced so it cannot pass for the real thing.

### Readiness: ripe versus still settling

Ripeness reads off artifact status.
A current requirement is settled and ready to design or test against; a draft one is still being worked out, so designing or testing against it now is aiming at a moving target.
Surfacing the missing links sorted by readiness is what lets effort flow to the obligations that have earned it ([Build and verify work sorted by readiness](../loom/note/needs/see-and-decide-on-coverage-gaps/gain-build-and-verify-work-sorted-by-readiness.md){id=note:gain:xfj2s29}), and the gaps stay visible for the engineer to act on or not, never forced closed ([The V incompleteness is visible](../loom/note/needs/see-and-decide-on-coverage-gaps/gain-the-v-incompleteness-is-visible.md){id=note:gain:xmzhz5v}).

### Deciding where to invest, not confirming after the fact

Reading these gaps is forward-looking work: it is about deciding where to invest next, which obligation still needs a design and which still needs a test, before and during the build.
Confirming after the build that nothing was left without a plan and a test is a different job, owned by a Reviewer or Auditor; that one lives in [Trust and drift visibility](../loom/note/needs/trust-intent-is-honored.md){id=note:need:46tkxcn}.
One plans where to put the effort; the other attests it was made.

### A worked example

Picture a Systems Engineer scanning the chain the week before a release.

The requirement "the catalog shall sync within five minutes of reconnect" is current, and a specification satisfies it: the sync design is there.
But nothing verifies it: no test covers whether the five-minute window actually holds.
That is an obligation with no test, surfaced before the release rather than discovered in the field.

A second requirement, "operators shall be paged on a failed sync," is also current and has a specification, and that specification carries a load test that runs green.
But the test traces to no requirement anyone can find: it is a check on work no one asked for.
That is an implementation tracing back to no requirement, the build-spine orphan.

Both are surfaced, each labeled, and both are ripe (their requirements are current, not draft).
The engineer decides the untested sync window is the one to close first: it is a real obligation about to ship unverified, while the orphan test is work to trace back or retire, not a release blocker.
The tool shows both and ranks them by readiness; the engineer chooses what to build or verify next.

## Coverage gaps in the discovery pack (the optional pack)

The discovery pack adds needs and offerings on top of the spine.
A Product Owner reads the gaps between them, where the fit between an offering and a need is derived from the `relieves` and `creates` edges, and the realization of the offered value from the `delivers` edges.
A gap here points four ways, and which way it points changes whether it is healthy.

### A need with no offering: an opportunity

A persona's jobs, pains, and gains are captured, but no offering answers them yet.
This is the natural and healthy order of discovery: understand the persona first, build later.
Read it as an opportunity to design against, not as a defect to fix.
A corpus full of unserved needs is a corpus that did its discovery before its building, which is the right way around.

### An offering whose pains and gains are not all covered: an incomplete fit

An offering addresses a need, yet some pain it claims to serve has no reliever, or some gain has no creator.
This is an incomplete-fit gap.
The specific unrelieved pains and uncreated gains are named, and the owner chooses to finish the fit or to accept it as is.
An uncovered pain is simply a pain with no inbound `relieves`; an orphan reliever is a reliever with no `relieves` target; both are reportable gaps, never ill-formed artifacts.

### Offered value that nothing delivers: a pitch outrunning the system

An offering's reliever or creator covers a pain or gain, and a value proposition may already pitch it, but no requirement `delivers` that reliever or creator: the value is offered, and nothing yet obliges the system to realize it.
This is the gap that lets a landing-page claim outrun the system behind it.
When the chain is closed it runs whole: the pitch `expresses` the offering, the offering's facets relieve and create the need's facets, requirements deliver those facets, specifications satisfy the requirements, and verifications confirm them, so the pitched claim is a true statement by inspection, the product does that, and the trace shows it.
When the chain is open, this gap names exactly which promised value is not yet anyone's obligation, so the owner can draft the requirement that delivers it or pull the claim.

### Two channels on one need, told apart

A requirement always keeps its spine edge: it `addresses` the need it serves, whatever packs are enabled, and authoring an offering never rewires that.
Coverage of a need with an offering therefore reads as a labeled union: the obligations serving the need directly, and the obligations delivering its offering's relievers and creators, each labeled for the channel it came through.
A direct edge sitting beside a complete delivers chain is redundant, and is reported as that; an obligation outside the pitched value, a regulatory constraint or a non-functional floor, keeps the direct edge as its honest home and is surfaced as exactly that.
Both readings are information for the owner, never errors.

### A requirement or specification with no need: an orphaned justification

A requirement or specification that traces to nothing on the need side is the discovery-side orphan: intent with no persona it serves.
It is the same smell as the build-spine orphan, building with no why, read one layer out: there the work traced back to no requirement, here the requirement traces back to no need.
It is surfaced so it cannot hide among the healthy unserved needs.

### Sorting opportunities by ripeness

Not every uncovered need is equally ready to build for, so opportunities are sorted by ripeness, read off artifact status.
A need whose facets are all current is ripe: discovery has settled, and it is ready to design an offering against.
A need still carried as draft is premature to build for: it is still being discovered, and an offering built against it now is built on a moving target.
The point is to tell the two apart, so effort flows to the needs that have earned it rather than to whichever uncovered need is noticed first.

### A worked example

Picture two needs and one offering shown together.

The first need, "schedule field visits offline," has all-current facets and no offering pointing at it.
That is a ripe opportunity: discovery has settled, and it is ready to design an offering against.

The second need, "reconcile invoices across currencies," is still all-draft.
It is also uncovered, but it is premature: the owner sees it ranked below the first, a discovery still in progress rather than a build waiting to start.

The one offering, "shared parts catalog," addresses the first need and brings relievers and creators for most of its facets, but one pain (the technician's fear of ordering a discontinued part) has no reliever pointing at it.
That is an incomplete fit, and the specific unrelieved pain is named so the owner can choose to finish it or accept it.

The same offering carries a gain creator, one-tap reorder of a recognized part, and the sales deck already pitches it; but no requirement `delivers` that creator yet.
The pitch is ahead of the system: the claim is on the deck, and nothing yet obliges the build to make it true.
Surfaced, the owner chooses: draft the requirement that delivers it, or pull the claim.

All the directions appear at once, each labeled for what it is, and the owner decides what to do with each.

## Normative sources

The orientation here restates what these fix:

- [See and decide on coverage gaps](../loom/note/needs/see-and-decide-on-coverage-gaps.md){id=note:need:7kp2v9d}: the gaps in a body of intent shall be surfaced and made decidable, each direction told apart, rather than closed for the reader; the build-spine side (the V-model chain) and the discovery side (needs and offerings) are both covered.
- [Coverage you can act on, not a checklist to clear](../loom/note/offerings/coverage-you-can-act-on.md){id=note:offering:5kw7nq4}: every gap is shown with its direction, the work is sorted by ripeness, and each gap is left open for the reader to act on or not.
- [The spine pack](../loom/note/specifications/note/spine-pack.md){id=note:spec:6kjja5r}: fixes the need-to-requirement-to-specification-to-verification chain and the `addresses`, `satisfies`, `derivedFrom`, and `verifies` relations the build-spine gap readings are computed from.
- [The discovery pack](../loom/note/specifications/note/discovery-pack.md){id=note:spec:w6nsgt1}: fixes the offering, the need profile, their facets, and the derived fit the discovery-side gap readings are computed from.
- [Offering, fit, and the value proposition](../loom/note/decisions/offering-fit-and-value-proposition.md){id=note:dec:cjqwsxt}: the fit is the derived set of `relieves` and `creates` edges, so an uncovered pain or an orphan reliever is a reportable gap, never authored; a reliever or creator that no requirement `delivers` is the third reportable gap, value offered that no obligation yet realizes; and coverage of a need with an offering reads as a labeled union of the direct and offering channels, with the spine's `addresses` edge legal on every need whatever packs are enabled.
- [Tell where the V is incomplete](../loom/note/needs/see-and-decide-on-coverage-gaps/job-tell-where-the-v-is-incomplete.md){id=note:job:mmj6f76}, [An obligation has no design](../loom/note/needs/see-and-decide-on-coverage-gaps/pain-an-obligation-has-no-design.md){id=note:pain:7pg4p7y}, [An obligation has no test](../loom/note/needs/see-and-decide-on-coverage-gaps/pain-an-obligation-has-no-test.md){id=note:pain:ettzaw3}, [An implementation traces to no requirement](../loom/note/needs/see-and-decide-on-coverage-gaps/pain-an-implementation-traces-to-no-requirement.md){id=note:pain:8rdzdep}, [The V incompleteness is visible](../loom/note/needs/see-and-decide-on-coverage-gaps/gain-the-v-incompleteness-is-visible.md){id=note:gain:xmzhz5v}, [Build and verify work sorted by readiness](../loom/note/needs/see-and-decide-on-coverage-gaps/gain-build-and-verify-work-sorted-by-readiness.md){id=note:gain:xfj2s29}: the Systems Engineer facets that frame the build-spine side of the need.
- [Trust and drift visibility](../loom/note/needs/trust-intent-is-honored.md){id=note:need:46tkxcn}: the separate, after-the-build job of attesting that nothing was left without a plan and a test, distinct from this forward-looking decide-where-to-invest reading.
