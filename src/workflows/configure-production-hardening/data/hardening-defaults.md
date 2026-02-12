# Production Hardening Defaults & Best Practices

Reference data for the configure-production-hardening workflow. These defaults reflect OpenClaw's configuration schemas, runtime behavior, and best practices.

---

## Memory Backend Defaults

### Architecture

OpenClaw uses a hybrid RAG memory system with both vector and full-text search. Configuration lives in the `memory` section of `openclaw.json`.

### Backend Options

| Backend | Use Case | Auto-Recall | Auto-Capture |
|---------|----------|-------------|--------------|
| builtin | Default SQLite-based vector + FTS5, suitable for most workspaces | yes | yes |
| lancedb | LanceDB plugin for larger-scale vector search | yes | yes |
| qmd | QMD plugin for specialized retrieval | yes | yes |
| (disabled) | Stateless agents, no persistence needed | no | no |

### Actual Configuration Format (from Zod schema)

```json
"memory": {
  "backend": "builtin",
  "autoCapture": true,
  "autoRecall": true,
  "embedding": {
    "provider": "openai",
    "model": "text-embedding-3-small"
  }
}
```

### Per-Agent Memory Patterns

| Agent Role | Recommended Backend | Auto-Recall | Auto-Capture | Notes |
|------------|-------------------|-------------|--------------|-------|
| Triage/Router | builtin | true | true | Needs session context for routing accuracy |
| Specialist | builtin | true | true | Benefits from recalling past resolutions |
| Assistant | builtin | true | true | Full memory for personalized interactions |
| Monitor/Observer | builtin | true | false | Recalls context but doesn't capture noise |
| Stateless Tool | (disabled) | false | false | No persistence needed |

### Workspace Artifacts for Memory

- **`MEMORY.md`** — Long-term curated storage. Agents distill daily logs into curated wisdom here
- **`memory/YYYY-MM-DD.md`** — Daily logs (raw append-only)
- **`USER.md`** — User profile with structured data (name, timezone) and unstructured context

### Embedding Model Token Limits

The embedding model has a token limit that is enforced automatically to prevent overflow. Very long single messages may be chunked for embedding.

---

## Tool Policy Defaults

### Architecture

Tool policies use a "Profile + Exception" model. Policies support inheritance: Global → Group → Agent. Subagents get automatically restricted policies.

### Pre-defined Profiles

| Profile | Description | Includes |
|---------|-------------|----------|
| minimal | Bare minimum tools | Basic read, search |
| coding | Development-focused | File read/write, shell (restricted), search |
| messaging | Communication-focused | Channel send, user lookup, search |
| full | All tools available | Everything except dangerous |

### Actual Configuration Format (from Zod schema)

```json
"tools": {
  "profile": "minimal",
  "allow": ["camera.*"],
  "deny": ["shell.exec"],
  "alsoAllow": ["weather"]
}
```

- `profile` — base permission set
- `allow` — explicit allows (overrides profile denials)
- `deny` — explicit denies (highest priority, overrides everything)
- `alsoAllow` — additive permissions on top of profile

### Risk Tiers (Recommended Framework)

| Tier | Tools | Default Policy |
|------|-------|---------------|
| Safe | read, search, browse, calculate | allow-all |
| Moderate | write-file, api-call, database-read | allow-with-logging |
| Sensitive | shell-exec, database-write, email-send | deny-unless-explicit |
| Dangerous | system-admin, credential-access, network-scan | deny-always |

### Per-Role Recommended Profiles

| Agent Role | Profile | Additional Allow | Deny |
|------------|---------|-----------------|------|
| Triage/Router | minimal | channel routing | shell.*, write-file |
| Specialist | coding or messaging | domain-specific tools | system-admin, credential-access |
| Assistant | full | — | shell.exec (unless needed) |
| Admin Agent | full | — | — |
| Subagent | minimal | — | shell.*, write-file (outside output), credential-access |

### Subagent Restrictions

Subagents spawned via `spawn()` automatically receive restricted tool policies:
- No shell execution
- No file write outside designated output folders
- No credential or secret access
- Read-only database access at most
- Can be further scoped by parent agent's `tools.byProvider` config

### Approval Gates

For sensitive operations, OpenClaw supports approval gates:
```json
"approvals": {
  "required": ["shell.exec", "file.write"],
  "elevatedAllowFrom": ["admin-user-id"]
}
```

---

## Failover Chain Defaults

### Architecture

Model redundancy is configured per-agent in the `model` section. The system attempts the primary model first; on failure (API error, rate limit, timeout), it cascades through the fallbacks array sequentially.

### Actual Configuration Format

```json
"model": {
  "primary": "claude-sonnet-4-20250514",
  "fallbacks": ["gpt-4o", "claude-haiku-4-20250514"]
}
```

### Recommended Fallback Chains

**For primary agents (complex tasks):**
1. claude-sonnet-4-20250514 (timeout: 30s)
2. gpt-4o (timeout: 30s)
3. claude-haiku-4-20250514 (timeout: 15s)

**For lightweight tasks (subagents, simple operations):**
1. claude-haiku-4-20250514 (timeout: 15s)
2. gpt-4o-mini (timeout: 15s)

**For local-first setups:**
1. local-llama-3 (timeout: 60s)
2. claude-haiku-4-20250514 (timeout: 15s)

### Context Overflow Handling (Compaction Safeguard)

The compaction system automatically summarizes conversation history when context limits are reached. **Smart Retention** preserves critical data even during compaction:

| Preserved During Compaction | Why |
|---------------------------|-----|
| Tool failure logs | Agent must not lose track of recent errors |
| File operation summaries | Agent must know what files were changed |
| User corrections | Agent must remember what it got wrong |

| Strategy | When | Action |
|----------|------|--------|
| compaction | context > 80% limit | Summarize older messages with smart retention |
| truncation | compaction insufficient | Drop oldest messages beyond summary |
| escalation | repeated overflow | Alert user, suggest session reset |

### Retry Policy

| Condition | Max Retries | Backoff |
|-----------|-------------|---------|
| Rate limit (429) | 3 | exponential (1s, 2s, 4s) |
| Server error (500+) | 2 | linear (2s, 4s) |
| Timeout | 1 | immediate failover to next in chain |
| Auth error (401/403) | 0 | fail immediately |

---

## Observability Defaults

### Heartbeat Architecture

Heartbeats are cron-style proactive triggers. The runtime:
- Injects current time into prompts
- Respects `activeHours` and `timezone` to prevent waking agents at inappropriate times
- Deduplicates identical heartbeat outputs to prevent nagging
- Agent must read `HEARTBEAT.md` (if present) and reply `HEARTBEAT_OK` if no action needed

### Actual Configuration Format

```json
"heartbeat": {
  "every": "1h",
  "activeHours": {
    "start": "09:00",
    "end": "17:00",
    "timezone": "America/New_York"
  },
  "prompt": "Check in: review pending tasks, surface anything that needs attention"
}
```

Supports time units: `ms`, `s`, `m`, `h`

### Per-Role Heartbeat Patterns

| Agent Type | Frequency | Active Hours | Prompt Pattern |
|------------|-----------|-------------|----------------|
| Monitor | 30m | 24/7 | "Check system status, report anomalies" |
| Assistant | 1h | business hours | "Review pending tasks, surface needs" |
| Batch Worker | 4h | off-peak | "Process queued items" |
| Passive | none | n/a | No heartbeat needed |

### Logging Configuration

OpenClaw logging format:

```json
"logging": {
  "level": "info",
  "consoleStyle": "pretty",
  "redactSensitive": "tools",
  "file": "/var/log/openclaw.log"
}
```

- `consoleStyle`: `"pretty"` (human-readable) or `"json"` (machine-parseable)
- `redactSensitive`: `"tools"` redacts tool inputs/outputs containing secrets

| Level | What Gets Logged | When |
|-------|-----------------|------|
| fatal | Unrecoverable errors | always |
| error | Tool failures, API errors, crashes | always |
| warn | Rate limits, fallbacks triggered, unusual patterns | always |
| info | Session starts/ends, tool calls, agent handoffs | production |
| debug | Full prompts, responses, memory operations | development only |
| trace | Token counts, latency, internal state | development only |

---

## Self-Correction Defaults

### Architecture

Self-correction in OpenClaw is a behavioral pattern defined in workspace artifacts, not hardcoded runtime logic. Agents follow directives from `AGENTS.md` and `SOUL.md`.

### Memory-Based Self-Correction

The journaling pattern uses workspace artifacts:
1. **Daily logs**: `memory/YYYY-MM-DD.md` — raw append-only session logs
2. **Curated memory**: `MEMORY.md` — distilled insights from daily logs
3. **Directives**: `AGENTS.md` — operational rules including self-correction

### Error Journaling Directives

Add to each agent's `AGENTS.md`:

```markdown
## Self-Correction Protocol

### Error Journal
- When a tool fails: log the error, the attempted action, and the context
- When a user corrects you: log the correction, what you got wrong, and why
- When you detect an issue: log the issue, your reasoning, and the fix
- Review error patterns at each session start

### Learning Loop
- Check memory/YYYY-MM-DD.md at session start for recent errors
- Look for recurring patterns across sessions
- Adjust behavior based on past mistakes
- Reference past corrections in similar situations
```

### Pre-Response Checks (Directive-Based)

| Check | Description | Action on Fail |
|-------|-------------|----------------|
| boundary-scan | Verify response doesn't violate SOUL.md boundaries | suppress + rephrase |
| tone-check | Verify response matches SOUL.md persona tone | soft-correct |
| factuality | Flag claims that might be fabricated | add disclaimer |
| scope-check | Verify response stays within agent's domain per AGENTS.md | redirect to appropriate agent |

### Feedback Capture

| Trigger | Capture | Storage |
|---------|---------|---------|
| User says "that's wrong" | Correction + context | memory/YYYY-MM-DD.md |
| Tool returns error | Error + attempted action | memory/YYYY-MM-DD.md |
| Agent self-detects issue | Issue + reasoning | memory/YYYY-MM-DD.md |
| User explicit feedback | Rating + comments | MEMORY.md |

---

## Boundary Rule Defaults

### Architecture

Boundaries are enforced at two levels in OpenClaw:
1. **Soft (Prompt-based)**: Defined in `SOUL.md` — "Core Truths", "Boundaries", and "Vibe"
2. **Hard (Runtime-based)**: Docker sandboxing, approval gates, privilege scoping

### Soft Boundaries (SOUL.md Directives)

Add to each agent's `SOUL.md`:

```markdown
## Boundaries
- Private things stay private
- Ask before acting externally
- Stay within your domain
- Escalate when uncertain
- Never repeat credentials or secrets
```

### Hard Boundaries (Runtime Configuration)

**Sandboxing:**
```json
"sandbox": {
  "enabled": true,
  "runtime": "docker",
  "restrictions": {
    "network": "limited",
    "filesystem": "read-only-except-output"
  }
}
```

**Approval Gates:**
```json
"approvals": {
  "required": ["shell.exec", "file.write"],
  "elevatedAllowFrom": ["admin-user-id"]
}
```

### Privacy Rules

| Rule | Description | Default |
|------|-------------|---------|
| no-pii-storage | Don't store PII in logs (use redactSensitive) | enabled |
| no-credential-echo | Never repeat credentials, API keys, or passwords | enabled |
| session-data-only | Only access current session data unless memory loaded | enabled |
| user-data-scope | Only access data user explicitly shared | enabled |

### Escalation Triggers

| Trigger | Condition | Action |
|---------|-----------|--------|
| confidence-low | Agent confidence below threshold | flag for human review |
| out-of-scope | Request outside agent's domain | hand off to appropriate agent |
| safety-concern | Content triggers safety filters | escalate to human |
| repeated-failure | Same error 3+ times | escalate to human |
| user-request | User explicitly asks for human | immediate handoff |

### Data Handling Policies

| Policy | Description | Default |
|--------|-------------|---------|
| input-sanitization | Sanitize user inputs before processing | enabled |
| output-filtering | Filter outputs via redactSensitive | enabled |
| audit-trail | Logging with structured output | enabled for production |
| data-retention | Auto-purge session data after retention period | 30 days |

---

## Security Scanner Rules

These rules are enforced at runtime on all skill code:

### Critical Rules (Block Execution)

| Rule | Detects | Severity |
|------|---------|----------|
| dangerous-exec | Usage of `child_process` (exec, spawn) | critical |
| dynamic-code-execution | `eval()` or `new Function()` | critical |
| env-harvesting | `process.env` access + network calls in same file | critical |
| crypto-mining | Patterns matching mining pools/libraries | critical |

### Warning Rules

| Rule | Detects | Severity |
|------|---------|----------|
| suspicious-network | WebSockets on non-standard ports | warning |
| potential-exfiltration | File read + network send in same context | warning |

All skills must pass the security scanner before execution. Configure tool policies to restrict which agents can load custom skills.
