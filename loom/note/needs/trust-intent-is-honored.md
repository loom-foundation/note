---
id: note:need:46tkxcn
name: Trust and drift visibility
kind: need
persona:
  - "[Reviewer or Auditor](../personas/reviewer-auditor.md){id=note:persona:9jz2a3w}"
  - "[Verifier](../personas/verifier.md){id=note:persona:vk7m3qp}"
status: current
validation: observed
---

A Reviewer or Auditor, or a Verifier, examining what was built needs to trace any behavior back to the requirement that prompted it and to learn when something the work relied on has changed, so they can trust the system does what was promised and catch divergence before it ships.

## Source

The documented phenomena of intent loss across lossy hand-offs and of silent divergence between specifications and the systems built from them, long observed in software engineering practice.

External to this corpus.

This need is distinct from [Trace intent into the implementation that realizes it](trace-intent-into-implementation.md){id=note:need:jxhnj01}, which concerns finding the governing intent before changing a unit; this need concerns confirming after the build that behavior honors the intent. It is also distinct from [Operate one corpus across many repositories](operate-corpus-across-repositories.md){id=note:need:03gs33j}: both serve a Reviewer or Auditor confirming obligation coverage, but this need does so within a single corpus while that one does so across repository boundaries.
