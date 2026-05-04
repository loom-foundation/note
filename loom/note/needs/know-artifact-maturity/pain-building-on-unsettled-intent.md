---
id: note:pain:66a6e2t
name: Inheriting from Unsettled Intent
kind: pain
subkind: risk
persona:
  - "[Future Maintainer](../../personas/future-maintainer.md){id=note:persona:k04ezkv}"
  - "[AI Agent](../../personas/ai-agent.md){id=note:persona:sk3pzm2}"
status: current
---

A Future Maintainer or AI Agent treats an artifact's content as settled when it is still provisional or has been superseded, so the unsound assumption propagates into downstream work before anyone notices.

## Illustrative situations

- A Future Maintainer extends guidance treating it as authoritative, but it was never finished; the gap surfaces only after the downstream work has to be unwound.
- An AI Agent inherits a half-formed decision as though it were current, embeds it into the artifacts it authors next, and the mistake compounds at machine speed before anyone can intervene.

## Relations

- partOf: [Know an artifact's maturity before relying on it](../know-artifact-maturity.md){id=note:need:6pxykex}
- framedBy: [Calibrate Inheritance Posture from Artifact Status](job-recognize-retired-artifact.md){id=note:job:qrm1jdx}
