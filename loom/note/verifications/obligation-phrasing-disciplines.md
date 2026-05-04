---
id: note:ver:e4rsfch
name: Obligation phrasing disciplines
kind: verification
status: current
method: analysis
---

This verification confirms the phrasing disciplines that keep obligations checkable: every requirement lead is a shall statement in one of the constrained patterns, functional and non-functional obligations state outcomes without prescribing mechanism, and acceptance conditions are authorable as their own artifacts that qualify the obligation they sharpen.
The check is a static pass over the requirement and acceptance-criterion artifacts; it computes and reports findings only, and the verdict belongs to the Orchestrating Authority.

## Criteria

A pass requires that:

- every requirement lead is a single sentence built on `shall`, matching one of the constrained patterns (ubiquitous, event-driven, state-driven, optional-feature, or unwanted-behavior), so the trigger and the required response are separable by a reader without interpretation;
- no functional or non-functional obligation names a mechanism, technology, or design in its normative sentence: the obligation states what must hold, and any illustrative how is confined to non-normative prose;
- each obligation is testable as phrased: a reader can state, from the sentence alone, what observation would show it violated;
- an acceptance criterion is authorable as its own artifact carrying a `qualifies` relation to the obligation it sharpens, and every authored one names measurable conditions rather than restating the obligation.

A pass is zero failures across the requirements in force.

## Procedure

By analysis.
A static reader scans every requirement lead for the shall form and classifies it against the constrained patterns, flagging any lead that fits none; it scans normative sentences for mechanism terms and flags solution language; and it enumerates the acceptance-criterion artifacts, validating each `qualifies` edge and checking each criterion for measurable conditions.
Pattern classification and mechanism detection are judgment-assisted: the reader records its classification per lead so a reviewer can re-judge any call.
The reader only reads; it executes nothing, so the check is reproducible by anyone with the repository.

## Evidence

A run produces a report: the per-lead pattern classification, any lead outside the patterns, any mechanism language found in a normative sentence, and the acceptance-criterion census with its `qualifies` edges.
The report is kept with the run by the Orchestrating Authority; it is not stored in this artifact.

## Relations

- verifies: [Unambiguous, testable obligations](../requirements/stakeholder/unambiguous-testable-obligations.md){id=note:req:h6n3k8w}
- verifies: [Constrained, checkable obligation phrasing](../requirements/system/constrained-checkable-phrasing.md){id=note:req:m9w4k7p}
- verifies: [Author solution-free acceptance conditions](../requirements/stakeholder/definable-acceptance.md){id=note:req:5m2hwtj}
