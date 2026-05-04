---
id: note:dec:gh7mhc4
name: Archive and retention
kind: decision
status: current
decided: 2026-06-12T00:00:00Z
---

A terminal artifact, one whose status is `obsolete` or `rejected`, lives under a single visible **`archive/`** directory at each layer root, mirroring the kind tree beneath it (`archive/decisions/...`, `archive/requirements/system/...`).
Status stays authoritative for whether an artifact is terminal; placement under `archive/` is the derived, checker-synced convenience, and a tool may report or perform the move.
On a filename clash inside `archive/<kind>/`, the colliding file's opaque id is suffixed; a retired artifact may be shrunk to a tombstone (its lead plus pointers).
Deletion stays narrow and adopter-gated for a live corpus: the default is to retain, because citations held in immutable surfaces still resolve and the audit record survives.

## Context

A sustained body of work, whether a software system, a hardware product, a process, or a methodology like this corpus, accumulates terminal artifacts over time: obligations retired as the work changed, designs declined and kept as a record.
The lifecycle already names these two terminal states, `obsolete` for content that was operative and is retired, and `rejected` for a proposal that was weighed and declined.
What that lifecycle leaves open is where a terminal artifact sits in the tree, and whether it is ever deleted.

Volume forces the placement question.
A live corpus left to mix terminal artifacts among current ones makes the working set harder to read: a reviewer scanning `decisions/` reads past retired and declined records to find the live ones.
Three layouts fail.
A flat archive invites filename collisions and is hard to navigate.
A per-kind subdirectory such as `decisions/archive/` collides with group semantics, where a kind's subdirectories already mean topical groups.
A hidden, dot-prefixed file is not hidden on every platform, confuses tooling, and churns every filename on retirement.

The corpus already holds a structural precedent for a content-named subtree that sits outside the kind tree: the **`materialized/`** subtree, a non-kind directory at the corpus root for a special class of artifacts (a frozen, severed snapshot of resolved intent).
An archive is the same shape of thing, a content-named subtree for a class of artifacts the kind tree does not otherwise place, so it follows that precedent rather than inventing a new layout.

## Decision

- **One visible `archive/` per layer root, mirroring the kind tree.**
  Each layer root carries a single `archive/` directory, and beneath it the kind tree is mirrored: a retired decision sits at `archive/decisions/...`, a retired system requirement at `archive/requirements/system/...`, and so on.
  Navigation under `archive/` is isomorphic to the live tree, so a reader who knows where an artifact lived knows where its archived form sits.

- **Status is authoritative; placement is the derived mirror.**
  Whether an artifact is terminal is read from its `status` field, never from its location.
  Placement under `archive/` is a derived convenience the checker keeps in sync with status: a tool may report an artifact whose placement and status disagree, and may perform the move that reconciles them.
  Location never overrides status, consistent with the corpus's standing rule that the file's frontmatter, not its path, carries the load-bearing fact.

- **A filename clash suffixes the opaque id.**
  On the rare clash inside `archive/<kind>/`, where two artifacts archived under the same kind would share a filename, the colliding file's name is suffixed with its opaque id.
  The id is already unique and already the identity, so the suffix disambiguates without inventing a new key.

- **Tombstone shrinking is permitted.**
  A retired artifact may be reduced to a tombstone: its lead plus pointers (to a successor, to the decision that retired it), with the rest of the body dropped.
  This is permitted, not required; a corpus that wants the full retired text keeps it, and one that wants only the trail shrinks it.

- **The archive is not hidden.**
  Archives are part of the record, discoverable by inspecting the tree, so the `archive/` directory is visible.
  Hidden directories stay reserved for tool exhaust, the generated, derived, or cache content a tool writes and no reader authors; a record a reader may need to consult is never filed there.

- **Retention is the default; deletion is narrow and adopter-gated.**
  For a live corpus, the default is to retain a terminal artifact, archived, rather than delete it.
  Deletion is a narrow, adopter-gated act: an adopter's Orchestrating Authority may permit it for cause, but the method does not delete by default.

## Forces and trade-offs

A single visible `archive/` per layer costs one directory entry at each layer root and asks a reader to recognize that the subtree holds the retired record, not the live working set.
That cost buys a clean working set: the live kind directories hold only current and in-progress artifacts, and the retired record is one navigable, isomorphic subtree away rather than interleaved with the live work.

Keeping status authoritative and placement derived, rather than letting the directory define the terminal state, preserves the corpus's location-independence: a move never changes what an artifact is, and a tool reconciles placement to status rather than the reverse.
The cost is that placement and status can momentarily disagree (an artifact marked terminal but not yet moved); the checker reports the gap, and the move is mechanical.

Retaining terminal artifacts by default, rather than deleting them, leaves more in the tree for a reader to recognize as off the live set.
That cost is paid against two benefits that deletion forfeits: a citation of the artifact held in an immutable surface, a commit trailer or a code comment, still resolves to a real file rather than dangling, and the audit record of what was once operative or once proposed survives in the corpus rather than only in version-control history a reader must know to excavate.
Deletion remains available where an adopter has cause and authority, but it is the exception the adopter gates, not the default the method takes.

## Alternatives considered

- **A flat `archive/` directory with no kind structure.**
  Rejected: it invites filename collisions across kinds and is hard to navigate, losing the isomorphism with the live tree that lets a reader find a retired artifact where its live form sat.

- **A per-kind `decisions/archive/` subdirectory under each kind.**
  Rejected: a kind's subdirectories already carry group semantics (a subdirectory is a topical group), so an `archive/` subdirectory under a kind collides with that meaning; the single archive subtree at the layer root keeps the two apart.

- **A hidden, dot-prefixed archive or hidden retired files.**
  Rejected: dot-prefixing is not hidden on every platform, confuses tooling, and churns every filename on retirement; and an archive is part of the record, so it belongs in the visible tree, with hidden directories reserved for tool exhaust.

- **Delete every terminal artifact and rely on version-control history.**
  Rejected as the default for a live corpus: deletion dangles any citation held in an immutable surface and removes the audit record from the live tree, leaving it recoverable only by a reader who already knows to look in history; retention with archiving keeps both intact, and deletion stays available as a narrow, adopter-gated exception.

## Driven by

- groundedIn: [Single Source of Truth](../principles/single-source-of-truth.md){id=note:principle:8691937}
- groundedIn: [Compute and Report](../principles/compute-and-report.md){id=note:principle:6e7f28k}
- groundedIn: [Earned Substance](../principles/earned-substance.md){id=note:principle:yecemfe}
- groundedIn: [Universal artifact lifecycle and its transitions](artifact-lifecycle.md){id=note:dec:gfwq0mv}
