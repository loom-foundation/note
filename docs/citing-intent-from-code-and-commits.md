# Citing intent from code and commits

How a unit of implementation, and the commit that ships it, names the intent it enacts by a durable id, so an auditor can trace a shipped change back to the obligation that prompted it.
This is orientation and applied guidance, not normative text; the binding forms live in [In-code intent citation](../loom/note/decisions/in-code-intent-citation.md){id=note:dec:nfaeyk9} and [Commit-message intent citation](../loom/note/decisions/commit-message-intent-citation.md){id=note:dec:hf8k2wd}.

## What this is and why

An artifact states an obligation; some unit of code enacts it; some commit ships that code.
Citing intent is how the code and the commit name, resolvably, which artifact they answer to.
The point is traceability: when a requirement's text is later revised, every file and every change that cited it can be surfaced for re-check, so an implementation's reliance on an obligation does not quietly drift out of sight.

The citation carries one load-bearing thing: the artifact's durable id (for example `acme:req:7p2k9wd`).
The id is the only part a checker resolves and holds to staleness.
Everything else in the citation is for the human: a key that names the kind of relationship, and (in code) a short human-readable label.
Neither the key nor the label is authoritative, and a tool never blocks on them.

## Where the citation goes

There are two placements, and they answer different questions.

The in-code comment says what governs this unit of implementation now.
It travels with the code and is read where the code is read, by a maintainer who is already looking at the thing the cited intent governs.

The commit trailer says which change enacted which intent.
It travels with the change in history and is read by an auditor reconstructing how the work came to honor its intent.
The commit is the authoritative record precisely because it is immutable and signable, where a comment can be edited away from the change it once described.

In both placements the id never needs to appear in the commit subject, in prose, or in a sentence a reader has to parse.
A reference buried in prose is not reliably findable by a checker and not reliably resolvable.
The subject and body describe the change in words; the citation's job is only to name which intent, by id, in a place tooling already looks.

## The key vocabulary

A citation key names the kind of relationship between the change and the artifact.
The id is what gets resolved; the key tells a human (and a relationship-aware view) why the change points there.
Keys are an expected, never-checked convention drawn from a small set, each corresponding to one of Note's own typed relations.

| Key | Meaning | Typically points at | Example trailer line |
| --- | --- | --- | --- |
| `Satisfies:` | This change implements the obligation stated in the target. | a requirement | `Satisfies: acme:req:7p2k9wd` |
| `Verifies:` | This change is the check that confirms the target holds. | a requirement, specification, convention, or acceptance-criterion | `Verifies: acme:req:7p2k9wd` |
| `Enacts:` | This change puts the target's agreed rule into effect. | a convention or requirement | `Enacts: acme:conv:3m8x2qd` |
| `Refs:` | This change relates to the target without one of the stronger roles above. | any artifact | `Refs: acme:dec:hf8k2wd` |

The keys are Title-Case in committed code and commit trailers.
A tool may raise an advisory, non-blocking plausibility warning when a key is unknown or its target kind is implausible (for example, a `Satisfies:` aimed at a need rather than a requirement), but it never blocks on the key and never treats it as load-bearing.

**Agent default: `Refs:` unless the structural claim is verifiable.**
An agent that cannot confirm the stronger relationship by inspection writes `Refs:`, which claims only reference and overstates nothing.
A stronger key is written only when the structural claim it makes can be stood behind: a verification that exists and passes, a requirement the unit demonstrably meets, a convention the unit directly implements.

**Canonical tokens only.**
Committed files, code comments, and commit trailers carry canonical tokens only.
The manifest `vocabulary` map is display and input normalization; it is never an authoring vocabulary, and a variant spelling does not belong in committed history.

## What these keys do NOT do

These keys are citation keys: they assert a traceable relationship between a change and an artifact, and nothing more.
They do not transition an artifact's state, and they never will.

The imperative state-change family (`Closes`, `Fixes`, `Resolves`) is excluded.
Those keywords perform an action: GitHub and GitLab read them on merge to close a referenced issue; Jira Smart Commits read them and move an issue through its workflow; Azure Boards reads them and transitions a work item to "done."
A Note citation key does none of that.

A `Satisfies:` trailer asserts that this change implements an obligation; it does not mark the requirement done, closed, accepted, or verified.
Whether an obligation is discharged, and who is permitted to say so, is a lifecycle authorization decision that belongs to the Orchestrating Authority, never to a word in a commit message.

Use these keys to record relationships for traceability, and expect them to do exactly that: make the link findable and resolvable, surface a citation for re-check when its target changes, and otherwise leave every artifact's status untouched.

## Worked commit-message examples

A single citation, the common case:

```
Add replay guard to refund path

A second call with a seen idempotency key now returns the stored
outcome instead of issuing a duplicate refund.

Satisfies: acme:req:7p2k9wd
```

More than one citation, where one change discharges more than one obligation.
Each citation is its own trailer carrying one id; the set reads as repeated trailers, never a packed list:

```
Harden refund idempotency and add its contract test

Satisfies: acme:req:7p2k9wd
Verifies: acme:req:7p2k9wd
Refs: acme:dec:hf8k2wd
```

Alongside the trailers a commit already carries, in the same block at the foot of the message:

```
Rotate payment keys on the ninety-day PCI schedule

Satisfies: acme:req:0a4r1ke

Reviewed-by: Dana Okafor <dana@acme.example>
Signed-off-by: Sam Rivera <sam@acme.example>
```

The citation trailers sit with `Signed-off-by:`, `Reviewed-by:`, and the like, because that block is where a reader and a tool already look for machine-readable commit metadata.
Order among them does not matter to a checker; it resolves each citation by the id alone.

## The in-code comment form

In code, the citation is a marked comment in the host language.
A fixed marker precedes the citation so a checker can find it without parsing the host language, and a reader can see it for what it is.
The convention pairs the key and id with a short human-readable label in parentheses, so a maintainer reading the code cold, with no resolver wired up, still sees what the citation governs.
The label is never checked against the artifact's name and is never load-bearing; a tool may note when it has drifted, but never blocks on it.

```go
// RefundService issues refunds against prior captures.
//
// @intent Enacts: acme:req:7p2k9wd (refunds are idempotent)
type RefundService struct{ /* ... */ }

func (s *RefundService) Refund(ctx context.Context, r RefundRequest) (*Refund, error) {
	// Replay guard: a second call with a seen key returns the stored outcome.
	// @intent Refs: acme:req:7p2k9wd (the guard that makes the operation idempotent)
	if prior, ok := s.seen(r.IdempotencyKey); ok {
		return prior, nil
	}
	// ...
}
```

The citation sits at the granularity the obligation lands on: on the type for a file-wide obligation, on the load-bearing block for a local one, with more than one id where more than one obligation applies.
`@intent` is the fixed marker the grammar fixes.
