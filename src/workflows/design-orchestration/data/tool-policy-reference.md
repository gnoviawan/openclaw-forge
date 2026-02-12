# Tool Policy Reference

Quick reference for sub-agent tool restrictions and sandbox configuration.

---

## Default Sub-Agent Tool Policy (Built-In)

Sub-agents get all tools EXCEPT:

| Denied by Default | Reason |
|-------------------|--------|
| `sessions_list` | Session management — main agent orchestrates |
| `sessions_history` | Session management — main agent orchestrates |
| `sessions_send` | Session management — main agent orchestrates |
| `sessions_spawn` | No nested spawning |
| `gateway` | System admin — dangerous from sub-agent |
| `agents_list` | System admin |
| `whatsapp_login` | Interactive setup |
| `session_status` | Scheduling — main agent coordinates |
| `cron` | Scheduling — main agent coordinates |
| `memory_search` | Pass info in spawn prompt instead |
| `memory_get` | Pass info in spawn prompt instead |

**Sub-agents CAN by default:** `read`, `write`, `edit`, `exec`, `apply_patch`, `browser`, `process`, and others.

---

## Per-Agent Tool Configuration

**Approach options:**
- **Allow-list** (restrictive): Only specify tools the agent CAN use
- **Deny-list** (permissive): Only specify tools the agent CANNOT use
- **Default** (no restrictions): Agent gets standard tool set

```json5
{
  agents: {
    list: [
      {
        id: "{agent-id}",
        tools: {
          allow: ["{tool1}", "{tool2}"],  // OR
          deny: ["{tool1}", "{tool2}"],
        },
      },
    ],
  },
}
```

---

## Global Sub-Agent Tool Overrides

```json5
{
  tools: {
    subagents: {
      tools: {
        deny: ["{additional-denied-tools}"],
        // OR restrict to only:
        allow: ["{only-these-tools}"],
      },
    },
  },
}
```

---

## Sandbox Configuration

**Modes:**
- `off` — No sandboxing (host access)
- `all` — Always sandboxed
- `auto` — Sandbox when conditions met

**Scope:**
- `agent` — One container per agent
- `shared` — All agents share one container

```json5
{
  agents: {
    list: [
      {
        id: "{agent-id}",
        sandbox: {
          mode: "all",
          scope: "agent",
          docker: {
            setupCommand: "apt-get update && apt-get install -y git",
          },
        },
      },
    ],
  },
}
```

---

## Sub-Agent Model Configuration

```json5
{
  agents: {
    defaults: {
      subagents: {
        model: "minimax/MiniMax-M2.1",
        thinking: "low",
        maxConcurrent: 8,
      },
    },
    list: [
      {
        id: "{agent-id}",
        subagents: {
          model: "anthropic/claude-sonnet-4",  // Per-agent override
        },
      },
    ],
  },
}
```
