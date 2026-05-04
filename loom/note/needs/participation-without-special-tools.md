---
id: note:need:63w7v3e
name: Participation without special tools
kind: need
persona:
  - "[Systems Engineer](../personas/systems-engineer.md){id=note:persona:25fdjrx}"
  - "[AI Agent](../personas/ai-agent.md){id=note:persona:sk3pzm2}"
  - "[Adopter](../personas/adopter.md){id=note:persona:n66rj1d}"
status: current
validation: inferred
---

A Systems Engineer moving between machines, an AI Agent running in a sandbox or a continuous-integration runner, and an Adopter rolling the method out to a team all want to read or write intent at the lowest possible barrier, so taking part is never gated by having the right tool installed.

## Source

That specialized tooling raises the barrier to participation is a general and established property of tooling.

That AI agents in constrained environments (sandboxes, runners, small models) are specifically blocked by tool requirements is inferred from how those environments operate;
it has not yet been measured.

Tier is `inferred` to reflect the weaker, agent-specific half rather than overstate it.

This need is distinct from [Intent that outlives its tooling](intent-outlives-tooling.md){id=note:need:jwvn9b7}, which concerns access when the tool is gone or the corpus is inherited; this need concerns access when the preferred tool is not installed in the current environment. They share the plain, tool-independent format that resolves both.
