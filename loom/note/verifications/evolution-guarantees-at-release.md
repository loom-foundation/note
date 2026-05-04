---
id: note:ver:ev0gk5t
name: Evolution guarantees at release
kind: verification
status: current
method: inspection
---

This verification confirms, at each release of the method, that evolution keeps its promises: the manifest declares the method version the corpus is written against, a minor or patch release breaks no corpus valid under the same major, a major release ships with a defined migration for every breaking change, nothing normative disappears without a deprecation window, and the method and its reference tool version independently.
The check inspects the release against the prior one; the verdict belongs to the Orchestrating Authority.

## Criteria

A pass requires that:

- the manifest's `methodVersion` field is present, well-formed, and names the release under check, so any reader or tool can locate the rules the corpus is written against;
- every corpus valid under the prior release of the same major validates unchanged under this release: no new required field, no narrowed value set, no reinterpreted existing construct;
- if the release opens a new major, every breaking change carries a published migration: what changed, what a conforming corpus must do, and a mechanical procedure where one is possible;
- every normative construct removed in this release was marked deprecated in at least one prior minor release, so no obligation vanishes without warning;
- the release notes version the method's specifications alone, with no tool release coupled to it and no tool version constraining it.

A pass is all five holding for the release under check.

## Procedure

By inspection.
At each release, a reader compares the specifications against the prior release: diffing required fields, value sets, and construct meanings for silent breaks; checking each intentional break against the migration notes; and checking each removal against the deprecation markings of prior minors.
The reader validates a corpus authored under the prior release, unmodified, against the new specifications as the compatibility probe.
The inspection needs only the two releases' files, so it is reproducible by anyone with the repository history.

## Evidence

A run produces a release report: the version declaration, the compatibility probe's outcome, the migration coverage of any breaking change, and the deprecation trail of any removal.
The report is kept with the release by the Orchestrating Authority; it is not stored in this artifact.

## Relations

- verifies: [Non-breaking evolution with a guaranteed forward path](../requirements/stakeholder/non-breaking-evolution.md){id=note:req:peh9g30}
- verifies: [Declared method version](../requirements/system/declared-method-version.md){id=note:req:vtbay6d}
- verifies: [Within-major backward compatibility](../requirements/system/within-major-compatibility.md){id=note:req:c62shkd}
- verifies: [Defined migration across majors](../requirements/system/defined-major-migration.md){id=note:req:2kvyew2}
- verifies: [Deprecation window before removal](../requirements/system/deprecation-window.md){id=note:req:af33evm}
- verifies: [Independent versioning of method and tool](../requirements/system/independent-versioning.md){id=note:req:zscyz82}
