---
id: note:pain:caanj9p
name: Flat Directory Loses Relationships
kind: pain
subkind: obstacle
persona:
  - "[Systems Engineer](../../personas/systems-engineer.md){id=note:persona:25fdjrx}"
  - "[AI Agent](../../personas/ai-agent.md){id=note:persona:sk3pzm2}"
status: current
---

When a kind holds many artifacts with no readable grouping, the related ones are indistinguishable from the unrelated ones: a Systems Engineer cannot tell which artifacts form a coherent set without reading all of them, and so risks missing a member or redoing work already done, while an AI Agent must touch every artifact in the kind to recover a related subset, so the cost of working with any one group scales with the total count rather than the size of the group.

## Relations

- partOf: [Navigate related intent as groups](../navigate-related-intent-by-group.md){id=note:need:w7k2n4p}
- framedBy: [Enumerate a Group's Members](job-enumerate-group-members.md){id=note:job:8kq3v2m}
