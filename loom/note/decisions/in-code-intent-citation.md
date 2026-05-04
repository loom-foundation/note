---
id: note:dec:nfaeyk9
name: In-code intent citation
kind: decision
status: current
decided: 2026-06-12T00:00:00Z
---

A file outside the corpus, a module of source code or another implementation artifact, cites the intent it enacts by carrying that artifact's durable identifier in a comment, in a shape a checker can recognize: the fixed marker `@intent`, a recommended verb-key label, then the bare id.
The durable id is the only load-bearing part: a checker resolves the id and holds it to staleness, and nothing else in the citation is checked.
The label form is recommended by convention, expected but never enforced, and a tool may raise advisory, non-blocking plausibility warnings about it.

## Context

A corpus artifact cites another artifact with the reference-link form `[name](path){id=note:kind:opaque}`: a self-healing relative path for navigation, a human-readable name that renders in a Markdown viewer, and the durable id a tool resolves and checks.

A file outside the corpus is a different setting.
The relative path is meaningless across the corpus boundary and cannot self-heal there, because the file is not part of the corpus a tool reorganizes.
The rendered-link rationale does not apply either: a source comment is read as text, not through a Markdown viewer, so the link machinery buys nothing.
What remains useful across the boundary is the one part designed to survive relocation: the durable identifier ([Stable, location-independent identity](../requirements/system/stable-identity.md){id=note:req:sfmkwmm}).

That leaves an open question about the human-readable part of the citation.
In corpus prose the link text carries the meaning an opaque id alone lacks, and it stays current because a tool refreshes it from the target's name.
In a comment there is nothing to refresh against, so any text copied beside the id is a second copy of the artifact's name with nothing to keep it current: it rots silently, the precise failure the durable handle exists to avoid.
The reader who meets the code cold with no resolver wired up is exactly the reader a human-readable label most serves, yet that reader is also the one a stale label most misleads.

A second question is what the label, when present, should say.
A citation often wants to name not just which intent governs the unit but how the unit stands to it: that it satisfies a requirement, that a verification confirms it, that it enacts a convention, or merely that it refers to a piece of intent for context.
Naming that relationship in the label gives a cold reader a richer reading at a glance, but it also invites a structural claim the comment cannot back: a comment is not a typed corpus edge, and a `Satisfies:` written under completion pressure asserts a relationship nothing has checked.

## Decision

- **A file outside the corpus cites an artifact by its durable identifier**, carried in a comment in the host language, behind the fixed marker `@intent` that lets a checker find the citation without parsing the host language and lets a reader see it for what it is.
  The marker spelling is fixed: `@intent`.

- **The durable id is the only load-bearing part.**
  A checker resolves the id and holds it to staleness, and relies on nothing else in the citation.

- **A verb-key label is the recommended form.**
  Alongside the id the form expects, by convention, a Title-Case verb key that names how the unit stands to the cited intent: `Satisfies:` for a requirement the unit meets, `Verifies:` for an acceptance criterion or convention a check confirms, `Enacts:` for a convention or requirement the unit puts into effect, and `Refs:` as the neutral fallback that claims only reference.
  The label is recommended, not merely tolerated, because the reader who most needs it is the one reading the code cold without a resolver; but it carries exactly the standing the human name already had, expected by convention and never authoritative.

- **The label is never checked.**
  A checker never blocks on the verb key or its target and never treats either as load-bearing, because in a comment there is nothing to refresh the label against.
  A tool may raise an advisory, non-blocking plausibility warning, an unknown verb key, or a key whose target kind is implausible (a `Satisfies:` aimed at a need rather than a requirement), and surface it the way it surfaces any drifted comment, without holding the citation to it.

- **Default to `Refs:` unless the structural claim is verifiable.**
  An agent that cannot confirm the stronger relationship by inspection, a verification that exists and passes, a requirement the unit demonstrably meets, writes `Refs:`, which claims only reference and overstates nothing.
  A stronger key is written only when the structural claim it makes can be stood behind.

- **Committed comments carry canonical tokens only.**
  The verb keys and the marker are spelled canonically in committed code; the citation as it lands in history uses the fixed forms, not an author's variant.

## Forces and trade-offs

- The handle alone is what survives the boundary, so holding only the id load-bearing keeps the citation honest: the one checked part resolves and is checkable, and nothing in it can rot into a silent lie.
- Recommending the verb-key label, rather than leaving the label bare or omitting it, gives the cold reader both a name and a reading of the relationship, at the cost of a label that can drift; that cost is bounded because the label is never authoritative and a drifted label is no worse than any stale comment, which a tool may flag without blocking.
- Letting the label name a relationship the comment cannot prove invites over-claiming, which the `Refs:`-by-default rule contains: the neutral fallback is always available and always honest, and a stronger key is a deliberate act backed by a verifiable claim, not a reflex under completion pressure.
- Carrying the id in a host-language comment means the marker, not a Markdown structure, makes the citation recognizable; a checker reads comments as text and keys on the marker, a lighter recognizer than parsing each host language.

## Alternatives considered

- **The full reference-link form `[name](path){id=note:kind:opaque}`, as corpus prose uses.**
  Rejected for code: the relative path is meaningless across the corpus boundary and cannot self-heal there, and the rendered-link rationale, that a Markdown viewer shows a navigable link, does not apply to a source comment read as plain text.
  Carrying the path and link syntax into code imports weight that buys nothing and a path that rots immediately.
- **A bespoke structured annotation, an `@intent{...}` style schema with named fields.**
  Rejected: a marked comment carrying the id already gives a checker a recognizable, resolvable citation, so a new grammar adds parsing surface and a thing to learn without earning its weight ([Earned Substance](../principles/earned-substance.md){id=note:principle:yecemfe}; [Proportionality](../principles/proportionality.md){id=note:principle:es0vhzn}).
- **Make the verb key a checked, load-bearing part of the citation.**
  Rejected: a verb key embedded in a comment is a typed claim with nothing to keep it true, so checking it, or blocking on it, manufactures the very drift the durable handle avoids and asserts a typed edge the comment is not.
  The key is instead expected by convention and only ever advisory, so the id stays the one load-bearing, drift-proof part.
- **A bare id with no label, ever.**
  Rejected on ergonomics: the reader who meets code cold with no resolver, the one [Stable, location-independent identity](../requirements/system/stable-identity.md){id=note:req:sfmkwmm} most exists to serve, sees only an opaque token.
  Recommending a label costs the author a few words and is recoverable if it drifts, where a bare id costs every tool-less reader a lookup.
- **Defining nothing, leaving in-code citation to ad hoc convention.**
  Rejected: it leaves implementations uncitable and their reliance undetectable, which is the need this rests on.
- **The marker `@note`.**
  Rejected: it collides with the established Doxygen `@note` command and the informal note-to-self comment habit, so a checker grepping for it produces false positives across real codebases, and a cold reader parses it as a remark rather than a citation; `@intent` says what is cited and has no established doc-tool meaning.

## Driven by

- groundedIn: [Trace intent into the implementation that realizes it](../needs/trace-intent-into-implementation.md){id=note:need:jxhnj01}
- groundedIn: [In-code citation of intent](../requirements/system/in-code-citation-of-intent.md){id=note:req:cffvvdz}
- groundedIn: [Compute and Report](../principles/compute-and-report.md){id=note:principle:6e7f28k}

## Worked example

A payments team enacts the requirement `acme:req:7p2k9wd` ("refunds are idempotent") in a module of source code.
The citation sits at the granularity the obligation lands on: on the type for a file-wide obligation, on the load-bearing block for a local one, with more than one id where more than one obligation applies.

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

The id `acme:req:7p2k9wd` is the only part a checker resolves and holds to staleness.
The verb key reads the relationship for a maintainer with no tool at hand: the type-level `Enacts:` names the requirement the module puts into effect, while the local guard uses the neutral `Refs:` because no verification stands behind a stronger claim there.
A checker may note, without blocking, that a key is unknown or that its target kind is implausible, but it holds the citation to none of that.
When the requirement's text is revised, every file carrying the id is surfaced for re-check, so the implementation's reliance does not drift out of sight.
`@intent` is the fixed marker the grammar fixes.
