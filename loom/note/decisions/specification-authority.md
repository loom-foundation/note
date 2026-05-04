---
id: note:dec:av7k3mq
name: Independent authority on specifications
kind: decision
status: current
decided: 2026-06-13T00:00:00Z
---

A Specification carries an `authority` frontmatter field, required at the `strict` profile: a list of repository-relative paths to the external authorities its design answers to, which stay untouched and govern the parts they express.
Two tiers follow from the field. A non-empty list is the independently validated tier: the design answers to an authority outside the method. An empty list is the honest other tier: no external authority applies, so the design is a commitment checked by review, a weaker control stated plainly rather than dressed as validation.
The field is the source of truth; an optional `## Authority` section adds commentary, and both are distinct from a Verification, which checks an implementation against the Specification.

## Context

Three questions sit around a Specification, and Note already homes two.
Whether an implementation honors the Specification is a Verification, the check the manifesto names as code against specifications; an OpenAPI contract test, which asserts the status codes and schemas the spec fixes, is exactly this, and it verifies the Specification, not the Requirement behind it.
Whether the Specification is the right design for its Requirement is a judgment on the `satisfies` link, made by review.
The third question is whether the Specification's own content is falsifiable against something outside the method, so a Specification is not sound merely because Note labels it one.

[Verifiable, independently checkable design](../requirements/stakeholder/verifiable-independently-checkable-design.md){id=note:req:vh3k82n} and the system requirement derived from it, [Independently validatable specifications](../requirements/system/independently-validatable-specifications.md){id=note:req:fph0vnr}, state that third obligation, and the latter leaves its mechanism to specification: which authorities apply to which kinds of specification, and the fallback where no external authority exists.
This decision fixes that mechanism.

The fallback is half the value, and it has to be honest about its own limit.
Where an external standard fixes a Specification's content (an OpenAPI document, a JSON Schema, a security-verification standard), the design answers to it and is independently checkable.
Where none does (the graceful-degradation behavior when a dependency fails, an authentication posture, a privacy commitment), the design is a decision, not a claim falsifiable against a standard.
The method cannot manufacture an authority the world does not provide, so the honest move is to mark the absence and name review as the control, never to call review a form of independent validation.
Because the method's standing claim is that conformance is checkable from the files alone, the declaration of which tier a Specification is in belongs in the computable place, the frontmatter.

## Decision

- **An `authority` frontmatter field, required at `strict`.**
  Its value is a list of repository-relative paths to the external authorities a Specification's design answers to, one or more, since a single design may answer to more than one, an endpoint fixed by an OpenAPI document and a state-machine.

- **Two tiers.**
  A non-empty `authority` is the independently validated tier: the design answers to an authority outside the method, which is what [Independently validatable specifications](../requirements/system/independently-validatable-specifications.md){id=note:req:fph0vnr} obliges.
  An empty list (`[]`) is the review-gated tier: no external authority applies, so the design is a commitment checked by review, a weaker control than independent validation, and the empty list states that openly.
  The requirement obliges the method to provide the slot, which the field does; it does not oblige every design to carry an external authority, because not every design has one.
  There is no `internal` value and no claim that the Specification is "its own authority": the empty list is the disclosure, not a validation claim.

- **The authority is any external standard the design answers to.**
  It may be a machine-readable contract the design is generated against or checked against (an OpenAPI document, a JSON Schema, an OpenFGA model), or a completeness standard the design is reviewed against (a control catalogue, a security-verification standard such as OWASP ASVS).
  It need not be a format the design generates; what qualifies it is that it is external to the method and the design answers to it.

- **Prefer a stable authority.**
  An authority earns the field when it is ratified by a standards body, governed by a neutral foundation with a stability policy, or released at a version with a compatibility commitment.
  A governance-soft format, unratified, single-vendor-stewarded, or pre-release, is better treated as a non-authoritative derived export generated from the design than as the authority the design answers to; pointing the field at a moving target trades the method's say-so for one vendor's, which is not the independence the requirement asks for.

- **The field is the source of truth; the `## Authority` section is optional commentary.**
  The field is the computable declaration a checker reads, resolves, and reports over.
  The optional `## Authority` section names the standard in human terms and states that the external document governs on divergence; it restates none of the external content, and like a Need's or a Requirement's `## Source` it is optional.

- **External pointers are repository-relative.**
  The authority document lives outside the corpus and carries no durable id to self-heal against, so a corpus-internal relative path would shatter on a move; the pointer is resolved from the repository root.

- **The authority is external, so it is neither a typed relation nor a Verification.**
  A typed relation joins two artifacts by durable id, and an external authority is not an artifact and carries no id, so the pointer is a path, not a relation.
  And the executable check of an implementation against the Specification stays the Verification kind.

## Forces and trade-offs

Naming the empty-list tier a weaker control, rather than "falsifiable by review," costs the model its most reassuring phrase and buys the honesty a method about trust and drift cannot do without.
A reviewer of a no-authority Specification checks it against the corpus's own house shape, which is the method; that catches malformedness, not wrongness, and calling it validation would be the say-so the requirement exists to forbid.

The maturity preference has teeth for the same reason: a governance-soft format is independent of the method but not stable, so it weakens the guarantee it appears to strengthen; routing soft formats to derived-export status keeps the field's promise honest.

Putting the source of truth in the frontmatter and leaving the section optional keeps one canonical declaration a checker reads directly.
Gating the field at `strict` keeps it proportionate: a prototype or a brownfield scope pays nothing, and the discipline arrives with the rigor a regulated or audited corpus already wants.
Allowing more than one authority fits a design genuinely fixed by two contracts, while the one-unit-one-file instinct still applies as a smell test: a Specification answering to several unrelated authorities is usually a signal to split it.

## Alternatives considered

- **Frame the no-authority case as "the Specification is its own authority, falsifiable by review," a single tier.**
  Rejected as an overclaim.
  Review against the corpus's own house shape is a check against the method, not against an authority independent of it, so naming it a form of validation is exactly the say-so the requirement forbids; the two-tier framing states the weaker control plainly instead of dressing it as the stronger one.

- **Restrict the authority to machine-readable contracts only.**
  Rejected: it strands the high-stakes domains that answer to a completeness standard, security to a verification standard, privacy to a control catalogue, at the review-gated tier when a real external standard exists to check them against.
  The authority is any external standard the design answers to, not only one it generates.

- **Make the `## Authority` section the source of truth and the field optional.**
  Rejected: the forcing function belongs in the computable place.
  A required prose section is opaque to a checker, which would have to parse prose to tell a considered absence from a forgotten section; a required frontmatter field, with an empty list as the explicit no-authority case, is decidable from the files alone.

- **Name the section "Checked against", "Validated against", or "Verified against".**
  Rejected, each on a collision.
  "Verified against" collides with the Verification kind; "Validated against" collides with the Validation tier, the confidence dial; and "Checked against" collides with the manifesto's own "specifications are checked against intent", which on a Specification reads as the `satisfies` direction, the opposite of what is meant.
  The Requirement already coined the noun, an authority independent of the method, so the field and the section reuse it ([Reuse established vocabulary before coining new terms](established-vocabulary-first.md){id=note:dec:8f3m5vk}).

- **Fold the implementation-checker into the field or the section.**
  Rejected: it double-homes a check the Verification kind already represents, against [Single Source of Truth](../principles/single-source-of-truth.md){id=note:principle:8691937}, and contradicts the model the method already states, where an OpenAPI contract test verifies the Specification.

- **Carry the authority as a closed frontmatter enum of authority kinds.**
  Rejected: the set of external authorities is open (OpenAPI, JSON Schema, AsyncAPI, Gherkin, a DDL grammar, an authorization model, a control catalogue, and whatever an adopter brings), so a closed enum would lie; a list of pointers names the authority without fixing the set.

- **Introduce a Specification subkind per domain (an api kind, a schema kind).**
  Rejected against [Earned Substance](../principles/earned-substance.md){id=note:principle:yecemfe} and the universal-subject discipline: the domains are software-specific and would explode the kind set; a domain is a navigation grouping and a template label, not a kind, and the per-Specification authority lives in the field.

## Driven by

- groundedIn: [Independently validatable specifications](../requirements/system/independently-validatable-specifications.md){id=note:req:fph0vnr}
- groundedIn: [Verifiable, independently checkable design](../requirements/stakeholder/verifiable-independently-checkable-design.md){id=note:req:vh3k82n}
- groundedIn: [The default spine pack](spine-pack.md){id=note:dec:4tzn3av}
- groundedIn: [Earned Substance](../principles/earned-substance.md){id=note:principle:yecemfe}
- groundedIn: [Proportionality](../principles/proportionality.md){id=note:principle:es0vhzn}

## Worked example

A create-link API Specification answers to an OpenAPI document, named in the field and explained in the optional section:

```markdown
---
id: shortr:spec:k3m9p2x
name: Create Short Link API
kind: specification
status: current
authority:
  - contracts/links.openapi.yaml
---

The create-link endpoint accepts a long URL and an optional custom slug,
and returns the short link, or a typed error when the slug is taken or the URL is malformed.

## Authority

OpenAPI 3.1, at `contracts/links.openapi.yaml`.
That document fixes the path, the request and response schemas, and the status codes;
where the two disagree the OpenAPI document governs.
```

A graceful-degradation Specification answers to no external authority, and its empty list discloses that plainly:

```markdown
---
id: shortr:spec:p7w2n4q
name: Degradation Policy
kind: specification
status: current
authority: []
---

When the pricing service is unavailable, the cart shows the last cached price and blocks checkout
rather than failing open.
```

The empty list is not a validation claim: no external standard fixes this behavior, so it is a design commitment checked by review.
Whether a running implementation honors either Specification is a separate Verification that `verifies` it, never part of the `authority` declaration.
