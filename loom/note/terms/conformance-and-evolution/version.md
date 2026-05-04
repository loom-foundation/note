---
id: note:term:hstscqt
name: Version
kind: term
status: current
---

The released state of the method or the tool, as major.minor.patch.

Tier (how much a project has adopted within a version) and version (how the method itself has evolved) are orthogonal axes; do not conflate them.

## Inclusion test

Does it identify a released state of the method or the tool as it has evolved over time?
If so it is a version; if instead it names how much of that release a given project has chosen to adopt, that is a tier.

## See also

Evolution across versions is governed by [Non-breaking evolution with a guaranteed forward path](../../requirements/stakeholder/non-breaking-evolution.md){id=note:req:peh9g30} and the requirements derived from it.

## Origin

General English (Oxford: "a particular form of something differing in certain respects from an earlier form or other forms of the same type").

The major.minor.patch shape follows Semantic Versioning, where the leading number signals a breaking change, the middle a backward-compatible addition, and the last a fix.
