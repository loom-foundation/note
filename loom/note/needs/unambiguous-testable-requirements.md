---
id: note:need:e4k9w2n
name: Unambiguous, testable requirements
kind: need
persona:
  - "[Systems Engineer](../personas/systems-engineer.md){id=note:persona:25fdjrx}"
  - "[Reviewer or Auditor](../personas/reviewer-auditor.md){id=note:persona:9jz2a3w}"
  - "[AI Agent](../personas/ai-agent.md){id=note:persona:sk3pzm2}"
  - "[Verifier](../personas/verifier.md){id=note:persona:vk7m3qp}"
  - "[Implementer](../personas/implementer.md){id=note:persona:s4v9hn2}"
status: current
validation: observed
---

When a requirement is written, the people and agents who read, implement, or verify it want its obligation to be unambiguous and testable, so that what must be true is read the same way by everyone and can actually be checked, rather than being interpreted differently or proving impossible to verify.

## Source

The long-documented defects of natural-language requirements (ambiguity, vagueness, untestability) and the established practice of constrained requirement syntaxes and quality indicators that exist to remove them, in ISO/IEC/IEEE 29148, the INCOSE Guide for Writing Requirements, and the Easy Approach to Requirements Syntax.

The need is sharpened by autonomous agents, which act on exactly what is written and cannot resolve an ambiguity a human reader might.

External to this corpus and not derived from it.

This need is distinct from [Definable acceptance](definable-acceptance.md){id=note:need:fkbs761}, which concerns the acceptance criterion as a standalone artifact authored before build; this need concerns the requirement's own phrasing being unambiguous and carrying a testable condition.
