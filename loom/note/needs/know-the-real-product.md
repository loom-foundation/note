---
id: note:need:m0h1ncg
name: Know the real product behind the intent
kind: need
persona:
  - "[Product Owner](../personas/product-owner.md){id=note:persona:pd8w3kq}"
  - "[Organization or Platform Owner](../personas/organization-owner.md){id=note:persona:6ek4j8b}"
  - "[Implementer](../personas/implementer.md){id=note:persona:s4v9hn2}"
  - "[Future Maintainer](../personas/future-maintainer.md){id=note:persona:k04ezkv}"
  - "[AI Agent](../personas/ai-agent.md){id=note:persona:sk3pzm2}"
status: current
validation: inferred
---

When a reader reads a corpus, they want to know how the captured intent corresponds to the actual product (which part of the product is responsible for each piece of the value, and whether that intent is really built yet, and, where the product has several versions, what each version actually has) so that the corpus tells them the product's real, present state and not only what was once intended.

This need is distinct from [Articulate value offered](articulate-value-offered.md){id=note:need:9w2k4pt}, which names the value the product offers; this need names the value's provider and its built state.

## Illustrative situations

A product is delivered by several services maintained separately, and a reader asks which service is responsible for the click analytics the product promises; the answer, if it exists at all, is scattered across prose and tribal memory.

A corpus scopes a feature for a future version beside features that shipped long ago, and the two read identically on the page, so a reader cannot tell what the product can do today.

A laptop ships in two versions: the earlier one has no fingerprint sensor, the later one does. A reader needs to tell, from the corpus, that passkey login protected by biometric authentication is possible on the later version and not the earlier one, a capability whose availability depends on which version actually has the sensor.
