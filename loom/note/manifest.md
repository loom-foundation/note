---
methodVersion: 0.5.0
namespace: note
profile: strict
packs: [spine, discovery]
---

# Manifest

The corpus manifest for the `note` corpus: the method version it targets, the conformance profile it adopts, and the kind packages it enables, declared once and readable without any tool.

Its placement, field set, and configuration framing are decided in [The corpus manifest](decisions/corpus-manifest.md){id=note:dec:mf3k9w2}.

- **methodVersion** `0.5.0`: the version of the Note method this corpus is written against.
  Note is pre-release; the scheme is major.minor.patch over the method's specifications, with no weaker pre-1.0 promises, fixed in [The method version scheme](decisions/method-version-scheme.md){id=note:dec:v5chm3s}.
- **namespace** `note`: the corpus's identity-space prefix; every artifact's id carries it, and it is the same across any repository this corpus spans ([Namespace](terms/identity-and-references/namespace.md){id=note:term:x494sn0}, [The multi-root corpus](decisions/multi-root-corpus.md){id=note:dec:0n14gqx}).
- **profile** `strict`: this corpus adopts every opt-in rigor discipline (the full per-kind body sections, inclusion tests and Origins on terms, EARS phrasing, typed term-relations, and verifications on current requirements), dogfooding the method at its most rigorous.
  This corpus dogfoods the method at its most demanding configuration; an adopter's starting point is `standard` on the spine pack, per the reference's Day One.
  The named profiles (`bare`, `standard`, `strict`) and the rigor each bundles are fixed in [Conformance profiles as pure rigor bundles](decisions/conformance-profiles.md){id=note:dec:cf7n2wq}.
- **packs** `[spine, discovery]`: this corpus enables both built-in kind packages, the spine pack (the trace spine, plus decisions, terms, conventions, principles, context, and acceptance criteria) and the discovery pack (offerings, value propositions, and the Value Proposition Canvas facets), because it dogfoods both.
  Kind availability is the pack axis, fixed in [Kind-agnostic substrate and kind packages](decisions/substrate-and-kind-packages.md){id=note:dec:w4awceq}.

This corpus declares no `vocabulary` map: it authors in canonical tokens throughout ([The manifest vocabulary map](decisions/vocabulary-map.md){id=note:dec:wn3xsjw}).
Being single-scope, it declares no scope block.
A scope within the corpus may declare its own profile or packs; this manifest sets the corpus default.
