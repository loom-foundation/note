---
id: note:dec:af3k9w2
name: Atomic facets
kind: decision
status: current
decided: 2026-06-12T00:00:00Z
---

The discovery pack models a need and an offering at the granularity of single facets.
Job, pain, and gain are the facets of a need; pain-reliever and gain-creator are the facets of an offering; each is a first-class kind, one file with one opaque id.
A need is a profile over its Job, Pain, and Gain facets, an offering is a value map over its Pain Reliever and Gain Creator facets, and the polarity of a facet is carried by its kind, not by a discriminator field.
The fit between the two sides is a derived view, computed from the `relieves` and `creates` edges and never authored.

## Context

Any sustained body of work that captures the value it offers, whether a software system, a hardware product, a process, or a methodology like this corpus, has to let a trace land on the thing it is about.
The smallest thing worth tracing in the problem space is a single pain, gain, or job, and in the offered-value space a single relief or created gain: a requirement covers *this* pain, a reliever answers *that* one, an audit asks which pains are uncovered.

[Finely addressable intent](../requirements/system/finely-addressable-intent.md){id=note:req:fd8k2w4} already commits the method to intent decomposed into independently addressable units, one per file; this decision carries that commitment down to the facet level, where the traceable units actually live.

These facet kinds belong to the discovery pack.
Kind availability is the pack axis, not the rigor axis: a corpus that enables the discovery pack has the facet kinds; a spine-only corpus does not.
The facets are therefore the discovery pack's data model, the shape an offering and a need take once the value emphasis is in play, rather than a model present at every level of rigor.

The choice was tested two ways before being made.
It was put to three personas that use the method differently, an AI agent on a constrained runner, an author writing from research, and an auditor proving coverage, and the deciding considerations turned out to be data-model ones (an uncovered pain must be an auditable record, identity must be uniform and stable) rather than the ergonomics of reading or editing a single file, which a renderer supplies.
It was also weighed against three commitments that crystallized in the process: one file is one unit is one id; the data model is not the presentation; identity should be legible.
Those commitments, not the prior shape of any kind, settle the design.

## Decision

- **Facets are first-class kinds in the discovery pack.**
  `job`, `pain`, and `gain` (the facets of a need) and `pain-reliever` and `gain-creator` (the facets of an offering) are each one file with one opaque id.
  They are distinct kinds rather than one `facet` kind carrying a discriminator, so that a reference reveals what it targets and relation validity stays kind-based: a `relieves` targets a pain, a `creates` targets a gain.

- **A need is a profile.**
  It carries its `persona` and an optional `validation`, the job-story lead, and its source; its jobs, pains, and gains are member facet artifacts.
  The need remains a first-class artifact, the load-bearing overview that [Group overviews as co-located README files](group-overview-readme.md){id=note:dec:rd6w3k2} keeps as a real artifact rather than prose, not a directory README.

- **An offering is a value map.**
  It carries its benefit-led lead; its relievers and creators are member facet artifacts, and it carries no discriminator field, since polarity lives in the facet kind.
  Its pitch, when worth holding, is a separate value proposition that `expresses` it, per [Offering, fit, and the value proposition](offering-fit-and-value-proposition.md){id=note:dec:cjqwsxt}.

- **Polarity is carried by the facet kind.**
  Whether a facet is a pain or a gain, a reliever or a creator, is its kind, not a `type` field on a single shared kind.
  A pain is relieved and a gain is created, which are different inbound relations, so they are genuinely different kinds rather than one kind in two costumes.

- **Relations.**
  A facet authors `partOf` its parent; a pain-reliever authors `relieves` its pain; a gain-creator authors `creates` its gain.
  The inverses `composedOf`, `relievedBy`, and `createdBy` are derived views, never authored.
  A requirement may `relieves` a pain, `creates` a gain, `addresses` a job, or `delivers` a reliever or creator, at facet granularity.

- **The fit is a derived view.**
  The fit between a need and an offering is the set of `relieves` (reliever to pain) and `creates` (creator to gain) edges; an uncovered pain is a pain artifact with no inbound `relieves`, and an offering's fit is its set of `relieves` and `creates` edges.
  Both are computed, never authored.

- **Layout.**
  Facets are co-located in a directory named for their parent, beside the parent file, which keeps its own descriptive name (`needs/fast-checkout.md` beside `needs/fast-checkout/`), neither renamed to `README.md` nor moved inside the directory.
  That descriptive filename is the parent's identity wherever a path is read without the tool, an editor tab, a fuzzy-finder result, a pull-request changed-files list, a `git log`, an agent's tool-call log, and a generic `README.md` or `INDEX.md` would collapse that identity across every parent at once.
  A parent is therefore identified as the `.md` whose basename matches a sibling directory, not as any `.md` in the kind directory, so a kind- or group-level `README.md` overview ([Group overviews as co-located README files](group-overview-readme.md){id=note:dec:rd6w3k2}) can sit in the same directory without being read as a member.
  Co-location is navigation convenience; `partOf` is the authoritative link, as paths are conveniences and relations are authoritative.

- **Facet lifecycle.**
  A facet that is traced to is never hard-deleted; it is set `status: obsolete` with `superseded_by`, kept as a tombstone so inbound traces still resolve, and a trace to an obsolete facet is a drift finding.

- **Single membership.**
  A facet belongs to one parent ([Grouping of artifacts by directory](artifact-grouping.md){id=note:dec:q8k3w2n}); a pain wanted by two needs is a signal to lift it to a broader scope, not to share one file.

- **A bundled draft is a permitted on-ramp.**
  A facet may start life as a bundled draft inside its parent and be promoted to its own file: the lightweight bundled form is a permitted authoring on-ramp, and a tool promotes it to facets.
  The canonical, stored form is split.

## Forces and trade-offs

The file count rises: a need with four pains becomes four files.
This is accepted because facets are cheap, the count is a presentation concern a renderer answers (a single page assembled from the files), and the return is large: coverage and fit become computable, every facet gets its own history and attribution, and references are opaque ids immune to the silent re-pointing a content-anchored sub-id suffers.

Five kinds press against Earned Substance.
They are accepted because each clears the bar of carrying load at the point of reference and in its relations: a pain is relieved and a gain is created, which are different inbound relations, so they are not one kind in two costumes.

The decisive reframing is that most arguments for keeping facets bundled, reading a whole problem in one file, editing one buffer, a coherent narrative, are about presentation, and presentation is the tool's job; once those are set aside, the data-model case for splitting is one-sided.

The parent's placement is weighed against the one convenience it forgoes: a Git host auto-renders a directory's `README.md`, so a parent renamed to `README.md` would greet a first-time reader with the profile already open.
That convenience is paid back once per arrival, whereas the identity a descriptive filename carries, in tabs, fuzzy-finders, changed-files lists, and `git log`, is read on every edit and every review; the recurring cost dominates, and the arrival convenience is recovered anyway by a group `README.md` that introduces the directory without displacing a member.
A parent kept beside its directory also stays a valid artifact before any facet exists, where a directory-as-parent form would read, half-authored, as a folder of facets with no profile.

Scoping the facet kinds to the discovery pack costs a value-capturing effort one line of configuration to enable the pack.
This is accepted under Proportionality: an effort that captures only its trace spine should not carry a value model it does not use, and the pack axis is exactly the mechanism that holds the facet kinds out of the spine until they are earned.

## Alternatives considered

- **Keep the need bundled and address its facets with intra-file sub-ids.**
  Rejected: a second addressing scheme found nowhere else in the method, an absence that cannot be audited (a never-minted sub-id is not a record), and an anchor that re-points when the prose around it is edited.

- **One `facet` kind discriminated by a `type` field.**
  Rejected: opaque references and relation validity keyed off a field rather than a kind, against legible identity.

- **A `job` kind plus an `outcome` kind carrying `type: pain | gain`.**
  Considered as the compromise that keeps polarity pairs merged; rejected in favor of fully distinct kinds for legibility and for symmetry with the offering side.

- **Make the facets the data model at every level of rigor, gated by the profile axis.**
  Rejected: it ties kind availability to the rigor axis, the residue of the old model where the heaviest profile also switched on the richest kinds; kind availability is the pack axis, so the facets are the discovery pack's data model, not the floor's.

- **Move the parent file inside its facet directory, renamed `README.md`.**
  Rejected: it wins a Git host's directory auto-render but renames every parent to the same `README.md`, collapsing the parent's identity in editor tabs, fuzzy-finders, changed-files lists, and `git log`, where the descriptive filename is the only signal of which parent is in hand; the auto-render it chases is already earned, as prose, by a group `README.md` that displaces no first-class artifact.

- **Move the parent file inside its facet directory, renamed `INDEX.md`.**
  Rejected: it pays the same identity cost as the `README.md` form and earns nothing back, since a plain Git host does not auto-render `INDEX.md`.

- **Move the parent file inside its facet directory, keeping its descriptive name (`fast-checkout/fast-checkout.md`).**
  Rejected: it keeps a unique filename but duplicates the directory name in the path and couples a rename to two places, and it forfeits the parent-stands-alone property, since a need with no facets yet would otherwise be a single valid file rather than a directory.

## Driven by

- groundedIn: [Kind-agnostic substrate and kind packages](substrate-and-kind-packages.md){id=note:dec:w4awceq}
- groundedIn: [Finely addressable intent](../requirements/system/finely-addressable-intent.md){id=note:req:fd8k2w4}
- groundedIn: [Earned Substance](../principles/earned-substance.md){id=note:principle:yecemfe}
- groundedIn: [Single Source of Truth](../principles/single-source-of-truth.md){id=note:principle:8691937}
- groundedIn: [Proportionality](../principles/proportionality.md){id=note:principle:es0vhzn}

## Worked example

A need carries its facets in a co-located directory beside it:

```
needs/
├── know-the-system-boundary.md        # the profile
└── know-the-system-boundary/
    └── pain-reader-divergence.md       # a pain facet
```

The pain is a one-line lead plus a `partOf` edge naming its parent need by id.
A pain-reliever in an offering authors `relieves` against that pain by id, and a requirement that delivers that reliever closes the trace.
Asking "which pains are uncovered" is then a query for pain artifacts with no inbound `relieves`, not a reading of prose.
