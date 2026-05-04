# Corpus structure

How a Note corpus is laid out on disk.
This is orientation, not normative text; the binding rules live in [The substrate](../loom/note/specifications/note/substrate.md){id=note:spec:tkhd63e} (the file format and manifest schema) and [Adopter corpus placement](../loom/note/decisions/corpus-placement.md){id=note:dec:q2v7nk3} (the umbrella, discovery algorithm, and fallbacks).

## The loom/ umbrella and layers

A corpus is not a single body of intent.
It is a set of Layers, each a coherent concern riding the one substrate, anchored under a single `loom/` umbrella at the repository root.

Three Layers are named.
The **note** Layer is live: it carries intent, in the spine and discovery packs.
The **plan** Layer is deferred: it is designed but not yet specified.
The **guild** Layer is reserved: named for disciplines, roles, and skills, unspecified in this version.

Each Layer sits in its own subdirectory under the umbrella: `loom/note/`, `loom/plan/`, `loom/guild/`.
Each holds its own manifest and its own kind subdirectories beneath its layer-root.

## The layer-root rule

A layer-root is wherever that Layer's manifest sits.
The `loom/<layer>/` folder is the navigational mirror of an enabled Layer, never the switch.
The manifest is authoritative for whether a Layer is enabled and for everything that affects validation; folder presence is a derived mirror.

## Two-step discovery

A reader or a tool finds the corpus through two steps, in order:

1. If `loom.md` is present at the repository root, read it and follow its `root:` field to the umbrella's location.
2. Otherwise, use `loom/` at the repository root.

Step one is the override for a repository that cannot place the umbrella at `loom/`.
A tool or agent that skips it indexes the wrong tree in exactly the collision case the override exists for.

## Recognized fallbacks

Placement is non-normative: identity and resolution are location-independent, and the authoritative scope lives in frontmatter, so a move never breaks a reference.
Two fallbacks are recognized for repositories the default does not suit:

- **Hidden `.loom/`** with the same internal Layer layout, for a brownfield repository that cannot take a visible root entry.
- **Bare placement**: a layer-root that sits outside any `loom/` umbrella, recognized through the layer-root rule, because the manifest is what enables the Layer.

## The archive convention

Terminal artifacts (`obsolete` or `rejected`) live under a single visible `archive/` directory at the layer-root, mirroring the kind tree beneath it.
Status is authoritative; placement is the derived mirror a tool keeps in sync.

```
loom/note/
└── archive/
    ├── decisions/
    │   └── deferred-option.md        # status: rejected
    └── requirements/
        └── system/
            └── old-latency-budget.md # status: obsolete
```

## A single-scope corpus

A small but complete note Layer for a single scope (Acme Corp's checkout system):

```
loom/
└── note/
    ├── manifest.md                           # methodVersion + namespace + profile + packs (not an artifact)
    ├── context.md                            # system boundary (acme:ctx:…)
    │
    ├── needs/
    │   ├── stay-signed-in.md                 # need profile              (acme:need:…)
    │   └── stay-signed-in/                   # facet folder, BESIDE the profile
    │       ├── job-resume-work-quickly.md    #   a job   (acme:job:…)
    │       ├── pain-repeated-logins.md       #   a pain  (acme:pain:…)
    │       └── gain-seamless-return.md       #   a gain  (acme:gain:…)
    │
    ├── offerings/
    │   ├── persistent-session.md             # offering profile          (acme:offering:…)
    │   └── persistent-session/               # facet folder, beside the profile
    │       ├── pr-remember-this-device.md    #   a pain reliever (acme:pr:…)
    │       └── gc-one-tap-return.md          #   a gain creator  (acme:gc:…)
    │
    ├── value-propositions/
    │   └── never-log-in-twice.md             # the authored pitch (acme:vp:…)
    │
    ├── requirements/
    │   ├── stakeholder/
    │   │   └── session-persistence.md        # stakeholder obligation (acme:req:…)
    │   └── system/
    │       └── session-token-lifetime.md     # system obligation (acme:req:…)
    │
    ├── specifications/
    │   └── session-token-format.md           # committed design (acme:spec:…)
    │
    ├── decisions/
    │   └── opaque-session-tokens.md          # a choice and its rejected alternatives (acme:dec:…)
    │
    ├── verifications/
    │   └── token-expiry-check.md             # pass criteria and method (acme:ver:…)
    │
    ├── acceptance-criteria/
    │   └── token-lifetime-threshold.md       # solution-free condition (acme:ac:…)
    │
    ├── terms/
    │   └── session.md                        # a defined term (acme:term:…)
    │
    ├── personas/
    │   └── returning-user.md                 # a persona (acme:persona:…)
    │
    ├── principles/
    │   └── single-source-of-truth.md         # a principle (acme:principle:…)
    │
    └── archive/
        └── requirements/
            └── system/
                └── old-session-duration.md   # status: obsolete
```

## A multi-scope corpus

A larger deployment may carry several scopes under the same note Layer.
Directory containment mirrors the single structural parent of each scope; cross-cutting and multi-parent edges are carried by id in frontmatter.

```
loom/
└── note/
    ├── manifest.md                    # layer-root manifest
    ├── context.md                     # top-level system boundary (acme:ctx:…)
    │
    ├── checkout/                      # checkout sub-scope
    │   ├── manifest.md                # sub-scope manifest (scope id in frontmatter)
    │   ├── needs/
    │   ├── requirements/
    │   └── specifications/
    │
    ├── identity/                      # identity sub-scope
    │   ├── manifest.md
    │   ├── needs/
    │   └── requirements/
    │
    └── archive/
        └── decisions/
            └── abandoned-approach.md  # status: rejected
```

## Rules the trees show

- **A need or offering profile sits BESIDE its facet folder, never inside it.**
  `needs/stay-signed-in.md` is a sibling of `needs/stay-signed-in/`; the profile is never `needs/stay-signed-in/stay-signed-in.md`.
  The same holds for an offering.
- **Facets are their own files, in the shared facet folder, prefixed by kind-segment.**
  Inside a facet folder where kinds mix, each filename starts with its id kind-segment: `job-`, `pain-`, `gain-` for a need's facets; `pr-`, `gc-` for an offering's.
- **A need with no facets is just `needs/<name>.md`.** The facet folder appears only once the need has facets.
- **Kind-homogeneous directories use no prefix.**
  `requirements/`, `decisions/`, `terms/`, `personas/`, `principles/` hold a single kind (or, for requirements, split by level into `stakeholder/` and `system/`), so the directory names the kind and the files are plain descriptive slugs.
- **All kinds use uniform opaque ids.**
  Every artifact's identity is its opaque `namespace:kind-segment:opaque` id, carried in frontmatter as the `name`-carrying `id` field.
  The field is `name`, not `title`.
  The filename is a navigation convenience, never the identity.
- **`context.md` and `manifest.md` sit at the layer-root.**
  A scope has at most one context.
  Neither the manifest nor a group `README.md` is a first-class artifact (no `id`, no `kind`).
- **One visible `archive/` per layer-root, mirroring the kind tree.**
  Terminal artifacts are placed there; status is authoritative, placement is the derived mirror.
- **Location is a convenience, not the identity.**
  The authoritative scope is in frontmatter and the id is immutable, so moving a file never breaks a reference.
