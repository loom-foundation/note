The lifecycle records an artifact's maturity in the `status` field, so a reader can tell whether the content can be relied on without reading the body (the obligation is the legible-lifecycle requirement).

The ladder states run from least to most settled (`tbd`, `draft`, `current`), then reach one of two terminal states: `obsolete`, content that was operative and is now retired, and `rejected`, an authored proposal that was deliberately declined and kept as a record, the lifecycle analogue of Validation's `invalidated`.

The well-formed transitions between the states, and any check over them, are a specification concern.
