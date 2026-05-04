---
id: note:req:m9w4k7p
name: Constrained, checkable obligation phrasing
kind: requirement
level: system
type: functional
status: current
---

Note shall ensure that a requirement's obligation, including a conditional one that holds on an event, in a state, in an unwanted situation, or for an optional feature, can be expressed in a constrained form whose trigger and response are explicit and checkable.

A profile may require such a form; the Conformance Core does not.

## Rationale

Unambiguous, testable obligations need a form in which a condition is not buried in prose but is explicit enough to be read and checked the same way by every human and agent.

This requirement obliges that such a form be available and checkable, without committing the method to one syntax: the constrained convention is a profile's choice and a specification concern, so the method is not wedded to it.

Proportionality holds, a prototype writes plain obligations and pays nothing, a program that wants the discipline adopts the profile.

## Relations

- derivedFrom: [Unambiguous, testable obligations](../stakeholder/unambiguous-testable-obligations.md){id=note:req:h6n3k8w}
- delivers: [No Vague Terms Left to Interpret](../../offerings/precise-requirements/pr-no-vague-terms.md){id=note:pr:nc3x0mb}
- delivers: [The Passing Condition Is Written In](../../offerings/precise-requirements/pr-passing-condition-stated.md){id=note:pr:53t8sdd}
