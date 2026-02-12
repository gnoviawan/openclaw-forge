# Workspace Validation Rules

Reference data for the validate-workspace workflow. These rules define what constitutes a valid, consistent, and hardened OpenClaw workspace.

---

## Structural Checks

### Required Files

| File | Severity | Rule |
|------|----------|------|
| SOUL.md | FAIL | Must exist and be non-empty. Defines agent personality and boundaries. |
| AGENTS.md | FAIL | Must exist and be non-empty. Defines agent operational procedures. |
| USER.md | FAIL | Must exist. Defines the user the agent serves. |
| IDENTITY.md | WARN | Should exist. Defines agent name, emoji, and identity. If absent, check SOUL.md for identity section. |

### Optional Files (warn if missing)

| File | Severity | Rule |
|------|----------|------|
| TOOLS.md | WARN | Should exist if agent uses tools. User-maintained tool usage notes. |
| HEARTBEAT.md | WARN | Should exist if heartbeat is configured. Checklist of proactive tasks. |
| MEMORY.md | WARN | Should exist if memory backend is enabled. Long-term curated storage. |

### Files That Should NOT Exist

| File | Severity | Rule |
|------|----------|------|
| BOOTSTRAP.md | WARN | Should NOT exist in a fully initialized workspace. Should be deleted after first run. |

### Required Directories

| Directory | Severity | Rule |
|-----------|----------|------|
| memory/ | WARN | Should exist for daily logs (memory/YYYY-MM-DD.md). |

### Optional Directories

| Directory | Severity | Rule |
|-----------|----------|------|
| skills/ | WARN | Should exist if AGENTS.md or TOOLS.md references skills. |

### Well-Formedness

| Check | Severity | Rule |
|-------|----------|------|
| SOUL.md has ## sections | WARN | Should have structured sections (Core Truths, Boundaries, Vibe, Continuity). |
| AGENTS.md has ## sections | WARN | Should have structured sections (First Run, Every Session, Memory, Safety, Tools). |
| USER.md is non-empty | WARN | Should contain at minimum the user's name or preferences. |

---

## Coherence Checks

### Personality-Directive Consistency

| Check | Severity | Rule |
|-------|----------|------|
| SOUL.md has Boundaries section | FAIL | Boundaries section must be present and non-empty. |
| SOUL.md tone is consistent | WARN | The personality tone in SOUL.md should not contradict AGENTS.md directives. Check for conflicting instructions (e.g., "be bold" in SOUL vs "always ask permission" in AGENTS). |

### Session Startup References

| Check | Severity | Rule |
|-------|----------|------|
| AGENTS.md references SOUL.md | FAIL | Session startup sequence must instruct agent to read SOUL.md. |
| AGENTS.md references USER.md | FAIL | Session startup sequence must instruct agent to read USER.md. |
| AGENTS.md references memory files | FAIL | Session startup sequence must instruct agent to read memory/YYYY-MM-DD.md or similar. |
| AGENTS.md references MEMORY.md | WARN | Should instruct agent to read MEMORY.md in main sessions. |

### Skill References

| Check | Severity | Rule |
|-------|----------|------|
| Referenced skills exist | FAIL | All skills mentioned in AGENTS.md or TOOLS.md must have corresponding SKILL.md files in skills/ directories. |
| No orphan skill directories | WARN | Skill directories should be referenced somewhere in workspace files. |

### Identity Consistency

| Check | Severity | Rule |
|-------|----------|------|
| IDENTITY.md matches SOUL.md | WARN | If both exist, the agent name in IDENTITY.md should be consistent with any name references in SOUL.md. |

### Binding Completeness

| Check | Severity | Rule |
|-------|----------|------|
| Bindings are complete | WARN | If openclaw.json exists and has bindings referencing this workspace's agent, each binding should have a channel and target (accountId or peer). |

---

## Hardening Checks

### Memory Directives

| Check | Severity | Rule |
|-------|----------|------|
| Daily log directive | FAIL | AGENTS.md must contain directives about daily logs (memory/YYYY-MM-DD.md). |
| Long-term memory directive | FAIL | AGENTS.md must contain directives about MEMORY.md for long-term storage. |
| Write-it-down rule | WARN | AGENTS.md should contain the "write it down / no mental notes" directive or equivalent. |

### Memory Backend

| Check | Severity | Rule |
|-------|----------|------|
| Backend configured | WARN | If openclaw.json exists, memory backend should be configured (or explicitly disabled with justification). |

### Tool Policies

| Check | Severity | Rule |
|-------|----------|------|
| Tool profile or policies defined | WARN | If openclaw.json exists, tools section should have a profile set or explicit allow/deny rules. |

### Boundaries

| Check | Severity | Rule |
|-------|----------|------|
| Privacy boundaries | FAIL | SOUL.md Boundaries section must address privacy (e.g., "Private things stay private"). |
| External action rules | FAIL | SOUL.md or AGENTS.md must have rules about external actions (ask before sending emails, etc.). |
| Scope limits | WARN | SOUL.md or AGENTS.md should define the agent's domain scope. |

### Failover

| Check | Severity | Rule |
|-------|----------|------|
| Failover chain | WARN | If openclaw.json exists and agent is customer-facing, model.fallbacks should be defined. |

### Self-Correction

| Check | Severity | Rule |
|-------|----------|------|
| Error journaling | WARN | AGENTS.md should contain directives about logging errors and corrections to memory. |
| Learning loop | WARN | AGENTS.md should contain directives about reviewing past mistakes. |

### Safety

| Check | Severity | Rule |
|-------|----------|------|
| No-exfiltration rule | FAIL | AGENTS.md must contain a directive against exfiltrating private data. |
| Destructive command warning | WARN | AGENTS.md should contain guidance about destructive commands (prefer trash over rm, ask before destructive operations). |

### Group Chat Behavior

| Check | Severity | Rule |
|-------|----------|------|
| Group chat rules | WARN | If agent is bound to group channels, AGENTS.md should define when to speak vs stay silent. |
