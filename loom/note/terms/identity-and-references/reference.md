---
id: note:term:evt67dx
name: Reference
kind: term
status: current
---

A relative navigation link carrying the target's Durable Identifier as its load-bearing part, with the target's current name as the visible link text.

The Durable Identifier is what makes the reference durable: it resolves after the target moves or is renamed, and it crosses repository boundaries without loss of identity.
The navigation path is a convenience for editors and readers; a tool re-points it after a move.
The visible link text is the target's current name (its designation); after a rename the text may drift before the next refresh, but nothing breaks, because the id is the citation.
A reference never targets an alias; an alias is for lookup and display only.

## Inclusion test

Does it carry both a navigable link and the target's Durable Identifier?

A bare path with no identifier is not a Reference; it shatters on refactor.
A raw id with no navigable link is a citation token, not a Reference.

## Origin

Oxford: "the action of mentioning or alluding to something", and "a mention of a source of information in a book or article".
The term is standard in computing and documentation, where a reference is an indirection that names another element so it can be located and resolved (a citation, a cross-reference, a pointer or hyperlink).

This corpus pairs the navigable link with a Durable Identifier so the reference resolves even after the target moves, and keeps the visible text as the target's name rather than a frozen label that can silently become stale.
