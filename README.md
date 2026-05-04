# Note

Note is a methodology for capturing intent (needs, requirements, and design) as plain-text, Git-native artifacts that any actor with file access can read and author. This directory is Note's corpus: the controlled vocabulary, the needs, requirements, specifications, decision records, terms, personas, and principles that define the method.

Note is a part of **The Loom Method**, the methodology family that also includes the Loom Manifesto and Sett, Note's reference tool. It is *part of, but depends on nothing in,* The Loom Method: a team can adopt Note on its own, the way it would adopt any requirements tool, with its own continuous integration and code review playing the roles an orchestrator would otherwise play. Note's corpus, terminology, and principles are self-contained.

Sett, Note's reference tool, is a separate repository in The Loom Method; it computes over these artifacts and proposes authoring changes to them, validated as they are produced, while holding no authoritative state of its own: it writes, but it does not decide.

## Reading order

Before authoring or modifying anything under `note/`, read `meta/README.md` (the three compartments this corpus keeps apart), `meta/compartmentalization.md` (the discipline that keeps them apart), and `meta/prose-conventions.md` (how the corpus's prose is written). Then, to understand the corpus itself:

1. `loom/note/terms/`, the controlled vocabulary. Every load-bearing word used elsewhere is fixed here, once; start at `loom/note/terms/README.md`.
2. `loom/note/principles/`, the commitments the authoring obeys.
3. `loom/note/context.md`, the boundary.
4. `loom/note/needs/`, then `loom/note/requirements/`, then `loom/note/specifications/note/`.

## Layout

```
note/
├── README.md
├── docs/
├── loom/
│   └── note/
│       ├── context.md
│       ├── manifest.md
│       ├── terms/
│       ├── personas/
│       ├── principles/
│       ├── conventions/
│       ├── needs/
│       ├── offerings/
│       ├── value-propositions/
│       ├── requirements/
│       │   ├── stakeholder/
│       │   └── system/
│       ├── decisions/
│       ├── specifications/
│       │   └── note/
│       └── verifications/
├── meta/
│   ├── README.md
│   ├── compartmentalization.md
│   └── prose-conventions.md
└── templates/
```

The corpus of artifacts lives under the `loom/` umbrella; `meta/` and the governance files sit alongside it at the corpus root. The principles live under `loom/note/principles/`, and the specifications for Note live under `loom/note/specifications/note/`.

## The recursion, stated plainly

This corpus uses Note to specify Note. The consequence is that `loom/note/specifications/note/` is at once the design of the product and the normative definition this corpus conforms to. That is intentional dogfooding. While the method is below 1.0, the corpus uses the proposed format as a working draft and will be migrated to the stable format when the method reaches 1.0, under the forward-path guarantee in `loom/note/requirements/stakeholder/non-breaking-evolution.md`.

## Licensing and contribution

Note is licensed under CC BY 4.0 (see [`LICENSE`](LICENSE)). Copyright covers only the expression, not the method: anyone may practise and implement Note freely, in any tool, and the artifacts you author by applying it are entirely yours. A patent non-assertion pledge maintained by The Loom Foundation (`governance/patents.md` in the `org` repository) covers independent implementations. Contributions are under the Developer Certificate of Origin 1.1, inbound = outbound, with no Contributor License Agreement and no copyright assignment; see [CONTRIBUTING.md](CONTRIBUTING.md). Trademarks and conformance certification are governed by The Loom Foundation; see `governance/trademarks.md` in the `org` repository.
