---
id: note:dec:swar6np
name: The system-of-interest provides the value
kind: decision
status: current
decided: 2026-07-02T00:00:00Z
---

The discovery pack gains a `system` kind: the system-of-interest under design, a product, a service, a piece of hardware, or any arrangement that achieves a purpose, that `provides` an offering's value.
It is the Value Proposition Canvas's third value-map element, Products and Services, written generally and made first-class; the prose claim "the System provides the offering" becomes an authored `provides` edge, the offering-side counterpart of the need-side `framedBy`.
The kind is optional, versioned by tagged snapshots rather than a release kind, and its `provides` claim is substantiated by the as-built evidence (the upward `@intent` citations in code and commits, or, for a non-code deliverable, a test report or sign-off), never by an authored downward edge.
Allocating requirements to the system that owns them is a deliberate further step, deferred.
A panel review of this draft surfaced questions; each is resolved or explicitly deferred below, and the deferrals are recorded as deliberate.

## Context

The Value Proposition Canvas pairs a customer profile (a need's jobs, pains, and gains) with a value map of three elements: the Pain Relievers and Gain Creators an offering is composed of, and the Products and Services that provide them.
The discovery pack carried the first two but folded the third away: an earlier decision mapped Products and Services to the System, "the system-of-interest under design (a product, a service, or any arrangement achieving a purpose)", and recorded in prose that "the System provides the offering" ([Offering, fit, and the value proposition](offering-fit-and-value-proposition.md){id=note:dec:cjqwsxt}).
That fold was right for the common case and incomplete for the rest.
The System was never a node: it was a Term plus a single Context boundary per scope, so the provider relationship the pack asserts in three definitions was carried by no edge, a single-source-of-truth crack the method elsewhere forbids.

Three pressures made the gap concrete.
The question that opened this was the offering-side counterpart of the need-side framing: a pain or gain now names the Job it is felt against ([Pains and gains framed by their job](pains-and-gains-framed-by-job.md){id=note:dec:tyf5xxw}), so what, on the offering side, does a reliever or creator name?
The answer is not a sibling verb, since a reliever already reaches a job transitively through the pain it relieves, but the missing provider: the thing that provides the value.
A product evolves, and a product owner needs to say what a version delivers without cloning every repository and recomputing coverage from the code.
And a service-oriented architecture implements one offering in bits and pieces across many repositories, so "which system provides which facet, and is it built" has no machine-readable home.

A computed answer exists: a tool can resolve the upward `@intent` citations in each repository against the deployed commits and report coverage.
But it is expensive, demands access to every repository, and is re-run on every deploy.
It is the thorough, ground-truth tier; it is not a thing a product owner consults to answer "what is in v1.0".
The method already has the pattern for this two-tier shape: a Value Proposition is the authored claim and the fit is the computed evidence that substantiates it.
The same split applies to provision: an authored claim of what a system provides, substantiated by the computed as-built evidence.

## Decision

- **A first-class `system` kind, in the discovery pack.**
  It is the system-of-interest that provides value: a product, a service, a piece of hardware, or any arrangement that achieves a purpose.
  It completes the Value Proposition Canvas's value map (Products and Services) the pack had folded away, and it reuses the method's existing [System](../terms/system-and-boundary/system.md){id=note:term:0jbwfkm} concept rather than coining a new word.
  The kind lives in the discovery pack because its provision targets are discovery kinds; it adds no required frontmatter beyond the common envelope.

- **A `provides` verb, authored on the system.**
  A system `provides` the offerings, value-propositions, pain-relievers, or gain-creators it delivers.
  The edge is authored on the system, the provider, and points up to the value; its inverse `providedBy` is a derived view, never authored, so the intent the system answers stays clean and never points down at its provider.
  It is optional and may repeat: a coarse claim names a whole offering or value-proposition, a fine one names the specific relievers and creators a system provides, so an offering built across several systems records which system provides which facet, and full provision of an offering is then a derived view, like the fit.
  It is the offering-side counterpart of `framedBy`: just as a pain or gain names the job it is felt against, a reliever or creator names the system that provides it.

- **Coarse and fine claims compose by facet.**
  In the derived provision view, a `provides` naming a whole offering or value-proposition expands to the relievers and creators that offering is composed of, and the effective provision of an offering is the union of the expanded claims across systems, read at facet granularity.
  Two systems whose claims overlap on a facet read as shared provision, surfaced as information for the owner; a coarse claim beside a finer claim on the same value is redundancy reported the same way, and neither is reconciled silently or policed as an error.

- **Versions are tagged snapshots, not a release kind.**
  The corpus at a tag is that version's claimed value; the `provides` set a system carries there is what that version claims to deliver; the increment between two versions is their diff.
  Git tags are the common mechanism, but any version marker that snapshots the corpus serves, a model year or a published revision, so a non-Git adopter is not excluded.
  The set of commits a deployed version actually comprises is the Orchestrating Authority's record (a tag, a deployment manifest, or optional Records), never a field on the system, which would point durable intent down at a volatile build.

- **An authored claim, substantiated by computed evidence.**
  `provides` is the authored claim, the value-proposition's analogue; the fit's analogue is the computed coverage a tool derives from the upward in-code and in-commit `@intent` citations resolved against the deployed commits.
  For a non-code deliverable the evidence is whatever the authority can resolve against the as-built (a test report, a sign-off, a delivery record), the claim-and-evidence split holding whether or not there is code to scan.
  A divergence between what a system claims to provide and what its code cites is a reportable finding, not an authored correction; the claim is never authoritative over the code.

- **The system is the identity, not the boundary.**
  The system-of-interest is the thing that provides value; the Context states its boundary.
  A corpus with one system keeps it implicit in its single Context and authors a `system` artifact only when more than one system-of-interest must be told apart.

- **Requirement allocation is deferred.**
  Allocating a requirement to the system that owns it (a requirement `allocatedTo` a system) is a separable further step, left to a later decision.
  This version encodes only the value-side provision; it adds no allocation edge and no completeness rule.

## Forces and trade-offs

The kind must carry load no existing kind carries, or it fails Earned Substance.
It does: it is the only node a reliever or creator can name as its provider, the only place a multi-system corpus can attribute value to a product, and the encoding of a provider relationship the pack until now asserted only in prose.
For the single-system corpus the load is absent, there being one provider named by the one Context, so the kind is optional and authored by no one until a second system-of-interest appears.
This is Proportionality: the common case pays nothing, and the kind earns its place exactly where more than one system must be told apart.

Keeping provision an authored claim, rather than only a computed scan, is the decisive trade.
The computed coverage is ground truth but expensive: it demands every repository, scans code and history, and re-runs on every deploy, so it is unfit as the answer a product owner reads to learn what a version delivers.
The authored `provides` claim is cheap to read and cheap to write, and the computed scan becomes its audit rather than the only path to an answer.
The cost is that a claim can drift from the code; the method accepts this exactly as it accepts a value-proposition drifting from its fit: the computed evidence adjudicates, and a divergence is a finding.

Reusing "System" over a fresh word trades a little customer-facing warmth (a product owner may read "system" as engineering-flavoured) for generality and vocabulary coherence: "System" is already the method's term for "a product, a service, or any arrangement achieving a purpose", which is precisely the breadth wanted, and which "release" (software-only), "product" (excludes services and hardware), and "solution" (overloaded, and already rejected for the build) all lack.

Deferring requirement allocation keeps this change to its earned scope.
The value-side provision is well-motivated and light; allocating requirements to a solution element is a heavier, separable move that re-layers the requirements model and imports systems-engineering allocation discipline, and bundling it here would tax the common case for a benefit the value-side change does not need.

## Alternatives considered

- **A `release` kind that lists what a version delivers.**
  Rejected: a release is software-flavoured, where the method is not (it may capture a service, a piece of hardware, a process); a release is also a delivery verdict, which the method holds outside itself, not an intent kind.
  Versioning is carried by Git tags, and the durable provider is the System, of which a release is merely a tagged snapshot.

- **An `introduced_in` / `since` frontmatter field on the value artifacts.**
  Rejected: it makes a durable intent artifact point down at a volatile release label, the wrong direction, and duplicates the version a Git tag already records.

- **A sibling `framedBy`-style verb authored on the offering facets only.**
  Rejected: a reliever or creator already reaches a job transitively through the pain or gain it answers, so a sibling verb would mostly restate the fit; the real offering-side gap was the missing provider node, not a missing verb.

- **A frontmatter field rather than a kind, or authoring `provides` downward on the offering.**
  Rejected: the provider is a first-class thing many value artifacts cite and a version's claim is read off it, which a field cannot carry; and authoring the edge on the offering would make intent depend on its provider, inverting the rule that the dependent end authors the edge and the inverse is derived ([Single authoritative representation per relationship](../requirements/system/single-authoritative-relation.md){id=note:req:s5fh0e8}).

- **A separate "solution" or "allocation" pack for the kind now.**
  Rejected for this change: the value-side provision is the Products and Services element of the Value Proposition Canvas and belongs with the rest of the canvas in the discovery pack, whose kinds its `provides` targets; a later requirement-allocation extension may earn its own pack.

- **Bundle requirement allocation (`allocatedTo`) into this change.**
  Rejected: it is separable and heavier, re-layering the requirements model and importing allocation discipline the value-side change does not need; it earns its own decision when an adopter beyond the dogfooding corpus needs per-product allocation.

- **Make `provides` required, with a coverage-completeness rule.**
  Rejected: a mandatory edge or a "every offering must name its system" audit taxes the common case and imports exactly the completeness ceremony the method's Proportionality refuses; the edge is optional and its absence carries no completeness claim.

## Driven by

- groundedIn: [Offering, fit, and the value proposition](offering-fit-and-value-proposition.md){id=note:dec:cjqwsxt}
- groundedIn: [Pains and gains framed by their job](pains-and-gains-framed-by-job.md){id=note:dec:tyf5xxw}
- groundedIn: [Atomic facets](atomic-facets.md){id=note:dec:af3k9w2}
- groundedIn: [Established vocabulary first](established-vocabulary-first.md){id=note:dec:8f3m5vk}
- groundedIn: [Single authoritative representation per relationship](../requirements/system/single-authoritative-relation.md){id=note:req:s5fh0e8}
- groundedIn: [Earned Substance](../principles/earned-substance.md){id=note:principle:yecemfe}
- groundedIn: [Proportionality](../principles/proportionality.md){id=note:principle:es0vhzn}
- groundedIn: [Single Source of Truth](../principles/single-source-of-truth.md){id=note:principle:8691937}
- groundedIn: [Know the real product behind the intent](../needs/know-the-real-product.md){id=note:need:m0h1ncg}

## Panel findings and their resolutions

A blank-slate panel on the draft (a product owner, a platform engineer, a non-software adopter, a single-product minimalist, and an adversary) ratified the model and its Proportionality and surfaced five questions, concentrated in the multi-system case the kind exists for.
Each is resolved or explicitly deferred; none is silently dropped.

- **The `system` kind and the Context kind overlap.**
  Deliberated and settled in [The system/Context overlap is deferred to allocation](system-context-overlap-deferred.md){id=note:dec:yy8j83d}: the overlap is a symptom of the deferred requirement allocation rather than an independent defect, the status quo is retained, and the relationship resolves when allocation is taken up.

- **The `provides` claim is not auditable from the corpus alone.**
  Resolved by the boundary this decision already draws: the audit's out-of-band input, which repository a system maps to and which commits a version comprises, is the Orchestrating Authority's record, optionally carried as a Record where an adopter wants it in-tree, and never a field on the system.
  The full multi-system audit additionally needs the requirement allocation deferred below, so the audit machinery arrives with allocation; until then the claim-and-evidence split stands and a partial audit (resolving citations without per-system attribution) remains possible.

- **The deferred requirement allocation is load-bearing for the audit.**
  Deferred by design: the Decision defers allocation explicitly, and with it the per-system attribution of code coverage.
  This is a recorded dependency, not an oversight; taking up allocation reopens both together.

- **Coarse and fine `provides` claims have no composition rule.**
  Resolved: the "Coarse and fine claims compose by facet" bullet above fixes the derived view as expansion to facets, union across systems, and overlap surfaced as shared provision, never silently reconciled.

- **Whether to author `provides` at all.**
  Deliberated and settled in [The system/Context overlap is deferred to allocation](system-context-overlap-deferred.md){id=note:dec:yy8j83d}: derivation in place of authorship is rejected, because it collapses the authored-claim and computed-evidence split and rests on advisory, never-checked citation keys.

## Worked example

A link shortener, Linkly, is built as three services in three repositories: `gateway`, `aliases`, `analytics`.
The corpus authors three `system` artifacts and points each at the value it provides:

```
systems/
├── gateway.md      # provides: Short links (offering)
├── aliases.md      # provides: Custom aliases (offering), Links never expire (pain-reliever)
└── analytics.md    # provides: Share insights (gain-creator)
```

To answer "what does Linkly 1.0 deliver", a reader checks out tag `v1.0` and reads the systems' `provides` edges: one read, no repositories cloned.
To prove it, a tool resolves the `@intent Satisfies:` citations in each service at the v1.0 commits against the requirements behind those offerings; a claimed-but-uncited offering is a finding.
"What is new in v2.0" is the diff of the `provides` edges between the two tags.
