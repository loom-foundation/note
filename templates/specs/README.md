# Specification format templates

Optional, copy-paste starting points for authoring a Specification in a common software domain.
Each is a scaffold, not an artifact: you copy a domain's template into your corpus under `loom/note/specifications/<domain>/`, fill it in, and mint an id for it.
They are authored, not generated, unlike the per-kind templates ([Kind templates](../../loom/note/decisions/kind-templates.md){id=note:dec:vg3k34n}), and they are a software-oriented convenience, not part of the universal method: an effort whose specifications describe a hardware product, a process, or a methodology ignores this directory and writes its own.

Templates are grouped into families; `software/` is the first.

## The two-tier authority model

A Specification declares the external authority its design answers to in its `authority` frontmatter field ([Independent authority on specifications](../../loom/note/decisions/specification-authority.md){id=note:dec:av7k3mq}).
Two tiers follow:

- **Independently validated** (`authority` non-empty): the design answers to an external authority Note did not author, a machine-readable contract (OpenAPI, JSON Schema, an OpenFGA model) or a completeness standard it is checked against (OWASP ASVS, a control catalogue). The external file stays untouched and governs; the Markdown never restates its content.
- **Review-gated** (`authority: []`): no external authority fixes the content, so the design is a commitment checked by review, a weaker control stated plainly. The Markdown is the source of truth. Where a standard informs the design, cite it by name; it guides, it does not govern.

Prefer a stable authority. A governance-soft format (an unratified or pre-release spec) is better generated as a derived export than pointed at as the authority.

## The three forms

Every specification takes one of three forms, read off its `authority` field rather than declared.
They are a lens for thinking about a spec, not a kind and not a template of their own:

- **Contract**: an external contract holds the whole design (an HTTP API answers to OpenAPI). The Markdown is a thin attachment, the id and relations and rationale and the `authority` pointer, restating nothing.
- **House**: no external format fits, so the structured Markdown is the source (`authority: []`), a security posture or an operational policy.
- **Split**: an external contract holds part and irreducible policy holds the rest (an integration's wire answers to OpenAPI; its retry and fallback policy does not). The `authority` points at the contract; a `## Posture` section carries the policy.

The domain templates below each embody one of these forms with that domain's real structure.

## The software domain catalogue

| Domain | Form | Authority |
|---|---|---|
| api | contract | OpenAPI 3.1 |
| schemas | contract | JSON Schema 2020-12 |
| config | contract | JSON Schema, with a derived table |
| errors | contract | JSON Schema, RFC 9457 envelope |
| events | contract | AsyncAPI 3.x |
| features | contract | Gherkin |
| database | contract | ANSI / PostgreSQL DDL |
| state-machines | contract | YAML state machine |
| authz | split | OpenFGA model (relations) and house (RBAC matrix) |
| integrations | split | OpenAPI / AsyncAPI (wire) and posture (retry, fallback) |
| nfr | split | OpenSLO (SLIs/SLOs, opt-in) and posture (degradation) |
| design | split | W3C Design Tokens (values, opt-in) and house (roles) |
| security | house | cite OWASP ASVS; OSCAL when a framework binds |
| privacy | house | cite ISO 27560 for consent records; OSCAL when a framework binds |
| identity | house | cite NIST SP 800-63A; OIDC4IDA vocabulary |
| authn | house | cite NIST SP 800-63B and the protocol RFCs |
| operations | house | cite RFC 9111, OpenTelemetry, the RateLimit header draft |
| infra | house | topology is house-prose; IaC is implementation, not the spec |
| ui | house | MDX; no cross-framework screen contract exists |
| cli | house | JSON Schema for the `--json` output; the rest is house-prose |

To start, copy `software/<domain>.md` for your domain, replace the placeholders, point `authority` at your contract file (or leave it `[]`), and mint an id.
OpenSLO, W3C Design Tokens, and OpenCLI are governance-soft as of this writing; treat them as opt-in derived exports rather than authorities the spec answers to until they ratify.
