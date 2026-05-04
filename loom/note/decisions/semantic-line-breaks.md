---
id: note:dec:sw4k9n2
name: Semantic line breaks in artifact prose
kind: decision
status: current
decided: 2026-06-10T05:50:41Z
---

Prose in artifacts is wrapped with semantic line breaks: one sentence per source line, and a very long sentence may break at a major clause boundary.
The corpus does not hard-wrap prose to a fixed column, nor keep a whole paragraph on one long line.

A passage that makes several distinct points is split into one short paragraph per point.

Frontmatter, tables, code blocks, and diagrams are never reflowed.

## Context

How Markdown source is wrapped has no effect on the rendered output.
In a rendered Markdown file a single newline inside a paragraph is treated as a space, so every wrapping style renders identically; the choice is entirely about the source text, which is what the corpus versions, diffs, and reviews.

Three styles were weighed.

A fixed column hard-wraps prose at roughly eighty to a hundred characters, breaking wherever the column falls.

No wrap keeps each paragraph on one long line and lets the editor soft-wrap it for display.

Semantic line breaks put one sentence on each source line.

The corpus is held in git, reviewed through pull requests, rendered on hosts that soft-wrap, and co-authored by humans and AI agents.

## Decision

- Prose wraps at sentence boundaries, one sentence per source line.
  A genuinely long sentence may break at a major clause boundary, a semicolon, a dash, or a leading conjunction, rather than run to an unreadable length.
- A rationale, or any passage that makes several distinct points, is split into one short paragraph per point, separated by a blank line, rather than packed into a single block.
- Frontmatter, tables, code blocks, ASCII diagrams, and mermaid are left exactly as authored; only prose paragraphs are wrapped this way.
- This is a recommended authoring discipline, not a conformance gate.
  A profile may report a line that carries more than one sentence, but an artifact is not invalid for wrapping differently.

## Forces and trade-offs

The deciding force is review.
A one-word edit to a semantically-wrapped paragraph changes exactly one short line, and that line is a complete thought, so the change and its context read cleanly in a diff.

Under a fixed column the same edit cascades a rewrap across several lines whose breaks carry no meaning; under one long line per paragraph the diff is clean at the line level but a reviewer must scan a single very long line.

Clean, meaningful diffs are the corpus's commitment to reviewable change made concrete, for human reviewers and for the agents that co-author it.

An agent that edits by matching text lands a targeted edit cleanly on a short, sentence-scoped line and produces a minimal diff, the same gain a human reviewer gets.

The cost is that no general Markdown formatter enforces one sentence per line, so the discipline rests on the author.
For this corpus that cost is low: authoring follows explicit rules that agents also follow, and the tool can report a line carrying more than one sentence rather than enforce it, which is representation, not enforcement.

## Alternatives considered

A fixed-column hard wrap.
Rejected: its line breaks carry no meaning, a small edit rewraps several lines and muddies the diff, and agents frequently rewrap incorrectly.

No wrap, one long line per paragraph.
Kept as the documented fallback: it is nearly as good on diffs and is the one style a formatter can enforce automatically, for example Prettier with prose-wrap set to never, so a tooling-light adopter who would rather not rely on discipline should use it.

## Driven by

- groundedIn: [Proportionality](../principles/proportionality.md){id=note:principle:es0vhzn}
- groundedIn: [Compute and Report](../principles/compute-and-report.md){id=note:principle:6e7f28k}
