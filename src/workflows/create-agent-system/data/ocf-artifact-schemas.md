# OCF Artifact Schemas

## SOUL.md Schema

```markdown
---
agent_name: '{agent-name}'
version: '1.0'
created: '{date}'
---

# {Agent Display Name} — Soul

## Identity

**Name:** {display name}
**Archetype:** {archetype/role metaphor}
**Core Purpose:** {one-sentence purpose}

## Persona

**Voice:** {communication style description}
**Tone:** {tone characteristics}
**Perspective:** {how this agent sees the world}

## Principles

1. {principle 1}
2. {principle 2}
3. {principle 3}

## Communication Style

**With Users:** {how agent communicates with end users}
**With Other Agents:** {how agent communicates with peer agents}
**Under Pressure:** {how agent behaves when facing errors or ambiguity}

## Boundaries

**Will:** {what this agent does}
**Won't:** {what this agent refuses to do}
**Defers To:** {which agents it delegates to and when}
```

## AGENTS.md Schema

```markdown
---
agent_name: '{agent-name}'
version: '1.0'
created: '{date}'
---

# {Agent Display Name} — Agent Definition

## Role

**Title:** {role title}
**Domain:** {area of expertise}
**Scope:** {what this agent is responsible for}

## Capabilities

- {capability 1}
- {capability 2}
- {capability N}

## Relationships

| Agent | Relationship | Interaction Pattern |
|-------|-------------|-------------------|
| {other-agent} | {relationship type} | {how they interact} |

## Boundaries

**Authorized Actions:** {what the agent can do autonomously}
**Requires Approval:** {what needs user confirmation}
**Escalation Path:** {when and how to escalate}
```

## USER.md Schema

```markdown
---
agent_name: '{agent-name}'
version: '1.0'
created: '{date}'
---

# {Agent Display Name} — User Context

## User Profile

**Expected Users:** {who will interact with this agent}
**User Expertise Level:** {novice/intermediate/expert}

## Context Sections

### {Context Category 1}
{placeholder for runtime user data}

### {Context Category 2}
{placeholder for runtime user data}

## Personalization

**Adapts To:** {what the agent personalizes based on user data}
**Remembers:** {what user context persists across sessions}
```

## MEMORY.md Schema

```markdown
---
agent_name: '{agent-name}'
version: '1.0'
created: '{date}'
---

# {Agent Display Name} — Memory

## Memory Categories

### Short-Term
- **Session Context:** {what to remember within a session}
- **Conversation History:** {how much context to maintain}

### Long-Term
- **User Preferences:** {what to persist across sessions}
- **Learned Patterns:** {what the agent learns over time}

## Retention Rules

| Category | Retention Period | Priority |
|----------|-----------------|----------|
| {category} | {duration} | {high/medium/low} |

## Context Management

**Max Context Window:** {token/message limits}
**Summarization Strategy:** {how to compress old context}
**Priority Ordering:** {what context is most important to keep}
```

## REVIEW.md Schema

```markdown
---
agent_name: '{agent-name}'
version: '1.0'
created: '{date}'
---

# {Agent Display Name} — Self-Correction

## Review Criteria

### Quality Gates
- {gate 1: what quality check to perform}
- {gate 2: what quality check to perform}

### Self-Assessment Checklist
- [ ] {check 1}
- [ ] {check 2}
- [ ] {check N}

## Error Detection

**Common Failure Modes:**
1. {failure mode} → {detection signal}
2. {failure mode} → {detection signal}

## Recovery Patterns

| Error Type | Detection | Recovery Action |
|------------|-----------|-----------------|
| {error} | {how detected} | {what to do} |

## Self-Correction Directives

- {directive 1: when X happens, do Y}
- {directive 2: if output lacks Z, regenerate with A}
```

## SKILL.md Schema

```markdown
---
skill_name: '{skill-name}'
agent_name: '{agent-name}'
version: '1.0'
created: '{date}'
---

# {Skill Display Name}

## Description
{what this skill does}

## Invocation
**Trigger:** {how this skill is activated}
**Channel:** {WhatsApp/Telegram/API/etc. if applicable}

## Gating Rules
- {rule 1: when this skill should/shouldn't activate}
- {rule 2: prerequisites or conditions}

## Parameters
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| {param} | {type} | {yes/no} | {description} |

## Output
**Format:** {what the skill produces}
**Destination:** {where output goes}
```

## openclaw.json Fragment Schema

```json
{
  "agent": "{agent-name}",
  "model": "{model-id}",
  "tools": {
    "allowed": ["{tool-1}", "{tool-2}"],
    "denied": ["{tool-3}"]
  },
  "memory": {
    "provider": "{memory-provider}",
    "config_ref": "./config/memory-config.json"
  },
  "permissions": {
    "file_read": true,
    "file_write": false,
    "web_access": false,
    "subprocess": false
  }
}
```

## System Config Schemas

### tool-policies.json
```json
{
  "policies": [
    {
      "agent": "{agent-name}",
      "allowed_tools": ["{tool}"],
      "denied_tools": ["{tool}"],
      "tool_approval_required": false
    }
  ]
}
```

### memory-config.json
```json
{
  "architecture": "{shared/isolated/hybrid}",
  "providers": [
    {
      "name": "{provider}",
      "type": "{vector/file/api}",
      "config": {}
    }
  ]
}
```

### failover-config.json
```json
{
  "agents": [
    {
      "agent": "{agent-name}",
      "fallback_agent": "{fallback-agent-name}",
      "max_retries": 3,
      "timeout_ms": 30000
    }
  ]
}
```

### heartbeat-config.json
```json
{
  "interval_ms": 60000,
  "agents": [
    {
      "agent": "{agent-name}",
      "health_check": "{check-type}",
      "alert_threshold": 3
    }
  ]
}
```

### logging-config.json
```json
{
  "level": "info",
  "agents": [
    {
      "agent": "{agent-name}",
      "level": "{debug/info/warn/error}",
      "destination": "{console/file/api}"
    }
  ]
}
```
