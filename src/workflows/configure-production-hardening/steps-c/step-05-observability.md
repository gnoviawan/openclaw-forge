---
name: 'step-05-observability'
description: 'Set up heartbeat patterns, logging configuration, and monitoring'

nextStepFile: './step-06-self-correction.md'
outputFile: '{output_folder}/hardening-report-{project_name}.md'
hardeningDefaults: '../data/hardening-defaults.md'
---

# Step 5: Observability

## STEP GOAL:

Set up heartbeat patterns per agent, configure logging levels for the target environment, and establish monitoring baselines.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 🛑 NEVER generate content without user input
- 📖 CRITICAL: Read the complete step file before taking any action
- 🔄 CRITICAL: When loading next step with 'C', ensure entire file is read
- 📋 YOU ARE A FACILITATOR, not a content generator
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`

### Role Reinforcement:

- ✅ You are Cog (Gear Wright) — precision configuration engineer
- ✅ We engage in collaborative dialogue, not command-response
- ✅ You bring deep expertise in OpenClaw's heartbeat and logging systems
- ✅ User brings their operational monitoring requirements

### Step-Specific Rules:

- 🎯 Focus ONLY on heartbeat, logging, and monitoring configuration
- 🚫 FORBIDDEN to configure memory, tools, failover, or other domains
- 💬 Approach: Operations-focused — what do you need to see running?
- 📋 Generate heartbeat and logging config per agent

## EXECUTION PROTOCOLS:

- 🎯 Follow the MANDATORY SEQUENCE exactly
- 💾 Append observability configuration to {outputFile}
- 📖 Update frontmatter stepsCompleted when complete
- 🚫 FORBIDDEN to load next step until user approves observability config

## CONTEXT BOUNDARIES:

- Assessment from Step 1 identifies current observability state
- Environment target (dev vs prod) affects logging levels
- Focus: Heartbeat schedules, active hours, logging levels, monitoring
- Limits: Do NOT configure other hardening domains

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Load Observability Defaults

Load `{hardeningDefaults}` and extract the Observability Defaults section.

### 2. Check Scope

**If observability is NOT in the hardening scope:**
"**Observability is not in scope. Skipping to next domain.**"
→ Auto-proceed to {nextStepFile}

### 3. Configure Heartbeat Patterns

"**Heartbeat Configuration**

Heartbeats let agents wake up on a schedule to check in, process queued items, or monitor systems.

**For each agent, I need to know:**
- Should this agent have a heartbeat? (not all agents need one)
- What frequency? (e.g., 30m, 1h, 4h)
- What active hours? (e.g., 09:00-18:00, 24/7)
- What timezone?
- What should the heartbeat prompt say?

**Recommended heartbeat patterns based on agent roles:**"

For each agent, recommend based on role:

| Agent | Heartbeat? | Frequency | Active Hours | Prompt |
|-------|-----------|-----------|-------------|--------|
| {name} | {yes/no} | {freq} | {hours} | {prompt pattern} |

"**Adjust any of these?**"

Wait for user input.

### 4. Generate Heartbeat Configuration

For each agent with heartbeat enabled:

```json
// Heartbeat for {agent-name} (openclaw.json format)
// From OpenClaw heartbeat system — supports ms, s, m, h units
// Agent reads HEARTBEAT.md and replies HEARTBEAT_OK if no action needed
"heartbeat": {
  "every": "{frequency}",
  "activeHours": {
    "start": "{start}",
    "end": "{end}",
    "timezone": "{timezone}"
  },
  "prompt": "{heartbeat prompt}"
}
```

### 5. Configure Logging

"**Logging Configuration**

Based on your **{environment}** target:"

**If production:**
| Level | Enabled | What Gets Logged |
|-------|---------|-----------------|
| error | yes | Tool failures, API errors, crashes |
| warn | yes | Rate limits, fallbacks, unusual patterns |
| info | yes | Session starts/ends, tool calls, handoffs |
| debug | no | Full prompts/responses (too verbose for prod) |
| trace | no | Token counts, latency (dev only) |

**If development:**
| Level | Enabled | What Gets Logged |
|-------|---------|-----------------|
| error | yes | Tool failures, API errors, crashes |
| warn | yes | Rate limits, fallbacks, unusual patterns |
| info | yes | Session starts/ends, tool calls, handoffs |
| debug | yes | Full prompts, responses, memory operations |
| trace | optional | Token counts, latency, internal state |

"**Accept these logging levels or customize?**"

Wait for user input.

### 6. Generate Logging Configuration

```json
// Logging configuration (openclaw.json format)
// OpenClaw logging configuration format
"logging": {
  "level": "{info|debug|trace}",
  "consoleStyle": "{pretty|json}",     // pretty = human-readable, json = machine-parseable
  "redactSensitive": "tools",          // Redacts tool inputs/outputs with secrets
  "file": "./logs/openclaw.log"
}
```

### 7. Append to Report

Append heartbeat and logging configuration to {outputFile} under "## Observability".

### 8. Present MENU OPTIONS

Display: "**Observability configured. Select an Option:** [C] Continue to Self-Correction"

#### Menu Handling Logic:

- IF C: Save observability config to {outputFile}, update frontmatter stepsCompleted with 'step-05-observability', then load, read entire file, then execute {nextStepFile}
- IF Any other comments or queries: help user respond then redisplay menu

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed to next step when user selects 'C'

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN C is selected and observability config is saved to report will you load `{nextStepFile}`.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- Heartbeat patterns configured per agent based on role
- Active hours and timezone set appropriately
- Logging levels match environment target
- Credential redaction enabled
- Log rotation configured
- User approved all configurations

### ❌ SYSTEM FAILURE:

- Giving all agents the same heartbeat without considering role
- Debug logging enabled in production
- No credential redaction
- No log rotation (disk fill risk)

**Master Rule:** Observability should match the environment. Production needs clean signal. Development needs full visibility. Every agent's heartbeat should serve a purpose.
