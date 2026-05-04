---
id: note:dec:nkf13dw
name: Unknown frontmatter fields are reported, never fatal
kind: decision
status: current
decided: 2026-07-02T10:44:22Z
---

A frontmatter field no enabled pack declares is a warning-tier finding: reported, preserved untouched by any tool that rewrites the artifact, and never an error.

## Context

No specification said what a reader does with a field it does not know.
The within-major evolution promise depends on the answer: a minor release may add an optional field, so a corpus written against a later minor reaches earlier readers carrying fields they never learned.
A reader that errors breaks the compatibility guarantee from the consuming side; one that silently ignores hides typos and drift; one that strips on rewrite destroys another release's data.

## Decision

- An unknown field is reported as a warning-tier finding naming the field; the artifact stays well-formed.
- A tool that rewrites an artifact preserves unknown fields byte-for-byte.
- No profile escalates the finding to an error; a stricter posture toward stray fields is review judgment, not conformance.
- The substrate's conformance-floor section states the posture beside the frontmatter it governs.

## Forces and trade-offs

The warning posture lets a typo (`stauts:`) survive validation, found only by a human reading the report.
Accepted: the typo becomes visible the moment the required field it displaced is missed, while the reverse trade (erroring on unknowns) makes every future optional field a breaking change, which no deprecation machinery can repair.
Compute and Report already commits the method to this shape: the corpus represents, checks report, and authority to act stays outside.

## Alternatives considered

- **Unknown fields are errors.**
  Rejected: it converts every additive minor into a de facto major for older readers, hollowing the within-major guarantee.
- **Unknown fields are silently ignored.**
  Rejected: drift and typos vanish from view, and a rewrite that drops what it ignored destroys data; silence is the one posture that can lose information.

## Driven by

- groundedIn: [Within-major backward compatibility](../requirements/system/within-major-compatibility.md){id=note:req:c62shkd}
- groundedIn: [Compute and Report](../principles/compute-and-report.md){id=note:principle:6e7f28k}
