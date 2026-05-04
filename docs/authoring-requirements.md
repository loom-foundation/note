# Authoring requirements

How to write a good obligation once you reach the requirement layer: keep it solution-free, split it at the right grain, and record when a design choice determined its content.
This is orientation and applied guidance, not normative text; the binding rules live in the Requirement, Need, Constraint, and Type terms under `loom/note/terms/`, in [Finely addressable intent](../loom/note/requirements/system/finely-addressable-intent.md), and in [Constrained, checkable obligation phrasing](../loom/note/requirements/system/constrained-checkable-phrasing.md).

## Keep the obligation solution-free

A Requirement states an obligation on an observable property or behavior; the mechanism that meets it belongs in a Specification.
A Need states the problem, in the persona's own terms, and names no solution at all.
The one exception is a Constraint, which may name a mechanism when an external force imposes it, and only when it carries that force as its source.
These are the rules the Requirement, Need, Constraint, and Type terms define; the guidance here is how to apply them.

Prefer the verb *ensure* over *define* where the obligation is a property.
Drawing on this corpus's own requirements, "Note shall define a lifecycle taxonomy" presupposes the solution is a taxonomy, while "Note shall ensure an artifact's authority state is legible and its status changes are constrained to a well-formed set" states the property and leaves the taxonomy to a specification.

A worked example, again from this corpus.
"Note shall detect changes to a referenced artifact using content fingerprints recorded in the link" names a mechanism (fingerprints) with no external force, so it fails the rule.
The solution-free form states the property instead: "When a dependent artifact relies on another, Note shall make it detectable that the referenced artifact has changed since the dependency was established, and shall distinguish a change in the referenced text from a divergence between an implementation and the contract it claims to honor."
The fingerprint and the bound check belong in a specification.

On the customer side the same discipline holds, with a lighter touch.
A Need, Pain, or Gain is stated in the persona's voice and may name the kind of thing they need in their own domain ("I need a stable API so my code does not break and I do not have to re-integrate"), because that is their world, not a prescribed solution.
It crosses the line only when it obligates the system ("Shortr shall provide a stable API" is a Requirement) or prescribes a specific mechanism, format, or standard ("a versioned endpoint using the XYZ standard" is a leaked solution).
What the product offers in answer is a Pain Reliever or Gain Creator on an Offering, not a facet of the Need.

## Right-size the decomposition

Split two obligations into separate Requirements when they differ in any of: the evidence that would verify them; the Need or external force that is their source; their volatility (one could change or retire without the other); the boundary they sit on (one satisfiable inside the system, the other routing to an Orchestrating Authority); or their optionality (one core, one opt-in per profile).
Keep them together only when they are true-or-false as a single unit.

The criterion guards both directions.
Bundling distinct obligations hides them and makes the bundle impossible to verify cleanly; atomizing obligations that always move together multiplies artifacts and links without earning the cost (see [Earned Substance](../loom/note/principles/earned-substance.md)).

## Frontmatter and vocabulary

A requirement carries the common required envelope: `id`, `name`, `kind: requirement`, and `status`.
There is no `title` field; the designation lives in `name`.
The `id` is a uniform opaque identifier in the form `<namespace>:req:<opaque>`, where the opaque part is a seven-character Crockford Base32 string, minted once and never changed.

```yaml
---
id: acme:req:7k4m9pn
name: Checkout latency budget
kind: requirement
status: current
---
```

Optional fields `level` (`stakeholder` or `system`) and `type` (`functional`, `non-functional`, or `constraint`) may be added; a profile may require them.

When a design choice determined the content of a requirement, the requirement carries a `decidedBy` edge in its `## Relations` section, pointing at the decision:

```markdown
## Relations

- addresses: [Fast checkout need](../needs/fast-checkout.md){id=acme:need:3n7q8vp}
- decidedBy: [Latency budget decision](../decisions/latency-budget.md){id=acme:dec:2m8k4wn}
```

The `decidedBy` edge belongs on the requirement, not on the decision; the decision's `## Driven by` carries only `groundedIn` and `amends`.

## Acceptance criteria

An **acceptance-criterion** is a distinct spine-pack kind (kind-segment `ac`).
It is a solution-free condition under which a requirement or need is acceptable: the measurable threshold or observable outcome by which "acceptable" is judged, naming no mechanism.
It is authored before build, not derived from a design.

An acceptance-criterion is distinct from a verification.
A verification is the executable check that confirms the condition holds; the acceptance-criterion is the declarative statement of what acceptable means.
A verification may `verifies` an acceptance-criterion directly; the requirement is then met transitively through the `qualifies` edge.

### The on-ramp: inline section

A `## Acceptance criteria` section authored on a requirement is a permitted authoring on-ramp.
An author need not mint a separate file for every criterion from the first draft; they may list the conditions inline:

```markdown
---
id: acme:req:7k4m9pn
name: Checkout latency budget
kind: requirement
status: draft
---

The checkout flow shall complete within two seconds at the 95th percentile under normal load.

## Acceptance criteria

- p95 latency is at or below 2000 ms, measured from the user's submit action to the confirmation page render, under a load of at least 100 concurrent sessions.
- The measurement is reproducible in the staging environment using the standard load profile.

## Relations

- addresses: [Fast checkout need](../needs/fast-checkout.md){id=acme:need:3n7q8vp}
```

### Promotion to standalone artifacts

The standalone acceptance-criterion kind is the canonical, promoted form.
When a criterion is traced to, referenced from a verification, or verified directly, it earns its own file.
A tool promotes a bundled `## Acceptance criteria` section into individual acceptance-criterion artifacts; the same bundled-draft-to-facets promotion pattern as need facets.

A promoted acceptance-criterion carries the common envelope plus a required `## Relations` section that `qualifies` exactly one requirement or need:

```markdown
---
id: acme:ac:8w2k5np
name: Checkout p95 latency threshold
kind: acceptance-criterion
status: current
---

The checkout flow's p95 latency is at or below 2000 ms, measured from the user's submit action to the confirmation page render, under a load of at least 100 concurrent sessions.

## Out of scope

This criterion does not govern p50 latency or latency under error conditions.

## Relations

- qualifies: [Checkout latency budget](../requirements/checkout-latency-budget.md){id=acme:req:7k4m9pn}
```

### Out of scope section

A `## Out of scope` section on an acceptance-criterion is recommended at the `standard` profile.
It states what the criterion does not require, guarding against a reading broader than intended.
One short paragraph or a short list is sufficient; the goal is to close the most plausible over-reading.
