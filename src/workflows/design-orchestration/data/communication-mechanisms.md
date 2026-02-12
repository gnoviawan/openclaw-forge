# Communication Mechanisms Reference

Quick reference for spawn vs send decisions during orchestration design.

---

## sessions_spawn (Sub-Agents)

- Creates an isolated background session
- Non-blocking — main agent continues working
- Sub-agent announces results back when done
- Best for: Task delegation, background research, parallel work
- Limitation: Sub-agents CANNOT spawn their own sub-agents (no nesting)
- Limitation: Sub-agents have restricted tool access by default

## sessions_send (Agent-to-Agent Messaging)

- Sends a message into another agent's session
- Can be sync (wait for reply) or fire-and-forget
- Supports reply ping-pong (up to 5 rounds)
- Must be explicitly enabled in config
- Best for: Peer-to-peer communication, handoffs, notifications

## Key Decision Framework

- Is it a parent→child task delegation? → **spawn**
- Is it peer-to-peer collaboration? → **send**
- Does it need background processing? → **spawn**
- Does it need back-and-forth dialogue? → **send**
- Is it a one-way notification? → **send** (fire-and-forget)

---

## Cross-Agent Spawn Permissions

For agents that spawn sub-agents under a DIFFERENT agent id:

```json5
{
  agents: {
    list: [
      {
        id: '{spawning-agent}',
        subagents: {
          allowAgents: ['{target-agent-1}', '{target-agent-2}'],
        },
      },
    ],
  },
}
```

## Agent-to-Agent Messaging Config

For agents using `sessions_send`:

```json5
{
  tools: {
    agentToAgent: {
      enabled: true,
      allow: ['{agent-a}', '{agent-b}'],
    },
  },
}
```

**Ping-pong settings:**
- `maxPingPongTurns`: How many reply rounds? (0-5, default 5)
- Agents can reply `REPLY_SKIP` to end conversations early
- `ANNOUNCE_SKIP` skips posting announce to target channel

## Session Key Patterns

- Main DMs: `agent:{agentId}:{mainKey}`
- Groups: `agent:{agentId}:{channel}:group:{id}`
- Sub-agents: `agent:{agentId}:subagent:{uuid}`
- Cron: `cron:{job.id}`
