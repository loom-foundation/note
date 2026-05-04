---
id: note:need:29519ms
name: Inherited intent on fork
kind: need
persona:
  - "[Forking or Spun-Out Team](../personas/forking-team.md){id=note:persona:aqx1gv3}"
  - "[Future Maintainer](../personas/future-maintainer.md){id=note:persona:k04ezkv}"
  - "[Reviewer or Auditor](../personas/reviewer-auditor.md){id=note:persona:9jz2a3w}"
status: current
validation: inferred
---

When a project is forked to be run on its own (or a unit is spun out into its own company), a Forking or Spun-Out Team wants the obligations it inherited to come with it and stand on their own, so the new repository is self-contained from day one even when the origin's repositories are no longer reachable.

## Illustrative situations

These shaped the need and are kept here, in the problem space, rather than restated in the requirements they motivate;
they are inferred from common patterns, not observed by us.

1. Fork that walks away.
   A team forks a project repository to run it on its own.
   The need, requirement, and specification tree that applies to the fork descends partly from intent owned in the origin's other repositories;
   for the fork to stand alone, that effective intent must come across with it, resolved standalone, so the fork no longer depends on repositories it has stopped tracking.

2. Incubator spin-out.
   A unit is incubated inside a parent organization and operates under obligations the parent set;
   when the unit is extracted into its own company, the parent's repositories are no longer reachable.
   The effective obligations the unit carried, and the parent intent they descended from, must survive the cut so the new entity is self-contained rather than launching with a gap where the inherited obligations used to be.

## Source

The fork-and-detach pattern and the incubator-and-spin-out pattern are both real and external.

The need for inherited intent to travel and resolve standalone is inferred from those patterns;
since the method does not yet exist, the need has not been observed in practice.
