---
id: note:pain:j6gvm9m
name: Acting On Unverifiable Provenance
kind: pain
persona:
  - "[AI Agent](../../personas/ai-agent.md){id=note:persona:sk3pzm2}"
status: current
validation: observed
subkind: obstacle
---

An AI Agent has no way to know whether the context it is acting on is complete, current, or has been silently altered, so it proceeds on instructions whose provenance it cannot verify and can be steered by a poisoned chunk it cannot trace.

## Relations

- partOf: [Load only the intent a task needs](../load-only-relevant-intent.md){id=note:need:pv8k2w9}
- framedBy: [Load Exactly the Intent a Task Needs](job-retrieve-relevant-intent.md){id=note:job:p6nab75}
- framedBy: [Keep Context Current](job-keep-context-current.md){id=note:job:m080ftx}
