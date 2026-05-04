---
id: note:need:jwvn9b7
name: Intent that outlives its tooling
kind: need
persona:
  - "[Organization or Platform Owner](../personas/organization-owner.md){id=note:persona:6ek4j8b}"
  - "[Future Maintainer](../personas/future-maintainer.md){id=note:persona:k04ezkv}"
status: current
validation: observed
---

When an Organization or Platform Owner captures the intent behind a system, it wants that intent to stay readable and usable by whoever maintains the system later, no matter which tools come and go, so the intent is not lost when a vendor or a tool is.

## Source

The documented behavior of proprietary requirements tools, where intent is locked to a vendor store, and the well-known lossiness of migrating between such tools.

External to this corpus and not derived from it.

This need is distinct from [Participation without special tools](participation-without-special-tools.md){id=note:need:63w7v3e}, which concerns access when the preferred tool is not installed in the current environment; this need concerns access when the tool is gone or the corpus is inherited. They share the plain, tool-independent format that resolves both.
