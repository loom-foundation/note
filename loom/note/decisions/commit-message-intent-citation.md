---
id: note:dec:hf8k2wd
name: Commit-message intent citation
kind: decision
status: current
decided: 2026-06-12T00:00:00Z
---

A citation from a Git commit lives in a trailer at the foot of the message, the `Signed-off-by:`-style block a commit already reserves for machine-readable metadata, behind a Title-Case key followed by the bare durable id; the id never appears in the subject or the prose.
The durable id is the only load-bearing part: a checker resolves the id and holds it to staleness, and nothing else in the citation is checked.
The trailer keys are an expected, never-checked convention, and the imperative state-change family is excluded: a citation states a relationship, it never transitions an obligation's state.

## Context

A file outside the corpus cites the intent it enacts by a durable id behind a marker in a comment ([In-code intent citation](in-code-intent-citation.md){id=note:dec:nfaeyk9}).
A commit is the same kind of setting with respect to the corpus boundary: the relative path of the reference-link form is meaningless across that boundary and cannot self-heal there, and the message is read as plain text, not through a Markdown viewer, so the link machinery buys nothing.
What carries across the boundary is the durable identifier ([Stable, location-independent identity](../requirements/system/stable-identity.md){id=note:req:sfmkwmm}, which names a commit message among the places a reference travels).

A commit differs from a source comment in one respect that shapes the form: it has an established convention for machine-readable metadata, the trailer block at the foot of the message, as `Signed-off-by:` and `Co-authored-by:` use it.
A citation placed there is recognizable to a checker by its key without parsing prose, and recognizable to a reader as metadata rather than narrative.
Keeping the id out of the subject and the body keeps the prose free to describe the change in human terms while the trailer carries the resolvable handle.

The setting also differs from the corpus in what a verb key can mean.
Inside the corpus, `satisfies`, `verifies`, and `enacts` are typed relations with a defined source kind and a defined target kind, authored once and checked.
A commit has no source kind: it is a change in history, not an artifact of a kind the verb relates.
So a trailer key is a homonym of the corpus verb, not the same typed relation, and three things follow that make checking it ill-founded.
Endpoint validation is ill-defined, because there is no typed source endpoint to validate the relation against.
A commit is immutable, so a citation made under one verb vocabulary cannot be re-typed when the vocabulary churns: a checked key would rot the moment a verb is renamed, with no way to amend the record in place.
And an agent under completion pressure over-claims, so a key the tool trusts becomes a claim nothing backs.

## Decision

- **A commit cites an artifact by its durable identifier**, carried in a trailer at the foot of the message, behind a Title-Case key; the id appears only in the trailer, never in the subject or the prose.

- **The durable id is the only load-bearing part.**
  A checker resolves the id and holds it to staleness, and relies on nothing else in the citation.

- **The trailer keys are an expected, never-checked convention.**
  The keys are `Satisfies:`, `Verifies:`, and `Enacts:`, with `Refs:` the neutral fallback that claims only reference.
  They are expected by convention so a reader sees the relationship at a glance, but a checker never blocks on a key and never treats it as load-bearing, because a commit has no source kind: the keys are homonyms of the corpus verbs rather than the same typed relations, endpoint validation against a commit is ill-defined, and an immutable commit would rot under verb churn if its key were checked.
  A tool may raise an advisory, non-blocking plausibility warning only, an unknown key, or a key whose target kind is implausible, and surface it without holding the citation to it.

- **A commit may cite more than one artifact.**
  Where one change stands to more than one piece of intent, each citation is its own trailer carrying one id, so the set is read as repeated trailers rather than a packed list.

- **Default to `Refs:` unless the structural claim is verifiable.**
  An agent under completion pressure over-claims, and a false `Satisfies:` poisons the derived trace views auditors trust, where a neutral `Refs:` claims nothing.
  So an agent writes `Refs:` unless it can stand behind the stronger key, a verification that exists and passes, a requirement the change demonstrably meets, and reaches for `Satisfies:`, `Verifies:`, or `Enacts:` only then.

- **The imperative state-change family is excluded.**
  Keys such as `Closes`, `Fixes`, and `Resolves` are not citation keys: a citation states a relationship, it never transitions an obligation's state.
  Whether an obligation is met is a verdict the Orchestrating Authority owns, established by a Verification, not asserted by a word in a commit trailer.

- **Committed trailers carry canonical tokens only.**
  The keys are spelled canonically in committed history; the citation as it lands uses the fixed forms, not an author's variant.

## Forces and trade-offs

- The handle alone is what survives the boundary, so holding only the id load-bearing keeps the citation honest: the one checked part resolves and is checkable, and nothing in it can rot into a silent lie.
- Reusing the existing trailer convention rather than inventing a placement means the citation sits where readers and tooling already look for machine-readable commit metadata, so it earns no new structure ([Earned Substance](../principles/earned-substance.md){id=note:principle:yecemfe}; [Proportionality](../principles/proportionality.md){id=note:principle:es0vhzn}).
- A commit is immutable once made: the citation cannot drift away from the change it describes by a later careless edit, which is the property that makes it the auditor's evidence.
  The mirror-image cost is that a citation made in error is corrected only by a later commit, never in place, the same constraint history imposes on every commit message; this is also why a checked verb key would rot, and why the keys are convention rather than checked relations.
- A false stronger key would silently corrupt the derived trace view an auditor reads, so the `Refs:`-by-default rule trades a slightly weaker default claim for a trace surface that never lies: the neutral fallback is always honest, and a stronger key is a deliberate, verifiable act.
- Excluding the state-change family keeps the boundary clean: Note represents the relationship a commit asserts and computes over it, and leaves the verdict of whether an obligation is met to the authority that owns it and the Verification that establishes it.

## Alternatives considered

- **A free-text mention of the artifact in the commit subject or body.**
  Rejected: a mention in prose is not recognizable to a checker without parsing natural language, and an id buried in a sentence is not reliably resolvable.
  The trailer makes the citation findable by key and the id resolvable, which a free-text mention does not.
- **The full reference-link form `[name](path){id=note:kind:opaque}`, as corpus prose uses.**
  Rejected, for the same reason it is rejected for code: the relative path is meaningless across the corpus boundary and cannot self-heal there, and the rendered-link rationale does not apply to a commit message read as plain text.
- **The in-code middle form: the id followed by a parenthetical name label, expected and never checked.**
  Rejected: a commit is immutable, so a label frozen into history cannot be refreshed when the artifact is renamed; a reader following an old trailer meets a name the corpus no longer uses, and no tool pass can correct the record in place.
  A source comment differs exactly here: a file is amendable, so its label refreshes with the corpus, while a trailer's cannot, which leaves the bare id as the only part of a commit citation that never lies.
- **Make the trailer key a checked, load-bearing relation, as the corpus verbs are.**
  Rejected: a commit has no typed source kind for the verb to relate, so endpoint validation is ill-defined; and an immutable commit cannot be re-typed when the verb vocabulary churns, so a checked key rots the moment a verb is renamed.
  The key is therefore a never-checked convention, advisory at most.
- **Admit the imperative state-change keys (`Closes`, `Fixes`, `Resolves`).**
  Rejected: these transition an obligation's state, and a citation never transitions state.
  Whether an obligation is met is a verdict the Orchestrating Authority owns, established by a Verification; a commit trailer asserting it would let an agent close an obligation by writing a word, which is exactly the authority boundary Note does not cross.
- **Defining nothing, leaving commit-message citation to ad hoc convention.**
  Rejected: it leaves the auditor's authoritative record uncitable and the commit's reliance undetectable, which is the need this rests on.

## Driven by

- groundedIn: [Commit-message citation of intent](../requirements/system/commit-message-citation-of-intent.md){id=note:req:cm7vq3x}
- groundedIn: [In-code intent citation](in-code-intent-citation.md){id=note:dec:nfaeyk9}
- groundedIn: [Compute and Report](../principles/compute-and-report.md){id=note:principle:6e7f28k}
