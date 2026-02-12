---
name: 'step-06-self-correction'
description: 'Add error journaling, pre-response checks, and feedback capture'

nextStepFile: './step-07-boundary-rules.md'
outputFile: '{output_folder}/hardening-report-{project_name}.md'
hardeningDefaults: '../data/hardening-defaults.md'
selfCorrectionRef: '../data/self-correction-config-reference.md'
---

# Step 6: Self-Correction

## STEP GOAL:

Add self-correction directives to each agent — error journaling for learning from mistakes, pre-response checks for catching issues before they reach users, and feedback capture for continuous improvement.

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
- ✅ You bring deep expertise in OpenClaw's self-correction patterns
- ✅ User brings their quality and reliability requirements

### Step-Specific Rules:

- 🎯 Focus ONLY on self-correction: error journaling, pre-response checks, feedback capture
- 🚫 FORBIDDEN to configure memory, tools, failover, observability, or boundaries
- 💬 Approach: Quality engineering — catch and learn from mistakes
- 📋 Generate REVIEW.md directives and self-correction config per agent

## EXECUTION PROTOCOLS:

- 🎯 Follow the MANDATORY SEQUENCE exactly
- 💾 Append self-correction configuration to {outputFile}
- 📖 Update frontmatter stepsCompleted when complete
- 🚫 FORBIDDEN to load next step until user approves self-correction config

## CONTEXT BOUNDARIES:

- Assessment from Step 1 identifies current self-correction state
- Load hardening defaults for self-correction patterns
- Focus: Error journaling, pre-response checks, feedback capture, REVIEW.md
- Limits: Do NOT configure other hardening domains

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Load Self-Correction Defaults

Load `{hardeningDefaults}` and extract the Self-Correction Defaults section. Also load `{selfCorrectionRef}` for configuration templates.

### 2. Check Scope

**If self-correction is NOT in the hardening scope:**
"**Self-correction is not in scope. Skipping to next domain.**"
→ Auto-proceed to {nextStepFile}

### 3. Configure Error Journaling

"**Self-Correction Configuration**

**Error Journaling** captures mistakes so agents learn from them.

**What gets captured:**
- Tool failures, user corrections, validation errors, boundary violations

**Configuration:**"

```yaml
errorJournal:
  enabled: true
  maxEntries: 50
  retentionDays: 30
  captureOn:
    - tool-failure
    - user-correction
    - validation-error
    - boundary-violation
```

"**Accept these defaults or customize?**"

Wait for user input.

### 4. Configure Pre-Response Checks

Present the pre-response checks table from {selfCorrectionRef}.

"**Which checks should be enabled for each agent? Recommended:**"

For each agent:
- {Agent}: {recommended checks based on role}

"**Adjust?**"

Wait for user input.

### 5. Configure Feedback Capture

"**Feedback Capture** closes the improvement loop — capturing user corrections, tool errors, self-detected issues, and explicit feedback.

**Accept default triggers or customize?**"

Wait for user input.

### 6. Generate REVIEW.md Directives

Using the REVIEW.md directive template from {selfCorrectionRef}, generate per-agent self-correction directives.

### 7. Generate Self-Correction Configuration

Using the configuration template from {selfCorrectionRef}, generate the complete self-correction config based on user's choices.

### 8. Append to Report

Append self-correction configuration and REVIEW.md directives to {outputFile} under "## Self-Correction".

### 9. Present MENU OPTIONS

Display: "**Self-correction configured. Select an Option:** [C] Continue to Boundary Rules"

#### Menu Handling Logic:

- IF C: Save self-correction config to {outputFile}, update frontmatter stepsCompleted with 'step-06-self-correction', then load, read entire file, then execute {nextStepFile}
- IF Any other comments or queries: help user respond then redisplay menu

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed to next step when user selects 'C'

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN C is selected and self-correction config is saved to report will you load `{nextStepFile}`.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- Error journaling configured with appropriate triggers
- Pre-response checks selected per agent based on role
- Feedback capture enabled with clear triggers
- REVIEW.md directives generated per agent
- User approved all configurations

### ❌ SYSTEM FAILURE:

- No error journaling (agents can't learn)
- No pre-response checks (mistakes reach users)
- No feedback capture (no improvement loop)

**Master Rule:** Self-correction is a sign of maturity. Every agent should journal errors, check before responding, and capture feedback for improvement.
