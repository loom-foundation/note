---
id: <namespace>:spec:<opaque>
name: <Name>
kind: specification
status: draft
authority:
  - contracts/integrations/<vendor>.openapi.yaml
---

This specification defines the wire contract and operational posture for the <Vendor> integration.

## Authority

The wire contract is expressed in OpenAPI 3.x (or AsyncAPI 3.x for webhook events) at the path given in `authority`.
That file governs on any divergence between it and this document.
An implementation's conformance to the contract is a separate Verification; it is not established here.

## Provider Details

```yaml
provider: <Vendor name>
purpose: <one-line statement of why this integration exists>
base_url: <https://api.vendor.example>
auth_method: <e.g. Bearer token, API key header, OAuth 2.0 client credentials>
rate_limit: <requests per window, e.g. 100 req/min>
declared_sla: <uptime or latency commitment the vendor publishes>
```

One row per provider; a second integration with the same vendor under a different base URL is a separate file.

## Operations Used

<!-- List only the operations the application calls; the OpenAPI contract holds the wire detail. -->

| Operation | Purpose |
|-----------|---------|
| <OperationId> | <why this operation is called> |

Add one row per operation declared in the authority contract that this integration exercises.

## Error Handling

<!-- Our Behaviour must state one of: retry, fallback, surface error, or fail silently. -->

| Provider Error | HTTP Status | Our Behaviour |
|----------------|-------------|---------------|
| <ErrorCode> | <4xx/5xx> | <retry \| fallback \| surface error \| fail silently> |

Omission of any known provider error code is a specification defect.
Where Our Behaviour is "surface error", name the application-level error id.

## Retry Strategy

```yaml
backoff: <e.g. exponential>
initial_delay_ms: <number>
max_delay_ms: <number>
max_attempts: <number>
jitter: <true | false>
retryable_statuses: [<429>, <503>]
```

State which HTTP status codes are considered transient and eligible for retry.

## Fallback Behaviour

<What the system does when the provider is unavailable or returns a non-retryable failure.>
Options include: serve cached data, return a degraded response, enqueue for later, or surface an error to the caller.
State the fallback in terms of observable system behavior, not implementation detail.

## Circuit Breaker

```yaml
failure_threshold: <number of failures before opening>
success_threshold: <number of successes to close from half-open>
timeout_ms: <time the breaker stays open before moving to half-open>
scope: <per-instance | global>
```

If no circuit breaker applies to this integration, replace this section with a one-line statement explaining why.

## Webhook Events

<!-- Conditional: include only when the provider delivers webhooks to this system. -->

| Event | Our Handler | Idempotency |
|-------|-------------|-------------|
| <event.name> | <handler identifier> | <key field or strategy> |

State the signature-verification method the handler applies; the security specification governs the key-management detail.

## Relations

- satisfies: [<Requirement>](../../requirements/system/<requirement>.md){id=<namespace>:req:<opaque>}
