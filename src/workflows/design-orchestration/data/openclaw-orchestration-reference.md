# OpenClaw Orchestration Reference

Quick reference for orchestration primitives used during the design workflow.

---

## Agent Definition

Each agent is a fully scoped brain with its own workspace, state directory, and session store.

```json5
{
  agents: {
    list: [
      {
        id: "agent-id",
        name: "Display Name",
        workspace: "~/.openclaw/workspace-agent-id",
        agentDir: "~/.openclaw/agents/agent-id/agent",
        // Optional overrides:
        model: { primary: "anthropic/claude-sonnet-4" },
        identity: { name: "Agent Name" },
      },
    ],
  },
}
```

---

## Bindings (Channel Routing)

Bindings route inbound messages to agents. Most-specific match wins.

**Match Priority (highest to lowest):**
1. `peer` match (exact DM/group/channel id)
2. `guildId` (Discord)
3. `teamId` (Slack)
4. `accountId` match for a channel
5. Channel-level match (`accountId: "*"`)
6. Fallback to default agent

```json5
{
  bindings: [
    // Peer-level (most specific)
    {
      agentId: "ops",
      match: { channel: "whatsapp", peer: { kind: "group", id: "12036...@g.us" } },
    },
    // Account-level
    {
      agentId: "work",
      match: { channel: "whatsapp", accountId: "biz" },
    },
    // Channel-level (least specific)
    {
      agentId: "main",
      match: { channel: "telegram" },
    },
  ],
}
```

---

## sessions_spawn (Sub-Agents)

Spawn background tasks in isolated sessions. Non-blocking.

**Parameters:**
- `task` (required) — what the sub-agent should do
- `label` — short identifier
- `agentId` — spawn under a different agent (must be allowed)
- `model` — override model
- `thinking` — override thinking level
- `runTimeoutSeconds` — abort after N seconds
- `cleanup` — `"delete"` or `"keep"` (default)

**Cross-Agent Spawning:**
```json5
{
  agents: {
    list: [
      {
        id: "orchestrator",
        subagents: {
          allowAgents: ["researcher", "coder"], // or ["*"]
        },
      },
    ],
  },
}
```

**Constraints:**
- Sub-agents cannot spawn sub-agents (no nesting)
- Max concurrent: 8 (configurable)
- Auto-archive after 60 minutes (configurable)

---

## sessions_send (Agent-to-Agent Messaging)

Send a message into another session. Supports sync and fire-and-forget.

**Parameters:**
- `sessionKey` (required)
- `message` (required)
- `timeoutSeconds` (default >0; 0 = fire-and-forget)

**Reply Ping-Pong:**
- After primary run, agents alternate replies
- Reply `REPLY_SKIP` to stop
- Max turns: `session.agentToAgent.maxPingPongTurns` (0-5, default 5)

**Agent-to-Agent must be enabled:**
```json5
{
  tools: {
    agentToAgent: {
      enabled: true,
      allow: ["agent-a", "agent-b"],
    },
  },
}
```

---

## Sub-Agent Tool Policy

Default denied tools for sub-agents:
- `sessions_list`, `sessions_history`, `sessions_send`, `sessions_spawn`
- `gateway`, `agents_list`, `whatsapp_login`
- `session_status`, `cron`
- `memory_search`, `memory_get`

**Custom restrictions:**
```json5
{
  tools: {
    subagents: {
      tools: {
        deny: ["browser", "firecrawl"],
        // OR restrict to only specific tools:
        allow: ["read", "exec", "write", "edit"],
      },
    },
  },
}
```

---

## Per-Agent Tool & Sandbox Configuration

```json5
{
  agents: {
    list: [
      {
        id: "restricted-agent",
        tools: {
          allow: ["read", "exec"],
          deny: ["write", "edit", "apply_patch"],
        },
        sandbox: {
          mode: "all",
          scope: "agent",
        },
      },
    ],
  },
}
```

---

## Group Chat Configuration

```json5
{
  agents: {
    list: [
      {
        id: "group-agent",
        groupChat: {
          mentionPatterns: ["@agent", "@agentbot"],
        },
      },
    ],
  },
}
```

---

## Session Send Policy

```json5
{
  session: {
    sendPolicy: {
      rules: [
        { match: { channel: "discord", chatType: "group" }, action: "deny" },
      ],
      default: "allow",
    },
  },
}
```
