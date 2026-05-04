---
id: note:dec:v5chm3s
name: The method version scheme
kind: decision
status: current
decided: 2026-07-02T10:44:22Z
---

The method's version is major.minor.patch over its specifications: major for a release carrying any breaking change, minor for additive surface that keeps every within-major guarantee, patch for clarification that changes no surface.
While the major is 0 the same guarantees bind; pre-1.0 signals the method's maturity, never weaker promises.

## Context

The manifest declared its methodVersion provisional, the scheme unspecified, and the owner has now set the current release at 0.5.0 with 1.0 ahead.
The [Version](../terms/conformance-and-evolution/version.md){id=note:term:hstscqt} term already fixes the major.minor.patch shape and its Semantic Versioning lineage, and the evolution guarantees are ratified obligations: a declared version, within-major backward compatibility, migration across majors, a deprecation window, and tool-independent versioning.
What was missing was the binding: which guarantee each position of the number carries for the method itself.

## Decision

- **major** increments on a release carrying any breaking change: a corpus valid under the prior major can fail, or an existing construct changes meaning; it ships with a defined migration for every such change.
- **minor** increments on additive surface (a new kind, verb, field, profile discipline, or check) under which every corpus valid at the same major stays valid and unreinterpreted; a removal only completes a deprecation window opened in an earlier minor.
- **patch** increments on clarification or erratum that adds and removes no surface.
- **No 0.x escape hatch.**
  Semantic Versioning's custom that anything may change before 1.0 is refused; the guarantees above bind at every major, 0 included.
- **The number covers the method's specifications alone.**
  The reference tool versions independently and no tool release constrains a method release.
- The manifest cites this scheme and drops "not yet specified" from its wording.

## Forces and trade-offs

Refusing the 0.x escape hatch costs freedom exactly where a young method most wants it, and it means a pre-1.0 mistake is paid for with a major bump or a deprecation window rather than a quiet rewrite.
Accepted: the earliest adopters carry the most conversion risk and the least leverage, and the corpus has already ratified the compatibility obligations without a pre-1.0 exception; the scheme only makes the number carry them.

## Alternatives considered

- **Calendar versioning.**
  Rejected: a date encodes when a release happened, not whether it breaks a conforming corpus, which is the one question a reader asks the number.
- **Free-form pre-1.0 markers with the scheme deferred to 1.0.**
  Rejected: it leaves the declared version unactionable for tools and readers exactly in the period the method changes most.

## Driven by

- groundedIn: [Declared method version](../requirements/system/declared-method-version.md){id=note:req:vtbay6d}
- groundedIn: [Within-major backward compatibility](../requirements/system/within-major-compatibility.md){id=note:req:c62shkd}
- groundedIn: [Defined migration across majors](../requirements/system/defined-major-migration.md){id=note:req:2kvyew2}
