---
id: note:principle:6e7f28k
name: Compute and Report
kind: principle
status: current
altitude: operating
---

The System derives the state that an authority-touching question needs from the substrate of record, and reports it for an Orchestrating Authority to decide and enforce.
It computes and reports; it holds no authority of its own.

Wherever a capability touches authority, approval, permission, gating, or who may act, the System surfaces the computed state and the evidence behind it, and leaves the decision and its enforcement outside itself.

## Why this matters

Features that look like they need authority recur: sign-off, permissioned writes, gating a merge, deciding who may act.

Building that authority into the System would duplicate control the Orchestrating Authority already holds, and because any actor with file access can bypass the System, an authority the files cannot enforce is advisory dressed as structural.

Deriving the state and reporting it keeps the corpus operable by any actor, keeps authority where identity actually lives, and keeps every derived view from silently becoming a second source of truth.

The risk this principle mitigates is the loss of trust that follows when a representation layer also enforces: an authority the files cannot back becomes a false guarantee, and derived views harden into a second, contradictory source of truth.

The positive rule also has a single-source-of-truth payoff for the corpus itself: the same idea is otherwise re-derived, with wording drift, in requirement after requirement, and naming it once gives it one home.
The negative face of this commitment is stated as an obligation in the representation-not-enforcement requirement; this principle states the positive rule that obligation follows from.

## How to apply

When a new capability seems to need authority, do not build the authority.

Identify the signal already in the substrate, a signed commit or tag, a pull-request approval, a CODEOWNERS entry, file content, the computed graph, compute the state it implies, and report it as a derived view, advisory and non-authoritative.

Route the decision and any gate to the Orchestrating Authority, which alone holds identity and the adopter's policy.

The litmus test: if a statement reaches into who may act or whether an action is permitted, the System computes and reports it; it does not decide it.

## Considered alternative

Build the enforcement into the System, so it gates merges, blocks writes, or confers approval directly.

Discarded: it duplicates the control the Orchestrating Authority already provides, it is bypassable by any actor with file access and so gives a false guarantee, and it turns derived views into authoritative state, the very drift the System exists to avoid.

## Origin

The separation of policy from mechanism in operating-system design (Brinch Hansen; the Hydra system's policy and mechanism separation, Levin and colleagues), and the policy-decision-point and policy-enforcement-point split in access control (as in XACML), where one component computes a decision and a separate component enforces it.

The application to a methodology and its tool is this project's; the access-control and mechanism-policy lineage is the established part, the framing here is ours.
