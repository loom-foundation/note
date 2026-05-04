---
id: note:req:6n6jdyq
name: Hierarchically scoped intent
kind: requirement
level: stakeholder
type: functional
status: current
---

Intent shall be expressible at the scope where it first becomes load-bearing and inherited by the scopes beneath it, so that an obligation is stated once and applies wherever it is in force.

Any scope shall be able to deviate from inherited intent, whether by strengthening it, replacing it, or removing it, in a way that is explicit, attributable, and rationale-bearing rather than a silent copy.

Where intent applies across more than one line of the hierarchy at once, a scope shall be able to inherit it from more than one source.

This is an opt-in discipline (see [Progressive, right-sized adoption](progressive-adoption.md){id=note:req:srzdd07}): a single-scope project never needs it and pays nothing for it;
it earns its place the moment the same obligation must hold across more than one team, product, or organization in the corpus.

## Source

See the Source and the illustrative situations of [State a shared obligation once](../../needs/state-obligation-once.md){id=note:need:257yf29}.

## Rationale

The alternative to scoped inheritance is duplication, and duplication drifts: the first time a shared obligation changes, the hand-copied instances disagree and no rule flags the inconsistency.

Scoped intent makes the single statement reusable and every exception not merely visible but attributable and auditable;
one can ask who deviated, where, and on what justification.

That is the working distinction this requirement draws: inheritance without a record of exceptions is just another silent copy, so the value is not the inheritance alone but the accountable trace of every departure from it.

The requirement names the three deviations a stakeholder needs (strengthen, replace, remove) and the multi-source case as capabilities, not as operators;
the operators and the inheritance structure are specification.

## Relations

- addresses: [State a shared obligation once](../../needs/state-obligation-once.md){id=note:need:257yf29}
- delivers: [Conventions Bind Where They Apply](../../offerings/scoped-intent/pr-conventions-bind-where-they-apply.md){id=note:pr:yt26nj2}
- delivers: [Single Statement, No Copies](../../offerings/scoped-intent/pr-single-statement-no-copies.md){id=note:pr:yfx7ffj}
