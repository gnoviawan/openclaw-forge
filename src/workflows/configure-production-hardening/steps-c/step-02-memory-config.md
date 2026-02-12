---
name: 'step-02-memory-config'
description: 'Configure memory backends with auto-recall and capture per agent'

nextStepFile: './step-03-tool-policies.md'
outputFile: '{output_folder}/hardening-report-{project_name}.md'
hardeningDefaults: '../data/hardening-defaults.md'
---

# Step 2: Memory Configuration

## STEP GOAL:

Configure memory backends for each agent in the workspace — selecting the appropriate backend, setting auto-recall and auto-capture strategies, and configuring sidecar folders where needed.

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
- ✅ You bring deep expertise in OpenClaw's memory system
- ✅ User brings their agent context and operational needs

### Step-Specific Rules:

- 🎯 Focus ONLY on memory configuration for each agent
- 🚫 FORBIDDEN to configure tool policies, failover, or other domains
- 💬 Approach: Present recommended defaults, let user customize per agent
- 📋 Generate complete memory config block for each agent

## EXECUTION PROTOCOLS:

- 🎯 Follow the MANDATORY SEQUENCE exactly
- 💾 Append memory configuration to {outputFile}
- 📖 Update frontmatter stepsCompleted when complete
- 🚫 FORBIDDEN to load next step until user approves memory config

## CONTEXT BOUNDARIES:

- Assessment from Step 1 identifies agents and current memory state
- Load hardening defaults for recommended patterns
- Focus: Memory backends, recall strategies, capture strategies, sidecar config
- Limits: Do NOT configure other hardening domains

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Load Memory Defaults

Load `{hardeningDefaults}` and extract the Memory Backend Defaults section for reference.

### 2. Check Scope

**If memory configuration is NOT in the hardening scope (from Step 1):**
"**Memory configuration is not in scope for this hardening pass. Skipping to next domain.**"
→ Auto-proceed to {nextStepFile}

### 3. Present Current State

"**Memory Configuration**

Here's the current memory state for each agent:"

For each agent from the assessment:
- Current backend: {existing or "none"}
- Current recall: {existing or "not configured"}
- Current capture: {existing or "not configured"}
- Has sidecar: {yes/no}

### 4. Recommend Memory Configuration

For each agent, based on their role and the defaults:

"**Recommended memory configuration:**"

| Agent | Backend | Auto-Recall | Auto-Capture | Sidecar |
|-------|---------|-------------|--------------|---------|
| {name} | {recommended} | {strategy} | {strategy} | {yes/no} |

"**This is based on each agent's role:**
- {Agent 1}: {reasoning for recommendation}
- {Agent 2}: {reasoning for recommendation}
- ...

**Would you like to adjust any of these? Or accept the recommendations?**"

Wait for user input. If they want changes, discuss and adjust.

### 5. Generate Memory Configuration

For each agent, generate the configuration block:

```json
// Memory configuration for {agent-name} (openclaw.json format)
"memory": {
  "backend": "{selected-backend}",  // builtin | lancedb | qmd | (disabled)
  "autoCapture": {true/false},
  "autoRecall": {true/false},
  "embedding": {
    "provider": "{provider}",       // openai | local | voyage
    "model": "{embedding-model}"    // e.g. text-embedding-3-small
  }
}
    captureTypes:
      - user-facts
      - decisions
      - corrections
```

If agent needs sidecar:
```
Sidecar folder: _memory/{agent-name}/
  - memories.md (append-only context log)
  - instructions.md (mutable operational directives)
```

### 6. Append to Report

Append the complete memory configuration to {outputFile} under the "## Memory Configuration" section, replacing the placeholder.

### 7. Present MENU OPTIONS

Display: "**Memory configuration complete. Select an Option:** [C] Continue to Tool Policies"

#### Menu Handling Logic:

- IF C: Save memory config to {outputFile}, update frontmatter stepsCompleted with 'step-02-memory-config', then load, read entire file, then execute {nextStepFile}
- IF Any other comments or queries: help user respond then redisplay menu

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed to next step when user selects 'C'

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN C is selected and memory config is saved to report will you load `{nextStepFile}` to execute tool policy configuration.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- All agents have memory configuration assigned
- Backend, recall, and capture strategies specified per agent
- Sidecar folders identified where needed
- User approved the configuration
- Configuration appended to hardening report

### ❌ SYSTEM FAILURE:

- Applying same config to all agents without considering their roles
- Not presenting defaults for user review
- Skipping agents
- Not appending to report

**Master Rule:** Every agent needs memory configuration tailored to its role. Present sensible defaults, let the user customize.
