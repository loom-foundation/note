# Authoring pains and gains

How to capture a persona's Pains and Gains, and an offering's Pain Relievers and Gain Creators, so each facet carries distinct load instead of being the polar opposite of another.
This is orientation and applied guidance, not normative text; the binding rules live in the [Pain](../loom/note/terms/artifact-kinds/pain.md){id=note:term:hb74nmn}, [Gain](../loom/note/terms/artifact-kinds/gain.md){id=note:term:7e4f92v}, [Pain Reliever](../loom/note/terms/artifact-kinds/pain-reliever.md){id=note:term:7qrdxnp}, and [Gain Creator](../loom/note/terms/artifact-kinds/gain-creator.md){id=note:term:g9fxrs5} terms and their inclusion tests, and in [Earned Substance](../loom/note/principles/earned-substance.md){id=note:principle:yecemfe}.
For the model these facets sit in, see [from-need-to-specification.md](from-need-to-specification.md).
To draft the underlying Job or Need first, see [authoring-the-discovery-pack.md](authoring-the-discovery-pack.md) for the "As a [persona], when [situation], I want [outcome], so [why]" formulation.

## The mirror-image trap

A Pain says what a persona suffers or fears; a Gain says what they want.
The recurring mistake, made by humans and agents alike, is to write a Gain that is nothing more than the Pain turned positive: a Pain of "the mapping drifts in a spreadsheet" paired with a Gain of "the mapping does not drift."
The second carries no information the first did not.
It reads as two facets but is one, written twice.

The same trap waits on the offering side: a Pain Reliever turned positive becomes a Gain Creator that says only "the pain is gone," and a Gain Creator turned negative becomes a Reliever in disguise.

A facet that only inverts another has not earned its place ([Earned Substance](../loom/note/principles/earned-substance.md){id=note:principle:yecemfe}).
It inflates the facet count, doubles what a reader and an agent must take in, and gives the fit nothing real to cover.

## The test: do the sought outcomes genuinely differ?

The [Pain](../loom/note/terms/artifact-kinds/pain.md){id=note:term:hb74nmn} and [Gain](../loom/note/terms/artifact-kinds/gain.md){id=note:term:7e4f92v} inclusion tests fix the rule; the applied form is this: keep a Pain and a Gain on the same Job both only where the outcome the persona wants to avoid and the outcome they want to reach are genuinely different, not two descriptions of one thing.

Ask of a candidate Gain: strip the Pain it sits beside, and does anything remain that the persona positively seeks?
If the only content is "that Pain does not happen," fold it into the Pain and drop the Gain.
If a distinct outcome remains, both have earned their place.

The same question, mirrored, polices a Pain drafted beside a Gain, and a Reliever drafted beside a Creator.

## Start from the primary motivation

Before writing either, decide what actually moves the persona here: a hurt they want to escape, or a benefit they want to reach.
That primary motivation is the facet to author first and to author well.
Lead with it; reach for the second facet only when the persona is genuinely pulled from both sides and the two pulls name different outcomes.

A Pain-led Job and a Gain-led Job are both normal.
What is not normal is every Job carrying a matched pain-and-gain pair, each the other's reflection; that pattern is the smell this guidance exists to catch.

## A worked example

Take the Job of bringing an external control framework into a corpus to map against.

- **Pain (primary here):** the persona needs the imported catalog to be trustworthy, its provenance recorded and its version pinned, or they cannot rely on what they map against. The motivation is avoidance: an untrustworthy or silently drifting copy.
- **Gain (distinct, so it earns its place):** the persona wants to stand the framework up *faster*, for instance through automated import rather than hand transcription. The motivation is attainment: speed, a different outcome from trust.

Both are kept because trust and speed are not the same outcome.
Had the Gain instead read "the catalog is trustworthy and does not drift," it would have been the Pain in positive voice, and the right move would have been to drop it and let the Pain stand alone.

## The same holds for Relievers and Creators

On the offering side the discipline is identical, and the agentive split makes it easier to see.
A Pain Reliever names what the product offers to *remove a negative*; a Gain Creator names what it offers to *produce a positive*.
A Reliever that relieves the drifting-spreadsheet Pain ("the mapping is authored beside the obligation, so it cannot drift") and a Creator that creates the speed Gain ("the framework is stood up by automated import") are genuinely different and both belong.
A Creator that says only "the mapping no longer drifts" is the Reliever restated, and earns nothing.

## When in doubt, prefer one

Earned Substance tilts the call toward the single facet: a near-identical pain-and-gain or reliever-and-creator pair is evidence of one facet written twice, not of thorough coverage.
Author the motivation that is real, name the distinct counterpart only when it is genuinely distinct, and let the rest stand as one.

## Pinning a facet to a Job with `framedBy`

A [Pain](../loom/note/terms/artifact-kinds/pain.md){id=note:term:hb74nmn} or [Gain](../loom/note/terms/artifact-kinds/gain.md){id=note:term:7e4f92v} may carry an optional `framedBy` relation pointing to the specific [Job](../loom/note/terms/artifact-kinds/job.md){id=note:term:41qzg6f} it is felt against, within its own Need.
The relation is authored on the facet (the dependent end); its inverse `frames`, readable from the Job, is derived and never authored.
The binding source is [Pains and gains framed by their job](../loom/note/decisions/pains-and-gains-framed-by-job.md){id=note:dec:tyf5xxw}.

**When to add it.**
Add `framedBy` when a Need has more than one Job and a given Pain or Gain is felt specifically while doing one of them.
In the control-framework example: the Need has at least two distinct Jobs, importing the catalog and mapping obligations against it.
The Pain about provenance and version trust is felt against the import Job; the Gain about faster setup is also felt at import time.
If there were a separate Pain about mapping obligations to the wrong control, that would sit against the mapping Job, not the import one.
Pinning each facet with `framedBy` makes the cluster machine-readable: a tool (or a reviewer) can tell at a glance which Jobs carry Pains and which carry Gains, and an agent loading context for one Job can load only the facets that frame it.

**When to omit it.**
Omit `framedBy` when the facet spans the whole Need rather than one Job, or when the Need has only one Job (the framing is unambiguous and adding the edge carries no load).
Absence carries no completeness claim: a bare absence reads as "spans the Need, or not classified," not as "no Job owns this facet."

**Repeatable.**
A facet genuinely felt against more than one Job may carry one `framedBy` edge per Job.
The relation is zero-or-more; the optionality is load-bearing and cannot be made required without forcing whole-Need facets to name a Job they are not felt against.

The line form, in the facet's `## Relations` section, is:

```
- framedBy: [Job name](relative/path-to-job.md){id=note:job:…}
```

## Normative sources

The orientation here restates what these fix:

- [Earned Substance](../loom/note/principles/earned-substance.md){id=note:principle:yecemfe}: a facet that carries no distinct load has not earned its place.
- The inclusion tests of [Pain](../loom/note/terms/artifact-kinds/pain.md){id=note:term:hb74nmn}, [Gain](../loom/note/terms/artifact-kinds/gain.md){id=note:term:7e4f92v}, [Pain Reliever](../loom/note/terms/artifact-kinds/pain-reliever.md){id=note:term:7qrdxnp}, and [Gain Creator](../loom/note/terms/artifact-kinds/gain-creator.md){id=note:term:g9fxrs5}: a facet must name its own outcome, not the opposite of another's.
- [Pains and gains framed by their job](../loom/note/decisions/pains-and-gains-framed-by-job.md){id=note:dec:tyf5xxw}: the decision that introduces `framedBy` as an optional, repeatable relation from a Pain or Gain to the Job it is felt against.
