---
id: note:pain:f4w2k7m
name: Reconstruction Mistaken for Confirmed Intent
kind: pain
persona:
  - "[Future Maintainer](../../personas/future-maintainer.md){id=note:persona:k04ezkv}"
  - "[Reviewer or Auditor](../../personas/reviewer-auditor.md){id=note:persona:9jz2a3w}"
subkind: risk
status: current
---

When a recovered record carries no signal that its intent was reconstructed after the fact rather than confirmed when the decision was made, a reader cannot tell a best guess from a settled decision, and so treats reconstruction as confirmed and acts on false certainty.

## Illustrative situations

- A Future Maintainer builds on a reconstructed entry as if it were authored, and discovers the mismatch only when something breaks.
- A Reviewer or Auditor, unable to weight a best guess differently from a settled decision, also cannot tell a genuine gap from low-confidence intent still awaiting validation.

## Relations

- partOf: [Adopt the method on a system that already exists](../brownfield-adoption.md){id=note:need:b3k9w2t}
- framedBy: [Locate Settled Versus Provisional Intent](job-locate-settled-versus-provisional-intent.md){id=note:job:h7m4q1c}
