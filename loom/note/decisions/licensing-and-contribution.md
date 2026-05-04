---
id: note:dec:k8w3n2p
name: Licensing and contribution model
kind: decision
status: current
decided: 2026-06-03T06:34:46Z
---

Note is licensed under Creative Commons Attribution 4.0; contributions are governed by the Developer Certificate of Origin with no Contributor License Agreement; and implementer patent peace comes from a standalone patent non-assertion pledge.

## Context

Adopters commit long-lived corpora to this method, so its licensing must guarantee three things at once: that anyone may practice and implement the method without permission, that contribution stays open with no gate, and that stewardship can later transfer to a foundation without re-papering the rights.
A methodology also licenses differently from software: copyright protects only the expression and never the method itself, so the load-bearing questions are the adaptability of the text, the provenance of contributions, and patent peace for independent implementations, which no text license reaches on its own.

## Decision

- Note, normative text and explanatory prose alike, is licensed under Creative Commons Attribution 4.0 International (CC BY 4.0).
  Copyright protects only the expression, not the method, so anyone may practice and implement Note freely; the license governs only the copying and adapting of the text.
- Implementer patent peace is provided by a standalone patent non-assertion pledge, maintained by The Loom Foundation (`governance/patents.md` in the `org` repository), covering The Loom Method and its parts, with defensive termination.
- Contributions are governed by the Developer Certificate of Origin 1.1, signed off on every commit, inbound-equals-outbound, with no Contributor License Agreement and no copyright assignment.
- Copyright is held by the author, with the intent to transfer stewardship, and the trademarks of The Loom Method, to a Loom Foundation on its incorporation.

Note is one part of The Loom Method; the method's other parts are licensed and governed in their own repositories, and the trademark and certification policy is maintained by The Loom Foundation (`governance/trademarks.md` in the `org` repository). This record decides Note's licensing only.

## Forces and trade-offs

CC BY 4.0 maximizes adoption, translation, and reuse at the cost of permitting divergent adaptations of the text; that cost is accepted because the method's conformance vocabulary, not its license, is what keeps a divergent restatement from passing as the method.
The Developer Certificate of Origin keeps contribution frictionless at the cost of resting on the sign-off's good faith rather than a signed agreement; accepted because inbound-equals-outbound still preserves a clean stewardship transfer with no copyright assignment to administer.
A standalone patent pledge reaches independent implementations, which a text license cannot, at the cost of one more governance file to maintain; accepted, with the pledge maintained by The Loom Foundation as a shared governance instrument in the `org` repository and referenced here rather than copied.

## Alternatives considered

- A single permissive license (Apache-2.0) over the methodology text: rejected. Apache-2.0's patent grant is tied to the text, not to implementing the described method, so it reads poorly on prose and does not cleanly deliver implementer patent peace, which the pledge provides instead.
- Creative Commons ShareAlike or NoDerivatives for Note: rejected. ShareAlike adds implementer friction, and NoDerivatives would block adaptation and translation of the methodology text, against universal participation.
- A specification license, the Community Specification License: rejected. A method is not copyrightable, so a right-to-implement framing adds little, and its patent peace is already given by the pledge.
- A Contributor License Agreement with copyright assignment: rejected. The Developer Certificate of Origin with inbound-equals-outbound keeps governance open and still enables a later foundation donation.

## Driven by

- groundedIn: [Intent that outlives its tooling](../needs/intent-outlives-tooling.md){id=note:need:jwvn9b7}
- groundedIn: [Universal participation](../requirements/stakeholder/universal-participation.md){id=note:req:j4kecn7}
- groundedIn: [Durable, portable intent](../requirements/stakeholder/durable-portable-intent.md){id=note:req:93kczqj}
