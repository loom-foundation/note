# Right-sizing artifacts

How to author no more artifact than the work earns, especially when the author is an AI agent filling a template at machine speed.
This is orientation and applied guidance, not normative text; the binding commitments live in [Earned Substance](../loom/note/principles/earned-substance.md){id=note:principle:yecemfe} and [Proportionality](../loom/note/principles/proportionality.md){id=note:principle:es0vhzn}, the decision threshold in the [Decision Record](../loom/note/terms/artifact-kinds/decision-record.md){id=note:term:met4a44} term, and the authoring on-ramps in [The acceptance-criterion kind](../loom/note/decisions/acceptance-criterion-kind.md){id=note:dec:sxv0tq9} and [Atomic facets](../loom/note/decisions/atomic-facets.md){id=note:dec:af3k9w2}.

## The trap: a template filled is not a task served

An agent asked to produce an artifact will fill the whole template, whatever the task deserves.
A one-line bug fix becomes a faceted need, an offering, and a decision record; a trivial, reversible choice becomes six sections of weighed alternatives.
The cost is not only the tokens: over-produced ceremony teaches readers to discount the corpus, which is the trust debt Earned Substance names, and it buries the artifacts that do carry load among the ones that do not.

The rules that prevent it are already in the method; this doc compiles them into authoring moves.

## Before minting anything

Ask, in order:

1. **Does an existing artifact already carry this intent?**
   Amend it; do not mint a near-duplicate sibling for it to drift against.
2. **Is this intent at all?**
   Work-planning content, what to do next and in what order, is not the note layer's concern; it belongs to the deferred plan layer or to the team's tracker.
3. **What is the smallest form that captures it?**
   The conformance floor is the envelope plus a lead.
   A section is added when it carries load the lead does not, never to complete a shape.

## The decision threshold

At `standard` and above, a design choice that shaped the corpus earns a decision record.
Not every choice is such a choice.
The litmus, from the [Decision Record](../loom/note/terms/artifact-kinds/decision-record.md){id=note:term:met4a44} term: were real alternatives weighed, would a future reader plausibly re-litigate or silently undo it, and does it bind work beyond the change that carries it?

When the answer is no, the record is the commit: describe the why in the commit message and cite the touched artifacts by id in trailers ([Commit-message intent citation](../loom/note/decisions/commit-message-intent-citation.md){id=note:dec:hf8k2wd}).
A fix, a rename, a reversible detail, or a call no one would contest is commit-message material, not a decision artifact.
The corpus stays legible exactly because a decision record still means something when one appears.

## Use the on-ramps

The method blesses lightweight starting forms precisely so a first draft need not mint everything:

- An acceptance criterion starts as a `## Acceptance criteria` section on its requirement; it earns its own file only when it is traced to, referenced, or verified.
- A need's facets may start bundled in the need and be promoted to files when they earn identity.
- A pain and a gain on the same job are both kept only where they name genuinely different outcomes; when in doubt, prefer one ([authoring-pains-and-gains.md](authoring-pains-and-gains.md)).

## Agent rules of thumb

- Default to the floor; earn each section.
- Prefer amending a `current` artifact over minting a sibling; prefer one artifact revised over two artifacts reconciled.
- Never mint a decision record to narrate a fix; cite, in the commit, the intent the fix serves, with `Refs:` as the default key.
- State honestly what was not validated: an inflated `validation` tier, or an over-claimed citation key, is worse than a modest one.
- Where a required section has nothing load-bearing to say, say why in one line rather than filling it; where the profile does not require it, omit it.

## Normative sources

The orientation here restates what these fix:

- [Earned Substance](../loom/note/principles/earned-substance.md){id=note:principle:yecemfe}: the bar for adding is higher than the bar for not adding.
- [Proportionality](../loom/note/principles/proportionality.md){id=note:principle:es0vhzn}: rigor matches stakes; ceremony matches consequence.
- [Decision Record](../loom/note/terms/artifact-kinds/decision-record.md){id=note:term:met4a44}: the inclusion test, including the weight threshold.
- [The acceptance-criterion kind](../loom/note/decisions/acceptance-criterion-kind.md){id=note:dec:sxv0tq9} and [Atomic facets](../loom/note/decisions/atomic-facets.md){id=note:dec:af3k9w2}: the section-before-file on-ramps.
- [Commit-message intent citation](../loom/note/decisions/commit-message-intent-citation.md){id=note:dec:hf8k2wd}: the commit as the record for choices below the decision threshold.
