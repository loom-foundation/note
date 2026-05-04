---
id: note:dec:59ptf2z
name: Governance as an opt-in pack
kind: decision
status: current
decided: 2026-06-19T00:00:00Z
---

The method defines a **governance** pack: an opt-in built-in package that adds three kinds, policy (`pol`), standard (`std`), and procedure (`proc`), for the governing instruments an organization authors to direct itself.
The pack is held out of the spine and out of the discovery pack, so a corpus pays for the kinds only by naming `governance` in its manifest; the three cascade like any intent, carry their own provenance, and trace to the obligations they put in force through one new verb, `implements`.

## Context

An organization that runs on Note documents three things its frameworks name and its auditors read: a policy, a mandated direction that is signed and owned; a standard, a compulsory way of building or doing that a policy makes concrete; and a procedure, the ordered, role-assigned steps that carry a policy or standard out.
This is [State a shared obligation once](../needs/state-obligation-once.md){id=note:need:257yf29} read from the governance seat: the obligation is stated once at the scope that owns it, inherited by the units beneath, and departed from only by a visible, attributed deviation.

The spine kinds do not house these three without distortion, and that is what earns the pack rather than a profile of optional fields.
A self-imposed standard names a mechanism, and a mechanism with no external force behind it is the leaked solution the requirement rule exists to catch ([Conventions as a first-class kind](conventions-first-class.md){id=note:dec:4g730rg}); it sits above many obligations as their authority, not below one as its design, which is the wrong end for a specification; and it binds the system, not the making of artifacts, which is the wrong side for a convention.
A policy mandates a set of obligations under one sign-off, a fact no single requirement carries and no directory README carries checkably.
A procedure effects a change in the world and holds no verdict, which is what divides it from a verification.

The distinction is not Note's invention.
Policy, standard, and procedure are distinct instruments across the frameworks an organization answers to, each with its own author, review cadence, and audience, recorded below under Frameworks surveyed.
Recognizing the words an adopter already uses is its own concern; the bar a new kind must still clear is Earned Substance, and the pass that tested these against it is recorded in Forces and trade-offs.

## Decision

- **A governance pack, opt-in, three kinds.**
  The pack adds policy, standard, and procedure, with kind-segments `pol`, `std`, and `proc`.
  It is enabled by naming `governance` in the manifest `packs`; absent that, no corpus carries the kinds, and landing the pack is additive, breaking nothing authored before it.

- **policy, the signed instrument of record.**
  A policy is a mandated direction that mandates a set of obligations and carries its own sign-off: an `approver` named by role, an `effective_date`, and a `review_due`.
  Its load-bearing fact is that *this instrument*, at this version and date, is in force, not that the system shall do a single thing.

- **standard, the compulsory internal mandate.**
  A standard names a mechanism, format, or threshold the organization makes compulsory of itself, derived from a policy and conformed to by many systems.
  Where an external force imposes the mechanism, the obligation is a constraint requirement and the correspondence is the compliance pack's crosswalk; the standard kind is for the organization's own self-imposed mechanism, which neither a requirement nor a specification can hold without distortion.

- **procedure, the ordered operational steps.**
  A procedure is the ordered, role-assigned steps that carry a policy or standard out: a `trigger`, an `owner` by role, and a `## Steps` section where each step names the role that performs it.
  It effects a state change and holds no verdict, and is owned by operations and revised on incident.

- **The verb `implements`.**
  A standard, a procedure, or a requirement reaches the policy or standard it carries out through `implements`, authored on the dependent end; its inverse `implementedBy` is a derived view, the coverage an auditor reads without the edge being authored twice.

- **Provenance, not access.**
  A governance artifact records who approved it, when it takes effect, and when it is next reviewed.
  It does not record who may read it: sensitivity is a separate, cross-cutting axis, and enforcement of either belongs to the Orchestrating Authority, not the artifact.

- **Compliance stays a view.**
  The governance pack holds the instruments an organization authors; the compliance pack maps them to the external frameworks they answer to.
  The two compose, and neither absorbs the other.

## Forces and trade-offs

Three new kinds is the cost Earned Substance guards, and a blind adversarial pass collapsed two of the three before they were minted: policy into a constraint requirement with provenance fields, standard into a specification or a constraint requirement.
The kinds ship over that pass, so the load each carries that the collapse loses is recorded here, not assumed.

A policy is not one obligation but the ratified container of a set: its fact is that the instrument, at a version, a date, and an approving role, mandates obligations beneath it, and its lifecycle is ratify, publish, and re-attest, where a lapsed review is itself a finding rather than an obligation gone unmet.
A standard names a self-imposed mechanism, the exact case the requirement rule rejects as a leaked solution, sits above many obligations rather than below one, and binds the system rather than the making of artifacts: the homelessness that earned convention, one axis over.
A procedure is a thing to do when a trigger fires, with no truth value, where a verification answers a question and a specification fixes a design.

The pack is opt-in for the reason the discovery, risk, and plan kinds are held out of the spine: a corpus that does not govern reads past nothing it has not earned, by Proportionality.

Two tripwires the same pass surfaced are kept as the inclusion tests' guard.
A procedure whose steps yield a verdict, name a verification method, or carry an expected result is a verification mis-filed.
A standard with an external force behind it is a constraint requirement carrying a crosswalk, not a governance standard.

## Alternatives considered

- **Reuse the spine kinds and add a policy-grade profile.**
  Rejected: a profile bolts provenance onto a requirement without giving the homeless standard a home or the policy its container, and the bolt-on was the weakest part of the design under adversarial review; the homelessness arguments above are what a profile cannot answer.

- **One governance kind, or the three welded into the spine.**
  Rejected: one kind collapses the author, lifecycle, and audience distinctions the frameworks draw and the kinds exist to carry; welding them into the spine taxes every corpus, including the many that never govern, against Proportionality.

- **Name the pack `compliance`.**
  Rejected: `compliance` already names the crosswalk pack ([The compliance crosswalk pack](compliance-crosswalk-pack.md){id=note:dec:ve053yf}) and the value proposition that compliance is a view of intent, not a second system; a second compliance would muddy exactly that line.
  Governance names the instruments an organization authors; compliance names their mapping to external control.

- **Carry a `classification` field on policy and standard.**
  Rejected: sensitivity is a cross-cutting axis any kind may carry, a specification or an inherited reference as readily as a policy, not a governance property; it is settled separately as a generic classification axis, complementary to this pack and not part of it.

## Frameworks surveyed

That policy, standard, and procedure are genuinely distinct instruments, each with its own author, lifecycle, and audience, is established across the governance and assurance frameworks an adopter answers to, not coined here.

- ISO/IEC 27001 and 27002: the documented-information hierarchy, and the Clause 7.5 controls for approval, version, and review.
- NIST SP 800-12: policy, standard, and procedure defined in sequence, with a standard "normally compulsory within an organization"; and SP 800-53, whose AC-1 states that "simply restating controls does not constitute an organizational policy or procedure."
- NIST OSCAL: the machine-readable governance model whose profile tailoring mirrors scope cascade, and whose control-mapping mirrors the crosswalk.
- The New Zealand Information Security Manual and the Australian ISM and IRAP: control catalogs maintained alongside a policy, standard, procedure, and system-security-plan document set.
- COBIT 2019, ITIL 4, and ISO 9001: the source of the process versus procedure distinction, on which this version carries procedure and holds process as a later addition.
- ISACA, (ISC)² CISSP, SANS, PCI-DSS, and SOC 2: the policy, standard, baseline, procedure, and guideline hierarchy, and its graded approval authorities.

A control, across all of them, is not a document kind but a measure: in Note it is a constraint requirement crosswalked to its source, not a governance kind.

## Driven by

- groundedIn: [State a shared obligation once](../needs/state-obligation-once.md){id=note:need:257yf29}
- groundedIn: [Kind-agnostic substrate and kind packages](substrate-and-kind-packages.md){id=note:dec:w4awceq}
- groundedIn: [Conventions as a first-class kind](conventions-first-class.md){id=note:dec:4g730rg}
- groundedIn: [Scope and inheritance](../requirements/system/scope-and-inheritance.md){id=note:req:96smmcv}
- groundedIn: [Visible, attributable deviation](../requirements/system/visible-attributable-deviation.md){id=note:req:64eknb1}
- groundedIn: [Representation, not enforcement](../requirements/system/representation-not-enforcement.md){id=note:req:agncpcc}
- groundedIn: [Declarable kind packages](../requirements/system/declarable-kind-packages.md){id=note:req:ekfkzzt}
- groundedIn: [Earned Substance](../principles/earned-substance.md){id=note:principle:yecemfe}
- groundedIn: [Proportionality](../principles/proportionality.md){id=note:principle:es0vhzn}
- groundedIn: [Single Source of Truth](../principles/single-source-of-truth.md){id=note:principle:8691937}
