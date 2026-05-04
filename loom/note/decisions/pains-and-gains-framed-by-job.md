---
id: note:dec:tyf5xxw
name: Pains and gains framed by their job
kind: decision
status: current
decided: 2026-07-02T00:00:00Z
---

A Pain or Gain may name the specific Job it is felt against, within its own Need, through an optional typed relation `framedBy` authored on the facet, whose derived inverse `frames` reads from the Job.
The relation encodes, at facet granularity, a framing the discovery pack already states only in prose; it is optional and repeatable, and its target Job is `partOf` the same Need as the facet.

## Context

The discovery pack models a Need as a profile over its Job, Pain, and Gain facets, each a first-class file carrying one typed edge, `partOf` the Need ([Atomic facets](atomic-facets.md){id=note:dec:af3k9w2}).
The methodology's own definitions assert a relationship the files do not encode: a Pain is "a negative outcome … a persona wants to avoid *while getting a Job done*", a Gain is "a positive outcome a persona wants to achieve *while getting a Job done*", and a Job is "the framing facet of a Need, the thing against which its Pains and Gains are felt".
The framing is therefore named in three term definitions but carried by no relation: all three facet kinds are flat siblings, each only `partOf` the Need.

In a Need with a single Job the gap is harmless: the framing Job is unambiguous, and the relationship is trivially inferable.
In a Need with two or more Jobs it bites.
A corpus review of twenty-four Needs, many with two to four Jobs, found that Pains and Gains frequently cluster against one Job in the set, and that the cluster lived only in the prose.
Two consequences followed.
A reviewer could not mechanically tell which Jobs had Pains, which had Gains, and which had neither.
An agent working a single Job had no principled way to load only the facets that contextualise it; it had to load every sibling and lean on text proximity, the inference the file-native model exists to remove.

A note worth recording from the same review: facet personas and Job personas do not always partition together.
A Need's Jobs may share a persona (two Jobs both held by a Systems Engineer), and a facet may carry a persona no Job in the Need carries.
So the framing a reader wants is genuinely task-level, not who-level, and it is not recoverable from the `persona` field.

## Decision

- **An optional `framedBy` relation, facet to Job.**
  A Pain or a Gain may author `framedBy` against a Job within its own Need.
  The verb is authored on the dependent end, the facet, exactly as every relation is; its inverse `frames` is a derived view read from the Job, never authored.
  It is a body relation in the facet's `## Relations` section, in the standard line form `- framedBy: [Job name](relative/path.md){id=…}`, not a frontmatter field: it is a typed link between two artifacts with constrained source and target kinds, which is what the relation machinery is for, and authoring it in `## Relations` is what lets the bundled checker validate its path and id and flag a renamed or deleted target Job with no checker change.

- **Optional and repeatable, zero-or-more.**
  A facet felt against one Job authors one `framedBy`; a facet felt against several authors one edge each; a facet that spans the whole Need, or whose persona no Job carries, authors none.
  Optionality is deliberate and load-bearing: not every Pain or Gain answers to a single Job, and the model must not force a facet that spans the Need to name a Job it is not felt against.

- **The target Job is in the same Need.**
  A `framedBy` target is a Job that is `partOf` the same Need as the facet.
  A target in a different Need is a finding surfaced by pack-aware validation, at the same tier as the facet-persona subset check ([Facet persona field](facet-persona-field.md){id=note:dec:aj00tq7}); the parent Need is computed through the facet's `partOf` edge, and the tool reports the disagreement rather than resolving it.

- **Absence carries no completeness claim.**
  Because the edge is optional, the absence of a `framedBy` on a facet does not mean its Job has no Pain: absence reads as "spans the Need, or not classified".
  `framedBy` therefore yields the positive view "which Jobs are framed by a Pain or Gain", and informs but does not close an uncovered-Job audit.
  This is the accepted price of optionality, recorded here so the signal is not over-read.

- **The verb is `framedBy`, its inverse `frames`.**
  The name is not coined; it promotes the Job term's own load-bearing word, "the *framing* facet … the thing against which its Pains and Gains are felt", into an encoded edge ([Established vocabulary first](established-vocabulary-first.md){id=note:dec:8f3m5vk}).
  It reads as a true sentence in both directions: a Pain is `framedBy` a Job, and a Job `frames` a Pain.

## Forces and trade-offs

The relation must carry load `partOf` does not, or it fails Earned Substance.
It does, but only in the multi-Job case: where a Need has one Job the framing is unambiguous and `framedBy` is omitted, so the verb costs the single-Job majority nothing and earns its place exactly where two or more Jobs make the cluster real.
It also carries load the `persona` field cannot: two Jobs in a Need may share a persona, so the who-axis does not discriminate among them, while `framedBy` names the task a facet is felt against directly.

The chief tension is between optionality and the coverage signal.
Three advisor personas, an adopter, a product owner, and an agent consumer, independently pressed to make the edge required in multi-Job Needs with an explicit "whole-Need" marker, so that absence would be unambiguous.
That was declined: it would force a facet that genuinely spans the Need, or whose persona no Job carries, to name a Job it is not felt against, the precise lie optionality exists to prevent.
The push was instead absorbed where it fits the constraint: the edge is repeatable, so a facet felt against several Jobs states that positively, one edge each, rather than falling silent; only a true whole-Need facet omits.
The residual ambiguity of a bare absence is then accepted and recorded, not designed away.

A sideways edge between sibling facet files is a new kind of reference for this corpus, which until now kept facet edges pointing up to the parent.
A renamed or deleted target Job breaks the path or id and the checker catches it.
A Job *split*, where the id survives on one half, does not break the reference but may strand its meaning on the wrong half; this is the ordinary [Staleness](../terms/drift/staleness.md){id=note:term:psh3vcg} every id-stable edge carries when its target is divided, not a hazard peculiar to this verb, and it is a tripwire for re-checking framed facets after a Job is split, not a reason to forgo the edge.

## Alternatives considered

- **Author `frames`/`contextualizes` on the Job (the governing end).**
  Rejected: it authors the edge on the wrong end and makes the facet-to-Job direction the derived one, inverting the rule that a relation is authored once on the dependent end and its inverse is never authored ([Single authoritative representation per relationship](../requirements/system/single-authoritative-relation.md){id=note:req:s5fh0e8}).
  The facet depends on the Job for its frame, not the reverse, so the facet is the dependent end.

- **A different verb: `feltAgainst` or `arisesFrom`.**
  `feltAgainst` reads true but coins a fresh word when the Job term already supplies "framing", against reaching first for the canon's established term.
  `arisesFrom` is rejected as semantically wrong: a Pain is felt *while* a Job is done, it does not *originate from* the Job, and the verb would assert a causal claim the model does not make.

- **Derive the framing from the `persona` field instead of a new verb.**
  Rejected: the join is ambiguous where two Jobs share a persona, and empty where a facet's persona matches no Job, which is exactly the multi-Job case the relation is for; persona partitions by who, `framedBy` by which task, and they are not the same cut.

- **Make the edge required in multi-Job Needs, with an explicit whole-Need marker.**
  The advisors' counter-proposal.
  Rejected as the cardinality rule because it forces whole-Need and persona-orphaned facets to name a Job they are not felt against; its sound core, that spanning should be stated rather than inferred, is kept by making the edge repeatable so multi-Job framing is authored positively.

- **Decompose so each Need has exactly one Job.**
  Rejected: it contradicts the settled model of a Need as a profile over several Jobs ([Atomic facets](atomic-facets.md){id=note:dec:af3k9w2}), multiplies Needs, and loses the persona-coherent grouping a Need exists to hold, while still not separating two Jobs that share a persona.

- **A frontmatter field rather than a body relation.**
  Rejected: this is a typed inter-artifact link, not an enrichment attribute like `subkind` or a facet `persona`, and a frontmatter field would sit outside the relation machinery and the checker's path-and-id validation, forfeiting the deletion check the requirement asks for.

## Driven by

- groundedIn: [Atomic facets](atomic-facets.md){id=note:dec:af3k9w2}
- groundedIn: [Established vocabulary first](established-vocabulary-first.md){id=note:dec:8f3m5vk}
- groundedIn: [Single authoritative representation per relationship](../requirements/system/single-authoritative-relation.md){id=note:req:s5fh0e8}
- groundedIn: [Earned Substance](../principles/earned-substance.md){id=note:principle:yecemfe}
- groundedIn: [Proportionality](../principles/proportionality.md){id=note:principle:es0vhzn}
- groundedIn: [Single Source of Truth](../principles/single-source-of-truth.md){id=note:principle:8691937}
