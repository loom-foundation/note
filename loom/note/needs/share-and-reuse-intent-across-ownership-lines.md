---
id: note:need:mqzq97r
name: Share and reuse intent across ownership lines
kind: need
persona:
  - "[Adopter](../personas/adopter.md){id=note:persona:n66rj1d}"
  - "[Reviewer or Auditor](../personas/reviewer-auditor.md){id=note:persona:9jz2a3w}"
status: current
validation: inferred
---

An Adopter that wants to share intent it has authored with a source outside its own line of ownership, or reuse intent published by one, needs to draw that intent in (or offer its own out) and depend on a known version of it.
The source sits outside the Adopter's line of ownership: there is no common ancestor and no inheritance cascade between them, so intent is never inherited; it must be drawn in or offered out across the gap by choice.
If this goes unmet, the Adopter either re-authors what the external source already settled, or pastes it in as an unattributed copy that silently diverges, with no record of which version it took or whether that version still stands.

## Source

The ordinary supply-chain pattern of depending on a published, versioned package owned by someone else (applied to intent rather than code), and the lateral-reuse pattern of peer teams exchanging needs, requirements, or decisions with no shared owner between them.
Both patterns are real and external; the need for intent to be drawn in or offered out at a known version is inferred from them.
Since the method does not yet exist, this has not been observed in practice.

## Illustrative situations

These shaped the need and are kept here in the problem space, not restated in the requirements they motivate; they are inferred from common patterns, not observed by us.

1. Subscribing to a peer's capability package.
   An Adopter subscribes to a shared GDPR-crosswalk capability package published by another organization and draws its needs and requirements into its own corpus, pinned to a stated version, so its work builds on a fixed target it can re-check when the package publishes a new release.

2. Two peer teams sharing laterally.
   Two teams under no common owner each maintain their own corpus; one has authored requirements the other wants to take up.
   With no inheritance line between them, the requirements cannot cascade down: one team offers them out and the other draws them in as a versioned dependency, each recording what it took and from where.

This need is distinct from [Promote intent to a broader scope](promote-intent-to-broader-scope.md){id=note:need:hq7k4w2}, which moves intent up the ownership graph so teams beneath inherit it (a vertical, inside-the-line cascade); here the source is outside the line and nothing is inherited.
It is distinct from [Operate one corpus across many repositories](operate-corpus-across-repositories.md){id=note:need:03gs33j}, which federates repositories that share one owner into a single connected corpus; here the source has a different owner and stays a separate corpus, reached only by an explicit drawn-in dependency.
It is distinct from [Inherited intent on fork](carry-inherited-intent-on-fork.md){id=note:need:29519ms}, which detaches intent from a former parent so a fork stands alone; here there was never a parent to detach from, only a peer to depend on.
And it is distinct from [Trust and drift visibility](trust-intent-is-honored.md){id=note:need:46tkxcn}: both touch change-visibility, but that need watches for drift between intent and the system built inside one corpus, whereas the concern here is drift of an external subscription source: learning when the upstream version an Adopter drew in has moved beneath it.
