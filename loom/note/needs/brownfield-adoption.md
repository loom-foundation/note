---
id: note:need:b3k9w2t
name: Adopt the method on a system that already exists
kind: need
persona:
  - "[Adopter](../personas/adopter.md){id=note:persona:n66rj1d}"
  - "[Future Maintainer](../personas/future-maintainer.md){id=note:persona:k04ezkv}"
  - "[Product Owner](../personas/product-owner.md){id=note:persona:pd8w3kq}"
  - "[Reviewer or Auditor](../personas/reviewer-auditor.md){id=note:persona:9jz2a3w}"
status: current
validation: observed
---

When an Adopter takes up the method on a system that already exists, with code, documents, and decisions already in place, it wants to capture the intent behind what was built incrementally, rather than starting from scratch or pausing to document everything up front, and to record reconstructed intent at its honest confidence so a best guess is never mistaken for a settled decision, so the method can be adopted on real, in-flight systems and not only on new ones.

## Source

The reality that most systems adopting a requirements method already exist, greenfield being the exception, and the documented failure of big-bang reverse-documentation efforts.

Also surfaced by research into tools that bootstrap context by reading an existing codebase rather than scaffolding blanks.

External to this corpus and not derived from it.

This need is distinct from [Ceremony sized to the stakes](right-sized-ceremony.md){id=note:need:p7ekr3c}, which concerns matching rigor to the stakes of the work, and from the tool's own frictionless-onboarding need on the Sett side, which concerns the cost of standing up the tool from an empty repository;
this need concerns recovering intent from a system that already exists.
