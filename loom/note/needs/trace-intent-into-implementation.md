---
id: note:need:jxhnj01
name: Trace intent into the implementation that realizes it
kind: need
persona:
  - "[AI Agent](../personas/ai-agent.md){id=note:persona:sk3pzm2}"
  - "[Reviewer or Auditor](../personas/reviewer-auditor.md){id=note:persona:9jz2a3w}"
  - "[Implementer](../personas/implementer.md){id=note:persona:s4v9hn2}"
status: current
validation: inferred
---

When an Implementer or an AI Agent changes a unit of implementation, an implementation artifact such as a module of source code, or a Reviewer or Auditor reviews one, they want to know which intent that unit claims to realize and to be warned when the relied-on intent has moved, so that the change is made with the governing obligations in view and the unit's reliance does not drift out of sight.

## Source

The recurring loss of the link from a specification to the implementation realizing it, and the silent divergence that follows once that link lives only in memory or in informal comment, long observed across software, hardware, and process work.

This need is reasoned from that observed phenomenon and from this corpus's own use rather than measured against a studied population, so its validation is inferred.

External to this corpus and not derived from it.

This need is distinct from [Trust and drift visibility](trust-intent-is-honored.md){id=note:need:46tkxcn}, which concerns confirming after the build that behavior honors the intent; this need concerns finding the governing intent before changing a unit.
