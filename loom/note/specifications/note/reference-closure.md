---
id: note:spec:6ntj28w
name: The reference closure
kind: specification
status: current
authority: []
---

This specification fixes the reference-closure rule: given a selection of artifacts in a corpus, which further artifacts the selection pulls in so that an actor who receives the closure can read each artifact correctly and act on it faithfully, with nothing it depends on left behind, and which artifacts it only cites.
The governing question is not "what does this artifact formally depend on by a declared edge?" but "given this artifact as a starting point, what does an actor need to read it correctly and act on it faithfully?", and the answer has two parts: an artifact enters the closure either by an **edge pull**, a load-bearing relation verb leads to it, or by a **structural pull**, it is constitutive of an in-closure artifact's meaning or validity with no edge to declare.
It classifies each relation verb in the effective catalogue for the edge pull (pull its target into the closure, in a fixed direction, or cite it reference-only), fixes the structural pull as the terms, conventions, and principles in force at an in-closure artifact's scope, fixes where the closure stops at the corpus boundary, fixes how selecting a scope or a group expands to its artifacts, and fixes that the closure is the unique deterministic set the two pulls produce together, reproducible at a recorded rule version.

It follows the relation grammar of [The substrate](substrate.md){id=note:spec:tkhd63e} and the cascade procedure of [Scope and cascade](scope-and-cascade.md){id=note:spec:1r673tc}, and supplies the closure rules that [Method-defined context slice](../../decisions/method-defined-context-slice.md){id=note:dec:pk6jzwy} fixed as the method's to own and deferred to a later specification.
It defines the Reference Closure ([Reference Closure](../../terms/relations-scope-and-traceability/reference-closure.md){id=note:term:6g971kr}) as a method-fixed set; what consumes that set is out of scope here.

## What this rule owns, and what it does not

The reference-closure rule is the meaning of the graph, and the meaning alone.
It fixes which relations pull versus reference, which kinds are pulled structurally by their standing at a scope, where a corpus ends, how a scope or a group expands, that the resulting set is well-defined, and that the rule carries a version.
It fixes nothing about how the set is found or what is done with it.

This holds a three-way split on the record, so the boundary between the method and what surrounds it is explicit:

- **The method owns the rule.**
  Note fixes the closure as a property of the committed artifacts: the relation classification (the edge pull), the structural pull, the boundary, the scope and group expansion, the determinism, and the rule version.
  This is the definition a reviewer reconstructs from the files, the same ownership [Method-defined context slice](../../decisions/method-defined-context-slice.md){id=note:dec:pk6jzwy} fixed for the relevant subset.
- **A tool computes the closure.**
  How the set is found, the traversal, the algorithm, any caching, the interface, and the performance, is a tool's concern, the Sett tool in this ecosystem.
  A tool computes and reports the closure the method defines; it may differ from another tool in every way except which artifacts the closure contains ([Compute and Report](../../principles/compute-and-report.md){id=note:principle:6e7f28k}).
- **A consumer uses the closure.**
  What is done with the set, materializing it into a ground, pinning a cross-corpus reference as a dependency, gating a lockfile or a clash, belongs to the consumer downstream, Common Grounds in this ecosystem.
  This specification stops at "the closure is this set" and says nothing about adoption.

The rule is the contract the tool computes against and the consumer builds on; keeping the contract here, in the corpus, is what makes both reproducible from the files.

## The selection

A closure is taken of a selection: one or more artifacts named by durable identifier, a scope, or a group.
A single artifact is the base case of a selection of one.
A scope and a group expand to a set of artifacts first ([Scope and group expansion](#scope-and-group-expansion) below), and the closure rule then applies to that set, so every selection reduces to a set of artifacts the rule closes over.

The reference closure of a selection is the smallest set of artifacts that contains the selection and is closed under both pulls: for every artifact in the set, every artifact its edge pulls reach and every term, convention, and principle in force at its scope is also in the set.
The selection's own artifacts are always in the closure.

## Two kinds of pull

An artifact enters the closure for one of two reasons, and the rule applies both.

An **edge pull** follows a load-bearing relation verb: the artifact holds a declared edge to a target it leans on for completeness, so the target is drawn in.
This is the relation-classification table below, and it is the formal-dependency half of the closure: a closure that satisfied only the edge pull would have no dangling edge, yet could still leave an actor unable to interpret what they received, because the terms an artifact is written in, the conventions in force over it, and the principles that shape it are load-bearing by nature and carry no edge that names which artifact they govern.

A **structural pull** is that missing half: an artifact is constitutive of an in-closure artifact's meaning or validity, with no edge to declare, so it is drawn in by its standing at the scope rather than by a verb.
This is fixed under [The structural pull](#the-structural-pull) below as the terms, conventions, and principles in force at an in-closure artifact's scope.

The need's persona is the precedent the structural pull generalizes.
The spine pack already obliges that a need name its personas by the `persona` frontmatter field rather than a relation verb ([The spine pack](spine-pack.md){id=note:spec:6kjja5r}), and the closure already pulls those personas, because a need cannot be read in its own terms without the actors it is wanted by (see [Scope and group expansion](#scope-and-group-expansion)).
A persona is constitutive context that travels, carried by a per-artifact field that declares exactly which personas govern.
Terms, conventions, and principles are the same need without such a field: a convention and a principle govern by applying across a scope, not by being named on each artifact they bear on, and a term is recognized in prose by closed-vocabulary lookup, not by a declared edge.
The structural pull generalizes the persona instinct to the three kinds that have no field to carry it, reading their governance off the scope they are in force at instead.

## Relation classification

The relation classification is the edge pull.
Every relation verb in the effective catalogue is either a **pull** verb or a **reference-only** verb.
A pull verb is load-bearing for completeness: an artifact that holds a pull edge is incomplete without its target, so the target is drawn into the closure.
A reference-only verb is a citation: the edge records a real relationship, but the holder stands without the target, so the target is cited, never pulled.

A pull verb is followed in a fixed direction.
The direction is the authored direction of the edge unless a row states otherwise: the closure of a dependent artifact pulls the governing artifact it leans on, the same direction the edge reads as a true sentence `<dependent> <verb> <governing>` ([The substrate](substrate.md){id=note:spec:tkhd63e}).
Derived inverses are not separately classified: an inverse is a view of its authored edge, so following the authored edge in its pull direction is the whole rule, and a closure never expands along an inverse.

The classification below is the contestable substance of this specification, the part the method owners ratify.
It is drawn over the effective verb catalogue: the substrate decision edges and term relations, plus the spine pack, with the discovery and governance pack rows classified for corpora that enable those packs.

### Spine and substrate verbs

| Verb | Authored on | Pull / reference | Direction (what the closure pulls) |
|---|---|---|---|
| `addresses` | requirement (or offering) | pull | the need (or job) it serves |
| `derivedFrom` | requirement, specification | pull | the coarser requirement it refines |
| `satisfies` | specification | pull | the requirement it designs for |
| `verifies` | verification | pull | the requirement, specification, convention, or acceptance-criterion it checks |
| `qualifies` | acceptance-criterion | pull | the requirement or need whose acceptance it defines |
| `enacts` | requirement, convention | pull | the principle it enacts |
| `decidedBy` | requirement, specification, convention | pull | the decision that determined its content |
| `groundedIn` | decision | pull | the need, requirement, decision, or principle the choice rests on |
| `amends` | decision | pull | the still-current decision it modifies in place |

### Term relations

| Verb | Authored on | Pull / reference | Direction (what the closure pulls) |
|---|---|---|---|
| `is a` | the subordinate concept | pull | the broader concept it specializes |
| `is a value of` | the value | pull | the term it is a value of |
| `is part of` | the part | pull | the whole it is part of |
| `carries` | the holder | pull | the term it carries |
| `scopes` | the Context | pull | the term it scopes |
| `contrasts with` | the alphabetically-earlier term | reference-only | (not pulled) |
| `relates to` | either end | reference-only | (not pulled) |

### Discovery and governance pack verbs

These are in the effective catalogue only where the corpus enables the pack ([The discovery pack](discovery-pack.md){id=note:spec:w6nsgt1}, [The governance pack](governance-pack.md){id=note:spec:gfz6q22}).

| Verb | Authored on | Pull / reference | Direction (what the closure pulls) |
|---|---|---|---|
| `partOf` | a job, pain, or gain; a pain-reliever or gain-creator | pull | the need or offering it is part of |
| `relieves` | a pain-reliever, or a requirement | pull | the pain it relieves |
| `creates` | a gain-creator, or a requirement | pull | the gain it creates |
| `delivers` | a requirement | pull | the pain-reliever or gain-creator it delivers |
| `expresses` | a value-proposition | pull | the offering it pitches |
| `provides` | a system | pull | the offering, value-proposition, pain-reliever, or gain-creator it provides |
| `framedBy` | a pain or gain | reference-only | (not pulled) |
| `implements` | a standard, procedure, or requirement | pull | the policy or standard it makes concrete |
| `enacts` (governance) | a policy or standard | pull | the principle it enacts |

The rule for which side a row pulls is the same throughout: a pull edge pulls the artifact its holder leans on for completeness, and an artifact whose absence would leave the holder a dangling claim is load-bearing.
`contrasts with`, `relates to`, and `framedBy` are reference-only because they record a kinship a reader may follow, not a dependency the holder needs to stand: a term still means what it means without the term it contrasts with, and a pain is still a pain without the job it happens to be felt against.

A `supersedes` or `superseded_by` citation, and a `materialized` provenance block, are not relation verbs and are not closure edges: they record lineage, not a dependency the artifact leans on, so they are reference-only by construction and never pulled.
The optional `scope` and `persona` frontmatter fields are not edge pulls: `persona` is resolved through group expansion and `scope` selects the structural pull, both below.

## The structural pull

For each artifact already in the closure, the closure also draws in the **terms, conventions, and principles in force at that artifact's scope**, whether or not any edge is declared to them.
These three kinds are constitutive of an artifact's meaning and validity: the terms fix the words the artifact is written in, the conventions bind the making of the artifact, and the principles are the normative anchors its judgment answers to.
An actor who received the artifact without them could verify that no edge dangles and still misread the artifact or apply it against the wrong commitments, which is the gap the structural pull closes.

This reuses Note's existing model and invents no new mechanism for "in force at scope."
A term, a convention, and a principle each carry the common optional `scope` field and cascade like any other kind ([Scope and cascade](scope-and-cascade.md){id=note:spec:1r673tc}, which fixes the cascade over "a convention, a term ... or a principle"), so the set in force at a scope is the cascade's effective result there: every such artifact whose intent reaches the scope through the `add`, `replace`, and `disinherit` operators, with a `disinherit`ed one not in force and so not pulled.
For terms this is exactly the resolution the substrate already fixes, where a word in prose resolves "against the names and aliases of the terms ... in force at the reading scope" ([The substrate](substrate.md){id=note:spec:tkhd63e}); the structural pull pulls the artifacts behind that in-force vocabulary rather than leaving them to be looked up.
The substrate writes that in-force resolution for terms and personas, the kinds recognized as words in prose; extending it to conventions and principles is deliberate and on the same ground, since the cascade fixes all three in force at a scope by the one `scope` field, and a closure must carry what governs an artifact, not only what resolves as a word in it.
The structural pull is read off the same scope the artifact already records, so it adds no new field and no new edge.

The membership is deliberately a **superset at the scope, not a per-artifact subset**.
The closure pulls every term, convention, and principle in force at the artifact's scope, not only the ones the artifact demonstrably uses, because a convention and a principle carry no per-artifact edge naming which artifact they govern, so there is no declared subset to read, and a term's use is recognized by closed-vocabulary lookup in prose rather than by a declared edge, so deciding which terms an artifact "really" uses would require parsing rather than the corpus's own relations.
Folding all three into one scope-rule gives a single deterministic mechanism, the cascade's effective set at a scope, rather than three kind-specific heuristics, and the cost of the superset is bounded by the same scoping: a single-scope corpus pulls its whole governing vocabulary once, and a multi-scope corpus pulls only the subset in force at the selected artifact's scope, the inner scope's narrowed set rather than every term and principle anywhere in the corpus.

A term, convention, or principle drawn in by the structural pull is itself an in-closure artifact, so its own edge pulls and its own structural pull apply in turn: a term that `is part of` another term pulls that term, a convention that `enacts` a principle pulls that principle, and each is closed over at its own scope.
The structural pull stops at the corpus boundary like the edge pull: a term, convention, or principle in force at a scope but maintained in another repository is an external reference, recorded as a boundary, never followed into the upstream.

## The corpus boundary

The closure stops at the corpus boundary.
A pull edge whose target lives in the same corpus draws that target into the closure.
A pull edge whose target lives in another corpus, named by a foreign-namespace identifier and resolved across the repository boundary at a pinned version ([Cross-repository inheritance and materialization](../../decisions/cross-repository-inheritance.md){id=note:dec:h4w9k2t}), is an external reference: it is recorded as a boundary of the closure, never followed into the upstream.

The closure of a selection is therefore always a set of artifacts within one corpus, together with the set of external references it leans on but does not contain.
What becomes of an external reference, resolved live against the upstream, pinned as a dependency, or materialized into the corpus so a former external reference becomes an internal one, belongs to the consumer ([Materialization](../../terms/relations-scope-and-traceability/materialization.md){id=note:term:3yted77}).
This is what makes the closure a finite, self-contained set per corpus rather than a traversal that chases identifiers across every reachable repository: the boundary is where the method's set ends and a dependency the consumer resolves begins.

A materialized artifact already lives inside the corpus, with its provenance recorded; it is an ordinary member of the closure, closed over like any authored artifact, and the upstream it was captured from is not followed.

## Scope and group expansion

A selection of a scope or a group expands to a set of artifacts, and the closure rule then closes over that set.

**Selecting a scope** yields the artifacts load-bearing at that scope, then each one's closure.
The artifacts load-bearing at a scope are the effective intent the cascade resolves there: the obligations in force at the scope after the `add`, `replace`, and `disinherit` operators are applied, and the scope's Context ([Scope and cascade](scope-and-cascade.md){id=note:spec:1r673tc}).
The closure of the scope is the closure of that effective-intent set: every artifact the cascade leaves in force, plus every artifact those pull into.
An obligation dropped by a `disinherit` at the scope is not load-bearing there and is not pulled; an inherited obligation in force is pulled, even when it is authored in an ancestor scope, because the cascade makes it part of the effective intent at the selected scope.
Resolving the effective intent is the cascade's job; this rule consumes its result.

**Selecting a group** yields the artifacts in the group, then each one's closure.
A group is a named collection of related artifacts; a need's persona set is the worked case, where a need names its personas by the `persona` frontmatter field rather than a relation verb ([The spine pack](spine-pack.md){id=note:spec:6kjja5r}).
Where a selection names an artifact that carries such a field, the referenced personas are part of the selection's expansion and are closed over, so a need never travels without the personas it is wanted by.

After expansion, the closure rule is identical for every selection: close the expanded set under both pulls, the edge pull and the structural pull, stopping at the corpus boundary.

## Determinism and the rule version

The reference closure of a selection is a unique set, well-defined independently of how it is computed.

Determinism follows from the construction: the closure is the least set containing the selection and closed under both pulls together, the edge pull and the structural pull, which is the unique fixed point of a single monotone expansion over a finite corpus.
The two pulls compose into one operator, expand a set by every artifact its members' edge pulls reach and every term, convention, and principle in force at its members' scopes, and the closure is that operator's least fixed point; taking the two together rather than in sequence is what makes the result independent of which pull was applied first.
Two actors, or one actor twice, deriving the closure of the same selection under the same rule version obtain the same set, whatever order either visited the edges and scopes in, because the set is defined by membership, not by traversal.
The edge pulls form an acyclic structure on the hierarchical edges ([The substrate](substrate.md){id=note:spec:tkhd63e}), and the structural pull reads a deterministic cascade result at each scope; where a cycle is admissible among non-hierarchical pull edges, the least-fixed-point definition still terminates on a finite corpus and yields one set.
An external reference contributes a boundary marker, not a member, so an upstream that is momentarily unresolvable changes which references are reported as external, never which internal artifacts are in the closure; the internal set is asserted over the resolvable corpus, as the cascade's global properties are ([Validation State](../../terms/conformance-and-evolution/validation-state.md){id=note:term:fjmzfre}).

The rule itself carries a version.
The classification table, the structural pull, the boundary, and the expansion are the rule; when the rule evolves, for instance when a new pack adds verbs, a verb is reclassified, or the structural pull's kind set changes, the change is a new rule version.
A closure recorded against a rule version is reproducible: applying that version's classification to the committed artifacts reproduces the same set, so an old closure is auditable after the rule has moved on.
The rule version is the method version the corpus conforms to ([The corpus manifest](../../decisions/corpus-manifest.md){id=note:dec:mf3k9w2}); a closure that must outlive the rule records the method version it was taken under, the way a materialized copy records the upstream version it was frozen at.

## Rationale

The closure is defined by classifying relations rather than by listing artifacts, so the same rule serves a three-artifact prototype and a regulated corpus, and a new kind or pack extends the catalogue without rewriting the rule.
Pull versus reference is the one distinction completeness turns on: a selection that travels must carry what it leans on and may leave behind what it merely cites, and the table is where that judgment is made once, on the record, for the method owners to ratify rather than for each tool to guess.

The structural pull is what keeps the closure interpretable, not merely edge-complete: an artifact carries terms it is written in, conventions in force over its making, and principles its judgment answers to, none of which declare a per-artifact edge, so a closure that followed only edges could be formally whole yet unreadable.
Reading those three off the scope they are in force at, by the cascade the method already fixes, generalizes the instinct the spine pack already had for personas, where a need carries the actors it is wanted by, to the kinds that have no field to carry it.
The membership is a scope-level superset on purpose: conventions and principles name no artifact they govern, and a term's use is recognized in prose rather than by an edge, so the in-force set at the scope is the deterministic, parse-free answer, and scoping bounds its size by pulling only the subset effective where the artifact lives.

Stopping at the corpus boundary is what keeps the closure finite and self-contained per corpus and keeps the method out of the consumer's job: the method says which set, the consumer decides whether an external reference is resolved, pinned, or materialized.
Defining the closure as a least fixed point, not a walk, is what makes it independent of traversal order and reconstructable from the files, the determinism [Method-defined deterministic context subset](../../requirements/system/deterministic-context-subset.md){id=note:req:kdtc9a8} obliges.
Versioning the rule is what lets the classification evolve without stranding the closures already taken under it.

## Relations

- satisfies: [Method-defined deterministic context subset](../../requirements/system/deterministic-context-subset.md){id=note:req:kdtc9a8}
- satisfies: [Self-contained extraction of inherited intent](../../requirements/stakeholder/self-contained-extraction.md){id=note:req:qq6eywy}
- decidedBy: [Method-defined context slice](../../decisions/method-defined-context-slice.md){id=note:dec:pk6jzwy}
