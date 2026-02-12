---
name: 'step-07-boundary-rules'
description: 'Define privacy rules, escalation triggers, and data handling policies'

nextStepFile: './step-08-review-report.md'
outputFile: '{output_folder}/hardening-report-{project_name}.md'
hardeningDefaults: '../data/hardening-defaults.md'
boundaryRef: '../data/boundary-config-reference.md'
---

# Step 7: Boundary Rules

## STEP GOAL:

Define boundary rules for each agent — privacy protections, escalation triggers for human handoff, and data handling policies that govern how agents interact with sensitive information.

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
- ✅ You bring deep expertise in agent safety, privacy, and boundary design
- ✅ User brings their compliance requirements and operational policies

### Step-Specific Rules:

- 🎯 Focus ONLY on boundary rules: privacy, escalation, data handling
- 🚫 FORBIDDEN to configure memory, tools, failover, observability, or self-correction
- 💬 Approach: Safety-first — protect users, protect data, know when to escalate
- 📋 Generate boundary config per agent

## EXECUTION PROTOCOLS:

- 🎯 Follow the MANDATORY SEQUENCE exactly
- 💾 Append boundary rules to {outputFile}
- 📖 Update frontmatter stepsCompleted when complete
- 🚫 FORBIDDEN to load next step until user approves boundary rules

## CONTEXT BOUNDARIES:

- Assessment from Step 1 identifies current boundary state
- Load hardening defaults for boundary rule patterns
- Focus: Privacy rules, escalation triggers, data handling policies
- Limits: Do NOT configure other hardening domains

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Load Boundary Defaults

Load `{hardeningDefaults}` and extract the Boundary Rule Defaults section. Also load `{boundaryRef}` for default tables and configuration templates.

### 2. Check Scope

**If boundary rules are NOT in the hardening scope:**
"**Boundary rules are not in scope. Skipping to review.**"
→ Auto-proceed to {nextStepFile}

### 3. Configure Privacy Rules

"**Boundary Rules Configuration**

**Privacy Rules** protect user data and prevent information leakage."

Present the privacy rule defaults table from {boundaryRef}.

"**Accept all defaults? Any rules to add or remove?**"

Wait for user input.

### 4. Configure Escalation Triggers

"**Escalation Triggers** define when an agent should hand off to a human or another agent."

Present the escalation trigger defaults table from {boundaryRef}.

"**For each agent, which triggers should be enabled? Recommended per agent:**"

For each agent:
| Agent | Triggers |
|-------|----------|
| {name} | {recommended triggers based on role} |

"**Adjust any?**"

Wait for user input.

### 5. Configure Data Handling Policies

"**Data Handling Policies** govern how agents process and store data."

Present the data handling policy defaults table from {boundaryRef}.

"**Accept defaults or customize? Consider:**
- Does your domain have specific data retention requirements?
- Are there compliance standards (GDPR, HIPAA, etc.) to consider?"

Wait for user input.

### 6. Generate Boundary Configuration

Using the configuration template from {boundaryRef}, generate per-agent boundary rules based on user's choices.

### 7. Append to Report

Append boundary rules to {outputFile} under "## Boundary Rules".

### 8. Present MENU OPTIONS

Display: "**Boundary rules configured. Select an Option:** [C] Continue to Review & Report"

#### Menu Handling Logic:

- IF C: Save boundary rules to {outputFile}, update frontmatter stepsCompleted with 'step-07-boundary-rules', then load, read entire file, then execute {nextStepFile}
- IF Any other comments or queries: help user respond then redisplay menu

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed to next step when user selects 'C'

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN C is selected and boundary rules are saved to report will you load `{nextStepFile}`.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- Privacy rules configured per agent
- Escalation triggers defined with clear conditions and actions
- Data handling policies set with appropriate retention
- User approved all boundary rules

### ❌ SYSTEM FAILURE:

- No privacy rules (data leakage risk)
- No escalation triggers (agents never hand off)
- No data handling policies (compliance risk)

**Master Rule:** Boundaries protect both users and agents. Every agent needs privacy rules, escalation paths, and data handling policies appropriate to its role.
