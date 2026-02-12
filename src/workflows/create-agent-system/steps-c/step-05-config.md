---
name: 'step-05-config'
description: 'Generate openclaw.json fragments, tool policies, memory config, failover config, heartbeat config, logging config'

nextStepFile: './step-06-self-correction.md'
outputFile: '{ocf_output_folder}/{system_name}/workspace-plan.md'
artifactSchemas: '../data/ocf-artifact-schemas.md'
advancedElicitationTask: '{project-root}/_bmad/core/workflows/advanced-elicitation/workflow.xml'
partyModeWorkflow: '{project-root}/_bmad/core/workflows/party-mode/workflow.md'
---

# Step 5: Config Generation

## STEP GOAL:

To generate openclaw.json fragments per agent, and system-level configuration files: tool-policies.json, memory-config.json, failover-config.json, heartbeat-config.json, and logging-config.json. Config is derived from the brief's Memory & Resilience section and the overall architecture, informed by all previous artifacts. This is the Cog (Gear Wright) phase — configuration and systems expertise.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- Generate content FROM the validated brief — the brief IS the user's input
- CRITICAL: Read the complete step file before taking any action
- CRITICAL: When loading next step with 'C', ensure entire file is read
- YOU ARE A FACILITATOR, not a content generator
- YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`
- TOOL/SUBPROCESS FALLBACK: If any instruction references a subprocess, subagent, or tool you do not have access to, you MUST still achieve the outcome in your main context thread

### Role Reinforcement:

- You are Cog (Gear Wright) — configuration and systems expert
- You translate architecture decisions into concrete, deployable configuration
- Every config value must trace back to a design decision from the brief or previous artifacts
- You bring systems engineering expertise, user brings their operational requirements

### Step-Specific Rules:

- Focus on generating openclaw.json fragments (per agent) and system-level config files
- FORBIDDEN to generate REVIEW.md, self-correction directives, or assembly artifacts — those come in later steps
- Config is derived from the brief's Memory & Resilience section and overall architecture
- Follow the openclaw.json and System Config schemas from {artifactSchemas} strictly
- Use subprocess per agent for openclaw.json fragments in large rosters (Pattern 2); fallback to sequential generation

## EXECUTION PROTOCOLS:

- Follow the MANDATORY SEQUENCE exactly
- Append generated content to {outputFile} — per-agent config under agent sections, system config in a new System Configuration section
- Update stepsCompleted and Generation Progress table in {outputFile} frontmatter when done
- FORBIDDEN to skip any agent or any system config file

## CONTEXT BOUNDARIES:

- Available: workspace-plan.md with all previous artifacts (identity, context, skills), source brief data
- Focus: Configuration — openclaw.json per agent, system config files
- Limits: Do NOT generate REVIEW.md or self-correction artifacts, do NOT assemble final directory
- Dependencies: Requires all previous artifacts (identity, context, skills) for complete configuration

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Load Context

Load {outputFile} (workspace-plan.md) and extract:
- Agent roster (names, roles, responsibilities)
- Identity artifacts (SOUL.md, AGENTS.md — boundaries inform permissions)
- Context artifacts (USER.md, MEMORY.md — memory categories inform memory config)
- Skill artifacts (SKILL.md files — skill list informs tool policies)
- Architecture context (memory architecture, resilience requirements from brief)

Load {artifactSchemas} and extract the openclaw.json fragment schema and all System Config schemas (tool-policies.json, memory-config.json, failover-config.json, heartbeat-config.json, logging-config.json).

### 2. Generate Per-Agent Config

DO NOT BE LAZY — For EACH agent in the roster, generate an openclaw.json fragment:

For each agent:

a. **Generate openclaw.json fragment** following the schema:
   - Agent name (kebab-case identifier)
   - Model (model-id derived from agent's complexity and role)
   - Tools: allowed tools (derived from skill artifacts), denied tools (derived from agent boundaries)
   - Memory: provider reference, config reference pointing to system memory-config.json
   - Permissions: file_read, file_write, web_access, subprocess — derived from AGENTS.md boundaries and authorized actions

b. **Append generated content** to {outputFile} under the agent's roster section:
   ```markdown
   ### {Agent Display Name} — Config Artifacts

   #### openclaw.json fragment
   ```json
   {generated openclaw.json fragment}
   ```
   ```

**Subprocess optimization (Pattern 2):** For agent rosters > 3 agents, launch a subprocess per agent. Each subprocess receives the agent's artifacts and schemas, and returns the generated openclaw.json fragment. If subprocess unavailable, generate sequentially in main thread.

### 3. Generate System-Level Config Files

Generate each system-level config file using the schemas from {artifactSchemas}:

a. **tool-policies.json** — aggregate tool policies across all agents:
   - For each agent: allowed_tools, denied_tools, tool_approval_required
   - Derived from per-agent openclaw.json tools and AGENTS.md boundaries

b. **memory-config.json** — system memory architecture:
   - Architecture type (shared/isolated/hybrid) from brief's memory architecture
   - Providers (vector/file/api) with configuration
   - Derived from MEMORY.md artifacts across all agents

c. **failover-config.json** — failover strategy:
   - For each agent: fallback_agent, max_retries, timeout_ms
   - Derived from AGENTS.md relationships and brief's resilience requirements

d. **heartbeat-config.json** — health monitoring:
   - Interval, per-agent health check type, alert threshold
   - Derived from brief's resilience and monitoring requirements

e. **logging-config.json** — system logging:
   - Global log level, per-agent log level and destination
   - Derived from brief's logging and monitoring needs

Append all system config files to {outputFile} in a new section:
```markdown
## System Configuration

### tool-policies.json
```json
{generated content}
```

### memory-config.json
```json
{generated content}
```

### failover-config.json
```json
{generated content}
```

### heartbeat-config.json
```json
{generated content}
```

### logging-config.json
```json
{generated content}
```
```

### 4. Cross-Reference Configuration

After all config is generated:
- Verify that every agent's tool list in openclaw.json matches their skill artifacts
- Ensure memory config references are consistent between openclaw.json fragments and memory-config.json
- Validate failover chains (no circular dependencies, fallback agents exist)
- Confirm permissions align with AGENTS.md boundaries
- Fix any inconsistencies

### 5. Present Summary

"**Config generation complete.**

**Per-Agent Config:**

| Agent | Model | Tools (Allowed) | Permissions Summary |
|-------|-------|-----------------|-------------------|
| {agent-1} | {model} | {tool count} | {permission summary} |
| {agent-2} | {model} | {tool count} | {permission summary} |
...

**System Config Files:**
- tool-policies.json: {agent count} agent policies
- memory-config.json: {architecture type}, {provider count} providers
- failover-config.json: {failover chain count} failover chains
- heartbeat-config.json: {interval}ms interval, {agent count} agents monitored
- logging-config.json: {global level} global level

**Cross-references:** {verified/adjusted count} config entries validated"

### 6. Present MENU OPTIONS

Display: **Select an Option:** [A] Advanced Elicitation [P] Party Mode [C] Continue

#### Menu Handling Logic:

- IF A: Execute {advancedElicitationTask}, and when finished redisplay the menu
- IF P: Execute {partyModeWorkflow}, and when finished redisplay the menu
- IF C: Save all generated content to {outputFile}, update frontmatter stepsCompleted to include 'step-05-config', update Generation Progress table (mark step 05 as Complete), then load, read entire file, then execute {nextStepFile}
- IF Any other: help user, then [Redisplay Menu Options](#6-present-menu-options)

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed to next step when user selects 'C'
- After other menu items execution, return to this menu

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN C is selected and all per-agent config fragments and system config files have been appended to {outputFile} will you then load and read fully `{nextStepFile}` to execute self-correction generation.

---

## SYSTEM SUCCESS/FAILURE METRICS

### SUCCESS:

- openclaw.json fragment generated for every agent in the roster
- All 5 system config files generated (tool-policies, memory-config, failover-config, heartbeat-config, logging-config)
- Schemas followed strictly
- Config values traced to brief decisions and previous artifacts
- Cross-references verified (tools match skills, memory refs consistent, failover chains valid)
- All content appended to workspace-plan.md
- stepsCompleted updated

### SYSTEM FAILURE:

- Skipping any agent's openclaw.json fragment
- Missing any of the 5 system config files
- Config values not traceable to design decisions
- Circular failover dependencies
- Permissions not aligned with AGENTS.md boundaries
- Tools in config not matching skill artifacts
- Generating artifacts beyond config (REVIEW.md, assembly, etc.)
- Not appending content to workspace-plan.md

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
