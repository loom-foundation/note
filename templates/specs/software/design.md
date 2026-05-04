---
id: <namespace>:spec:<opaque>
name: <Name>
kind: specification
status: draft
authority:
  - contracts/design/tokens.json
---

This specification defines the visual design vocabulary for <product or brand>: the token values and the semantic role each token plays in the interface.

## Authority

Where this project opts in to the W3C Design Tokens Community Group format, the authoritative token values are held in a JSON file at the path listed in `authority`, conforming to the W3C Design Tokens JSON format (Community Group draft, treat as opt-in until ratified).
The external file governs on any divergence between it and this specification.
An implementation's conformance to the token contract is a separate Verification; it is not established here.

Where the project does not use a machine-readable token file, remove `authority` entries and set `authority: []`; this section then serves as a prose record of the color and type values only.

## Colors

<!-- One row per semantic color token. -->

| Token | Value | Role |
|---|---|---|
| `<token.name>` | `<#hex or var ref>` | <One sentence: when and why this color appears, not its aesthetic description.> |

## Typography

<!-- One row per typographic scale entry. -->

| Token | Value | Role |
|---|---|---|
| `<token.name>` | `<value>` | <One sentence: the reading context this scale entry serves.> |

## Spacing and Sizing

<!-- One row per spacing or sizing token. -->

| Token | Value | Role |
|---|---|---|
| `<token.name>` | `<value>` | <One sentence: the layout relationship this dimension enforces.> |

## Border Radius

<!-- One row per radius token. -->

| Token | Value | Role |
|---|---|---|
| `<token.name>` | `<value>` | <One sentence: the surface category this rounding applies to.> |

## Semantic Roles

The sections above carry values; this section carries meaning.
For each semantic grouping in the token set, state the design intent: the emotion, hierarchy signal, or functional distinction the token cluster communicates, and the surface areas it governs.
This prose is irreducible: no token file can express it.

### <Color role group, e.g. Brand>

<One short paragraph: intent, usage context, and any constraint on combination with other tokens.>

### <Color role group, e.g. Feedback>

<One short paragraph: how error, warning, success, and informational states are expressed and distinguished.>

### <Typography role group, e.g. Hierarchy>

<One short paragraph: how the scale establishes reading hierarchy across headings, body, and supporting text.>

## Rationale

<!-- Include only where a choice is left open by the token contract and worth recording. -->
<!-- Example note: single paragraph per decision; state what was chosen and why alternatives were set aside. -->

## Relations

- satisfies: [<Requirement>](../../requirements/system/<requirement>.md){id=<namespace>:req:<opaque>}
