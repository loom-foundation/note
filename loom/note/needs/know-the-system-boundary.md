---
id: note:need:c7k2n9w
name: System boundary knowledge
kind: need
persona:
  - "[Systems Engineer](../personas/systems-engineer.md){id=note:persona:25fdjrx}"
  - "[AI Agent](../personas/ai-agent.md){id=note:persona:sk3pzm2}"
  - "[Implementer](../personas/implementer.md){id=note:persona:s4v9hn2}"
  - "[Reviewer or Auditor](../personas/reviewer-auditor.md){id=note:persona:9jz2a3w}"
status: current
validation: observed
---

When a Systems Engineer, an AI Agent, an Implementer, or a Reviewer or Auditor reads or authors intent, they want to know where the system's boundary lies, what sits inside it, what sits outside it, and what crosses it, so that every obligation is read against the right system and nothing is assumed inside or outside the system by accident.

## Source

The long-documented role of an explicit system boundary in avoiding scope ambiguity and misread requirements, established as the context diagram in structured analysis (DeMarco; Gane and Sarson) and in Jackson's Problem Frames, as the system boundary in ISO/IEC/IEEE 29148, and as the system-context view in the C4 model.

The need is sharpened by autonomous agents, which act on what is stated and cannot infer an unstated boundary.

External to this corpus and not derived from it.
