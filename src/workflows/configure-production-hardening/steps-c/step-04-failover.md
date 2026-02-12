---
name: 'step-04-failover'
description: 'Configure model fallback chains and context overflow handling'

nextStepFile: './step-05-observability.md'
outputFile: '{output_folder}/hardening-report-{project_name}.md'
hardeningDefaults: '../data/hardening-defaults.md'
failoverRef: '../data/failover-config-reference.md'
---

# Step 4: Failover & Resilience

## STEP GOAL:

Configure model fallback chains for each agent, set up context overflow handling strategies, and define retry policies for transient failures.

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
- ✅ You bring deep expertise in OpenClaw's failover and resilience systems
- ✅ User brings their reliability requirements and provider preferences

### Step-Specific Rules:

- 🎯 Focus ONLY on failover chains, context overflow, and retry policies
- 🚫 FORBIDDEN to configure memory, tools, or other domains
- 💬 Approach: Reliability engineering — plan for failure gracefully
- 📋 Generate complete failover config per agent or system-wide

## EXECUTION PROTOCOLS:

- 🎯 Follow the MANDATORY SEQUENCE exactly
- 💾 Append failover configuration to {outputFile}
- 📖 Update frontmatter stepsCompleted when complete
- 🚫 FORBIDDEN to load next step until user approves failover config

## CONTEXT BOUNDARIES:

- Assessment from Step 1 identifies current failover state
- Load hardening defaults for fallback chain patterns
- Focus: Model cascades, context overflow, retry policies
- Limits: Do NOT configure other hardening domains

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Load Failover Defaults

Load `{hardeningDefaults}` and extract the Failover Chain Defaults section.

### 2. Check Scope

**If failover is NOT in the hardening scope:**
"**Failover configuration is not in scope. Skipping to next domain.**"
→ Auto-proceed to {nextStepFile}

### 3. Assess Provider Availability

"**Failover & Resilience Configuration**

To configure fallback chains, I need to know which model providers are available in your environment:

- **Anthropic** (Claude models) — available? [Y/N]
- **OpenAI** (GPT models) — available? [Y/N]
- **Other providers** — list any additional providers

**Also, what is your primary model preference?**"

Wait for user input.

### 4. Design Fallback Chains

Based on available providers, design cascading fallback chains:

"**Recommended fallback chains:**

**Primary chain** (for main agent interactions):
1. {primary model} — timeout: {ms}
2. {fallback model} — timeout: {ms}
3. {lightweight fallback} — timeout: {ms}

**Lightweight chain** (for simple tasks, subagents):
1. {lightweight model} — timeout: {ms}
2. {ultra-lightweight fallback} — timeout: {ms}

**Any adjustments?**"

Wait for user input.

### 5. Configure Context Overflow

"**Context Overflow Handling**

When conversations exceed the model's context limit, OpenClaw can:

1. **Compaction** — Summarize older messages while preserving tool failures and file operations (recommended)
2. **Truncation** — Drop oldest messages beyond summary (fallback)
3. **Escalation** — Alert user and suggest session reset (last resort)

**Recommended strategy:** Compaction at 80% limit → Truncation if insufficient → Escalation on repeated overflow

**Accept this strategy or customize?**"

Wait for user input.

### 6. Configure Retry Policy

Present the retry policy defaults from {failoverRef} and ask: "**Accept these defaults or customize?**"

Wait for user input.

### 7. Generate Failover Configuration

Using the configuration template from {failoverRef}, generate the complete failover config for each agent based on user's choices.

### 8. Append to Report

Append the failover configuration to {outputFile} under "## Failover & Resilience".

### 9. Present MENU OPTIONS

Display: "**Failover configured. Select an Option:** [C] Continue to Observability"

#### Menu Handling Logic:

- IF C: Save failover config to {outputFile}, update frontmatter stepsCompleted with 'step-04-failover', then load, read entire file, then execute {nextStepFile}
- IF Any other comments or queries: help user respond then redisplay menu

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed to next step when user selects 'C'

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN C is selected and failover config is saved to report will you load `{nextStepFile}`.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- Fallback chains configured with available providers
- Context overflow strategy defined
- Retry policies set for all error types
- Compaction preserves critical data (tool failures, file ops)
- User approved all configurations

### ❌ SYSTEM FAILURE:

- Single point of failure (no fallback configured)
- Not asking about available providers
- Context overflow with no strategy
- Not preserving critical data during compaction

**Master Rule:** Plan for failure. Every model call needs a fallback. Every context overflow needs a strategy. Preserve what matters during compaction.
