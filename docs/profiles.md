# Conformance profiles

A profile is the rigor axis of the manifest: one of `bare`, `standard`, or `strict`.
It sets how much discipline every artifact in a scope must carry, and it is wholly separate from `packs`, which select which artifact kinds exist at all.
Packs answer "which kinds"; the profile answers "how rigorous."

## bare

`bare` is the conformance floor.
An artifact conforms at `bare` when it has a well-formed envelope (UTF-8, YAML frontmatter delimited by `---`, one artifact per file), the four common required frontmatter fields (`id`, `name`, `kind`, `status`), the per-kind required frontmatter its pack declares (for example, the `persona` field on a need), and a lead (an unheaded opening statement of the artifact's substance).
No body sections beyond the lead are required.
A validator reports nonconformance when any of those elements is absent or malformed.

## standard

`standard` is `bare`, plus two additional obligations.

First, each kind's required body sections must be present.
The spine pack marks `## Relations` required on requirement, specification, verification, and acceptance-criterion; and marks `## Context`, `## Decision`, `## Forces and trade-offs`, `## Alternatives considered`, and `## Driven by` required on decision; and marks `## Criteria`, `## Procedure`, and `## Relations` required on verification; and `## Why this matters` and `## How to apply` required on principle; and `## External entities`, `## What crosses the boundary`, and `## What is out of scope` required on context.
The discovery pack marks `## Relations` required on offering, value-proposition, job, pain, gain, pain-reliever, and gain-creator.
A validator reports nonconformance when a required section is absent.

Second, each design choice must be recorded in a decision artifact.
An undocumented choice that shaped the corpus does not conform at `standard`.

## strict

`strict` is `standard`, plus the profile-gated disciplines.

**Term inclusion tests and Origins.**
Every term artifact must carry an `## Inclusion test` section (a decision question that classifies a candidate as in or out of the term's scope) and an `## Origin` section (the relevant general-English sense, plus the professional or standards lineage that sharpens the term for this corpus).
A validator reports nonconformance on a term that lacks either section.

**Typed term relations.**
Where relationships between terms exist, they must be expressed as typed links from the substrate's closed term-relation set (`is a`, `is a value of`, `is part of`, `carries`, `scopes`, `contrasts with`, `relates to`), authored once on the end shown.
A validator reports nonconformance on a term whose cross-term relationships are stated only in prose.

**EARS requirement phrasing.**
EARS (Easy Approach to Requirements Syntax) constrains how requirement sentences are written: they follow fixed trigger-response templates such as "When X, the system shall Y," ensuring that every obligation names a condition and a response in a form a checker can parse and a reviewer can test against.
Every requirement artifact must phrase its lead in an EARS-compliant form.
A validator reports nonconformance when a requirement's lead does not follow an EARS template.

**Verifications expected on current requirements.**
Every requirement at `status: current` is expected to have at least one verification artifact linked to it via the `verifies` relation.
A validator reports a finding on a current requirement that has no verification; the artifact itself stays well-formed, and the findings are the owner's surfaced work queue.

**Independent authority on specifications.**
Every specification must declare its authority in the `authority` frontmatter field: a list of repository-relative paths to the external authorities its design answers to (a machine-readable contract, or a completeness standard the design is checked against), or an empty list when no external authority applies.
A non-empty list is the independently validated tier; an empty list is the review-gated tier, declaring the design a commitment checked by review rather than independently validated.
A validator reports nonconformance on a specification with no `authority` field.
The optional `## Authority` section adds commentary; the field is the source of truth.

A principle artifact must also carry an `## Origin` section at `strict`.

## Choosing

**Throwaway prototype or brownfield spike.**
Use `bare`.
You get a valid, identifiable corpus with minimal ceremony; none of the body sections are required and no design choices need decision records.

**Most teams and most projects.**
Use `standard`.
You get real traceability (relations, required body sections, a decision record per design choice) without the heaviest rigor.
This is the Day One recommendation in the adopter reference.

**Regulated or audited corpus.**
Use `strict`.
Term discipline, constrained requirement phrasing, expected verifications on every current obligation (with any gap reported as a finding), and a declared authority on every specification make the corpus defensible under an external assessment framework.

## Raising a profile later

Adoption is monotonic.
Raising a scope's profile from `bare` to `standard`, or from `standard` to `strict`, may require adding sections to existing artifacts, but it never invalidates an artifact that was already valid under the lighter profile.
Raising never changes an artifact's identity and never breaks a relation.
The climb is safe because each profile is a strict superset of the disciplines below it.

## Per-scope override

The manifest sets the corpus default, and any scope may declare its own profile.
A mature corpus at `strict` can give a brownfield application its own child scope at `bare`, so its legacy artifacts conform without requiring a mass retrofit.

Parent scope manifest (`loom/note/manifest.md`):

```markdown
---
methodVersion: 0.5.0
namespace: acme
profile: strict
packs: [spine]
---

# Manifest

The corpus manifest for acme: the method version, the namespace, the conformance profile, and the enabled packs.
```

Child scope manifest (`loom/note/payments-legacy/manifest.md`):

```markdown
---
methodVersion: 0.5.0
profile: bare
packs: [spine]
scope:
  id: acme-payments-legacy
  parents: [acme]
---

# Manifest

The manifest for the payments-legacy scope: a brownfield application inside the acme corpus, adopting the minimum conformance floor while the mature corpus runs strict.
```

The child scope's artifacts conform at `bare`; the parent corpus's artifacts conform at `strict`.
Neither scope's profile affects the other's obligations.

## Normative sources

The profiles and their requirements are fixed in [The substrate](../loom/note/specifications/note/substrate.md){id=note:spec:tkhd63e} (the "Conformance profiles" section) and [Conformance profiles as pure rigor bundles](../loom/note/decisions/conformance-profiles.md){id=note:dec:cf7n2wq}.
