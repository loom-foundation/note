---
id: note:need:7kp2v9d
name: See and decide on coverage gaps
persona:
  - "[Product Owner](../personas/product-owner.md){id=note:persona:pd8w3kq}"
  - "[Organization or Platform Owner](../personas/organization-owner.md){id=note:persona:6ek4j8b}"
  - "[Systems Engineer](../personas/systems-engineer.md){id=note:persona:25fdjrx}"
kind: need
status: current
validation: inferred
---

A Product Owner, an Organization or Platform Owner, or a Systems Engineer building out a body of intent wants the gaps in it surfaced and made decidable, with each gap's direction told apart, rather than closed for them, so they choose where to invest next instead of being handed a list to clear.
The gaps come in two sides.
On the discovery side: a need with no offering, or an offering that does not relieve every pain it claims.
On the build spine: a requirement nothing implements, an obligation nothing tests, or an implementation tracing back to no requirement.

This is distinct from [Trust and drift visibility](trust-intent-is-honored.md){id=note:need:46tkxcn}, whose confirm-obligation-coverage attests after the build that nothing was left without a plan and a test; this need is about deciding, before and during the build, where to invest next: which obligation still needs a design, which still needs a test.
One plans where to put effort; the other attests it was made.

## Illustrative situations

1. **A need with no offering yet.**
   A Product Owner has captured a persona's jobs, pains, and gains, but no offering answers them.
   This is the natural order of discovery: understand the persona first, build later.
   The owner wants this read as a healthy opportunity to design against, not flagged as a defect to fix.

2. **An offering that relieves some pains but not all.**
   An offering addresses a need, yet a pain it claims to serve has no reliever and a gain has no creator.
   The owner wants the incomplete fit shown as a coverage gap it can choose to close or accept, with the specific unrelieved pains and uncreated gains named.

3. **A specification with no need behind it.**
   A requirement or specification traces to nothing on the need side.
   The owner wants this orphaned justification surfaced as the real smell, building with no why, rather than left invisible among healthy unserved needs.

4. **Sorting opportunities by ripeness.**
   The owner is looking at a backlog of unserved needs and wants to know which are ready to design an offering against.
   A need whose facets are all current is ripe; a need still carried as draft is premature to build for, and the owner wants the two told apart.

5. **Walking the V-model chain before a release.**
   A Systems Engineer scans the chain from need to requirement to specification to test and sees a requirement that has a design but no test, and another that traces to no requirement at all.
   The engineer wants the two told apart so it can decide which to close first.

## Source

The value-proposition-design tradition treats the fit between an offering and a customer profile as derived from the edges, so an uncovered pain, an orphan reliever, and an unserved need are read off those edges rather than authored as defects.
The discovery pack makes that fit derived rather than authored ([The discovery pack](../specifications/note/discovery-pack.md){id=note:spec:w6nsgt1}), which is what lets a gap's direction be read off the edges and surfaced without forcing its resolution ([Offering, fit, and the value proposition](../decisions/offering-fit-and-value-proposition.md){id=note:dec:cjqwsxt}).

The need is reasoned from applying that derived-fit model to first-class intent capture, where needs, offerings, and commitments are all citable artifacts, rather than observed in the field.

External to this corpus and not derived from it.
