---
id: note:need:pv8k2w9
name: Load only the intent a task needs
kind: need
persona:
  - "[AI Agent](../personas/ai-agent.md){id=note:persona:sk3pzm2}"
  - "[Systems Engineer](../personas/systems-engineer.md){id=note:persona:25fdjrx}"
  - "[Reviewer or Auditor](../personas/reviewer-auditor.md){id=note:persona:9jz2a3w}"
  - "[Organization or Platform Owner](../personas/organization-owner.md){id=note:persona:6ek4j8b}"
status: current
validation: observed
---

When an AI Agent or a Systems Engineer sets out on a task, it wants to load only the intent relevant to that task rather than the whole corpus, so that it acts on precise, current context instead of drowning in unrelated or stale text; the pressure is sharpest for an AI Agent working in a bounded context window, while a Reviewer or Auditor needs to reconstruct afterward exactly what the actor was given, and an Organization or Platform Owner needs that record to be governed and the cost of every task to stay bounded across a fleet.

## Source

The empirically robust degradation of an AI model's attention as its context grows: recall drops in the middle of a long context, recent inputs dominate, instruction adherence drifts, and the model defaults to its pre-training priors, documented across providers and model families.

That a smaller, relevant context mitigates this and lowers cost and latency is reasoned from that established failure mode and seen in this corpus's own use.

External to this corpus and not derived from it.
