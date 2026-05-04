---
id: <namespace>:spec:<opaque>
name: <Name>
kind: specification
status: draft
authority: []
---

The target deployment topology for <system or scope>, covering services, external dependencies, and per-environment variations.

## Services

<!-- One subsection per owned service. All five fields are required; omit none. -->

### <service-name>

- **Runtime**: <language/runtime and version; container or serverless>
- **Dependencies**: <other services this service connects to, or "none">
- **Ports**: <port numbers and protocols exposed>
- **Health check**: <path and expected HTTP response status>
- **Environment variations**: <instance count, resource allocation, TLS termination, or other per-environment overrides; reference the Environment Variations section for the full table>

## External Dependencies

<!-- One row per dependency not owned by this project: managed databases, caches, object storage, CDNs, identity providers. Self-hosted entries must note that explicitly. -->

| Dependency | Type | Managed / Self-hosted | Consuming Services |
|------------|------|-----------------------|--------------------|
| <dependency name> | <database / cache / storage / CDN / IdP / other> | <managed by provider / self-hosted> | <service-name, ...> |

## Environment Variations

<!-- One row per environment the project operates. Scale, access controls, feature flags, and backup policies are typical axes; add columns as needed. At minimum: development, staging, production. -->

| Environment | Scale | Access Controls | Backup Policy | Notes |
|-------------|-------|-----------------|---------------|-------|
| development | <instance counts or resource sizes> | <access restrictions> | <backup schedule or "none"> | <any deviations from baseline> |
| staging | <instance counts or resource sizes> | <access restrictions> | <backup schedule or "none"> | <any deviations from baseline> |
| production | <instance counts or resource sizes> | <access restrictions> | <backup schedule> | <any deviations from baseline> |

## Topology Diagram

<!-- A Mermaid flowchart or graph diagram. Services are nodes; connections are directed edges. Use subgraphs for environment boundaries where relevant. The diagram is derived from the sections above; keep it consistent with them. -->

```mermaid
flowchart TD
    subgraph <environment>
        <service-a>[<service-name>] --> <service-b>[<service-name>]
        <service-a> --> <external-dep>[<dependency-name>]
    end
```

## Relations

- satisfies: [<Requirement>](../../requirements/system/<requirement>.md){id=<namespace>:req:<opaque>}
