---
id: note:gain:nh30ccc
name: No Team Left on a Stale Obligation
kind: gain
expectation: required
persona:
  - "[Organization or Platform Owner](../../personas/organization-owner.md){id=note:persona:6ek4j8b}"
  - "[Forking or Spun-Out Team](../../personas/forking-team.md){id=note:persona:aqx1gv3}"
status: current
---

When an Organization or Platform Owner updates a shared obligation in the repository that owns it, the change reaches every dependent: no downstream team keeps working against the superseded version unknowingly, so a Forking or Spun-Out Team can update and release its own repository on its own schedule and still know when a parent-level obligation it depends on has changed.

## Relations

- partOf: [Operate one corpus across many repositories](../operate-corpus-across-repositories.md){id=note:need:03gs33j}
- framedBy: [Build Own Intent on a Parent Obligation](job-depend-on-cross-repository-intent.md){id=note:job:a8f4sqd}
