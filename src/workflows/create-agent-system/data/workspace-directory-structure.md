# OCF Workspace Directory Structure

## Standard Layout

```
{ocf_output_folder}/{system-name}/
├── agents/
│   ├── {agent-1-kebab-name}/
│   │   ├── AGENTS.md          # Role definition, capabilities, relationships
│   │   ├── SOUL.md            # Identity, persona, voice, principles
│   │   ├── USER.md            # User context templates
│   │   ├── MEMORY.md          # Memory categories, retention, context management
│   │   ├── REVIEW.md          # Self-correction, quality gates, error recovery
│   │   └── skills/
│   │       ├── {skill-1}.md   # Individual skill definitions
│   │       └── {skill-N}.md
│   ├── {agent-2-kebab-name}/
│   │   └── ... (same structure)
│   └── {agent-N-kebab-name}/
│       └── ... (same structure)
├── config/
│   ├── openclaw.json          # Combined agent configurations
│   ├── tool-policies.json     # Tool access policies per agent
│   ├── memory-config.json     # Memory architecture configuration
│   ├── failover-config.json   # Failover and retry configuration
│   ├── heartbeat-config.json  # Health monitoring configuration
│   └── logging-config.json    # Logging levels and destinations
└── workspace-plan.md          # Generation plan and progress tracking
```

## Naming Conventions

- **Agent folders:** kebab-case matching agent_name (e.g., `soul-smith`, `gear-wright`)
- **Skill files:** kebab-case matching skill_name (e.g., `analyze-code.md`, `generate-report.md`)
- **Config files:** kebab-case with `.json` extension
- **Artifact files:** UPPER-CASE with `.md` extension (AGENTS.md, SOUL.md, etc.)

## openclaw.json Structure

The combined `openclaw.json` aggregates all per-agent fragments into a single configuration file:

```json
{
  "system_name": "{system-name}",
  "version": "1.0",
  "created": "{date}",
  "agents": [
    {
      "agent": "{agent-name}",
      "path": "./agents/{agent-name}/",
      "model": "{model-id}",
      "tools": {},
      "memory": {},
      "permissions": {}
    }
  ],
  "system": {
    "tool_policies": "./config/tool-policies.json",
    "memory_config": "./config/memory-config.json",
    "failover_config": "./config/failover-config.json",
    "heartbeat_config": "./config/heartbeat-config.json",
    "logging_config": "./config/logging-config.json"
  }
}
```
