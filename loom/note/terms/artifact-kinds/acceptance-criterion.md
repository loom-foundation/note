---
id: note:term:vthp0e7
name: Acceptance Criterion
kind: term
status: current
---

A solution-free condition that defines what "acceptable" means for a requirement or need, authored before build, declarative in form: it states the what-acceptable, naming a measurable threshold or observable outcome, and names no mechanism by which the condition is achieved or checked.
An Acceptance Criterion is distinct from a Verification: the criterion declares the condition; the Verification is the executable check that confirms the condition holds.

One criterion is one artifact with one id; a requirement may be qualified by more than one criterion, each a separate artifact.

## Inclusion test

Is it a solution-free, pre-build declaration of the condition under which a requirement or need is judged acceptable?
If it names a mechanism (how to build or how to test), it is not an Acceptance Criterion.
If it records a pass or fail result, it is evidence held by the Orchestrating Authority, not a criterion.
If it is the executable check rather than the declarative condition, it is a Verification.

## Relations

- *contrasts with* [Verification](verification.md){id=note:term:6wmj8e9}

## Origin

Oxford: "acceptance: the action of consenting to receive or undertake something offered; criterion: a principle or standard by which something may be judged or decided".

In agile and requirements engineering, acceptance criteria are the conditions a product or story must satisfy for the team to accept it as complete.
They sit at the intersection of requirements engineering (ISO/IEC/IEEE 29148, where stakeholder acceptance criteria are distinct from verification methods) and agile practice (where a Definition of Done and story acceptance criteria predate build and define the target, not the test script).
The Note usage sharpens the distinction further: the criterion is the declarative what-acceptable authored before build; the Verification is the separate executable artifact that checks whether the criterion holds at run time.
