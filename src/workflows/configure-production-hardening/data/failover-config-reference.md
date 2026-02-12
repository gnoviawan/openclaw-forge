# Failover Configuration Reference

## Retry Policy Defaults

| Condition | Max Retries | Backoff |
|-----------|-------------|---------|
| Rate limit (429) | 3 | exponential |
| Server error (500+) | 2 | linear |
| Timeout | 1 | immediate failover |
| Auth error | 0 | fail immediately |

## Configuration Template

```json
// Model failover for {agent-name} (openclaw.json format)
// System cascades through fallbacks on failure
"model": {
  "primary": "{primary-model}",
  "fallbacks": ["{fallback-1}", "{fallback-2}"]
}
        timeout: {ms}
  contextOverflow:
    compactionThreshold: 0.8
    strategy: compact-then-truncate
    preserveOnCompaction:
      - tool-failures
      - file-operations
      - user-corrections
  retry:
    rateLimit:
      maxRetries: 3
      backoff: exponential
      initialDelay: 1000
    serverError:
      maxRetries: 2
      backoff: linear
      initialDelay: 2000
    timeout:
      maxRetries: 1
      action: failover
    authError:
      maxRetries: 0
      action: fail
```
