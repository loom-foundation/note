---
id: <namespace>:spec:<opaque>
name: <Name>
kind: specification
status: draft
authority: []
---

This specification states the cross-cutting operational policies for <system or service name>.

## Logging

<Log format (structured JSON is conventional; deviation requires explicit rationale).>

Required fields on every log entry:

```yaml
# List the required fields and their types.
# Example fields: timestamp (ISO 8601), level, service, trace_id, message.
# Cite OpenTelemetry semantic conventions by name for field naming conventions.
```

<One sentence on rules for sensitive data (PII, credentials, tokens): what is redacted, masked, or omitted.>

Severity level mapping:

| Level | Condition |
|---|---|
| `<level>` | `<condition>` |

## Retry and Backoff

<Default backoff algorithm and its parameters (initial delay, multiplier, maximum attempts, jitter).>

Retryable conditions:

| Condition | Retryable |
|---|---|
| `<condition>` | `<yes / no>` |

<Circuit breaker behavior: threshold, half-open probe interval, and reset condition.>

## Caching

<HTTP caching header policy per response type.
Cite RFC 9111 (HTTP Caching) by name as the governing standard for Cache-Control semantics.>

| Response type | Cache-Control value | Rationale |
|---|---|---|
| `<type>` | `<directive>` | `<one line>` |

<Application-layer caching rules: what is cached, for how long, and in what store.>

<Cache invalidation strategy: event-driven, TTL-only, or explicit purge; and what triggers invalidation.>

## Health Checks

Liveness endpoint:

```yaml
path: <e.g. /healthz>
method: GET
checks: <what it verifies (process alive, not deadlocked)>
success_status: 200
```

Readiness endpoint:

```yaml
path: <e.g. /readyz>
method: GET
checks: <what it verifies (dependencies reachable, warm)>
success_status: 200
```

Response shape (both endpoints):

```yaml
# Define the shared response schema here.
# Example fields: status (ok | degraded | down), version, checks map.
```

## Graceful Shutdown

Shutdown sequence on termination signal:

```yaml
# Ordered steps, e.g.:
# 1. Stop accepting new requests.
# 2. Drain the in-flight request queue.
# 3. Close outbound connections.
# 4. Flush log buffers and exit.
```

<In-flight request timeout: maximum duration to wait before forceful termination.>

Exit code semantics:

| Code | Meaning |
|---|---|
| `0` | <clean shutdown> |
| `<n>` | <error condition> |

## Rate Limiting

<Scope: per user, per IP, per endpoint group, or a combination.>

Response when limit is exceeded:

```yaml
status: 429
headers:
  # Cite the IETF RateLimit header draft (draft-ietf-httpapi-ratelimit-headers)
  # by name for header naming conventions.
  RateLimit-Limit: <quota ceiling>
  RateLimit-Remaining: <remaining quota>
  RateLimit-Reset: <reset timestamp or seconds>
  Retry-After: <seconds>
```

<Any endpoint groups that carry a different limit from the system default.>

## Relations

- satisfies: [<Requirement>](../../requirements/system/<requirement>.md){id=<namespace>:req:<opaque>}
