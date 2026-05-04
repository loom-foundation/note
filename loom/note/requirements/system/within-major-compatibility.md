---
id: note:req:c62shkd
name: Within-major backward compatibility
kind: requirement
level: system
type: constraint
status: current
---

No release within a major version shall render a corpus that conformed under an earlier release of that major version non-conformant.
Backward compatibility holds across the whole of a major line.

## Rationale

The forward-path guarantee is cheap to honor if a corpus never breaks within a major line: an adopter can take every patch and minor release without fear, and any break is confined to a deliberate, migrated major step.

This bounds where breakage may occur, not how it is detected, which is specification.

## Relations

- derivedFrom: [Non-breaking evolution with a guaranteed forward path](../stakeholder/non-breaking-evolution.md){id=note:req:peh9g30}
