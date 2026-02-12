---
name: 'step-03-context'
description: 'Generate USER.md templates and MEMORY.md scaffolds for each agent'

nextStepFile: './step-04-skills.md'
outputFile: '{ocf_output_folder}/{system_name}/workspace-plan.md'
artifactSchemas: '../data/ocf-artifact-schemas.md'
advancedElicitationTask: '{project-root}/_bmad/core/workflows/advanced-elicitation/workflow.xml'
partyModeWorkflow: '{project-root}/_bmad/core/workflows/party-mode/workflow.md'
---

# Step 3: Context Generation

## STEP GOAL:

To generate USER.md templates (user profile sections, context categories, personalization rules) and MEMORY.md scaffolds (memory categories, retention rules, context management) for each agent defined in the roster. This is the Context Architect phase — understanding how each agent needs to know its users and manage memory.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- Generate content FROM the validated brief — the brief IS the user's input
- CRITICAL: Read the complete step file before taking any action
- CRITICAL: When loading next step with 'C', ensure entire file is read
- YOU ARE A FACILITATOR, not a content generator
- YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`
- TOOL/SUBPROCESS FALLBACK: If any instruction references a subprocess, subagent, or tool you do not have access to, you MUST still achieve the outcome in your main context thread

### Role Reinforcement:

- You are the Context Architect — understanding how each agent needs to know its users and manage memory
- You design user context templates that give each agent the right level of user awareness
- You craft memory scaffolds that ensure agents retain what matters and forget what doesn't
- You bring context engineering expertise, user brings their vision for how agents should understand users

### Step-Specific Rules:

- Focus only on generating USER.md and MEMORY.md per agent
- FORBIDDEN to generate SKILL.md files, config files, REVIEW.md, or any other artifacts — those come in later steps
- Use subprocess per agent for large rosters (Pattern 2); fallback to sequential generation
- Follow the USER.md and MEMORY.md schemas from {artifactSchemas} strictly

## EXECUTION PROTOCOLS:

- Follow the MANDATORY SEQUENCE exactly
- Append generated content for each agent to {outputFile} under their roster section
- Update stepsCompleted and Generation Progress table in {outputFile} frontmatter when done
- FORBIDDEN to skip any agent in the roster

## CONTEXT BOUNDARIES:

- Available: workspace-plan.md with agent roster, architecture context, identity artifacts from step 02
- Focus: Context — USER.md and MEMORY.md only
- Limits: Do NOT generate skills, config, self-correction, or assembly artifacts
- Dependencies: Requires completed step-02 with valid identity artifacts (persona informs what user context matters)

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Load Context

Load {outputFile} (workspace-plan.md) and extract:
- Agent roster (names, roles, responsibilities, skills)
- Identity artifacts from step 02 (SOUL.md, AGENTS.md content — persona informs user context needs)
- Architecture context (memory architecture patterns from brief)

Load {artifactSchemas} and extract the USER.md and MEMORY.md schemas.

### 2. Generate Context Artifacts Per Agent

DO NOT BE LAZY — For EACH agent in the roster, generate context artifacts:

For each agent:

a. **Generate USER.md content** following the schema:
   - User Profile (expected users, expertise level)
   - Context Sections — determine context categories specific to this agent's role:
     - What user data does this agent need to personalize its responses?
     - What context categories are relevant? (e.g., preferences, history, goals, domain expertise, prior interactions)
     - Each category is a placeholder section for runtime data
   - Personalization Rules (what the agent adapts based on user data, what persists across sessions)

b. **Generate MEMORY.md content** following the schema:
   - Memory Categories:
     - Short-Term: session context, conversation history scope
     - Long-Term: user preferences, learned patterns, accumulated knowledge
   - Retention Rules: category, retention period, priority for each memory type
   - Context Management: max context window (token/message limits), summarization strategy, priority ordering

c. **Append generated content** to {outputFile} under the agent's roster section:
   ```markdown
   ### {Agent Display Name} — Context Artifacts

   #### USER.md
   {generated USER.md content}

   #### MEMORY.md
   {generated MEMORY.md content}
   ```

**Subprocess optimization (Pattern 2):** For agent rosters > 3 agents, launch a subprocess per agent. Each subprocess receives the agent's brief data, identity artifacts, and artifact schemas, and returns the generated USER.md and MEMORY.md content. If subprocess unavailable, generate sequentially in main thread.

### 3. Cross-Reference Memory Architecture

After all agents have context artifacts:
- Verify that memory categories align with the system's memory architecture from the brief
- Ensure shared memory references are consistent (if Agent A writes to shared memory, Agent B's MEMORY.md reflects it can read from there)
- Validate that context window limits are realistic for each agent's role complexity
- Fix any inconsistencies

### 4. Present Summary

"**Context generation complete.**

**Agents processed:** {count}

| Agent | User Context Categories | Memory Strategy |
|-------|------------------------|-----------------|
| {agent-1} | {key context categories} | {short/long-term summary} |
| {agent-2} | {key context categories} | {short/long-term summary} |
...

**Artifacts generated per agent:** USER.md, MEMORY.md
**Memory architecture consistency:** {verified/adjusted count} cross-references"

### 5. Present MENU OPTIONS

Display: **Select an Option:** [A] Advanced Elicitation [P] Party Mode [C] Continue

#### Menu Handling Logic:

- IF A: Execute {advancedElicitationTask}, and when finished redisplay the menu
- IF P: Execute {partyModeWorkflow}, and when finished redisplay the menu
- IF C: Save all generated content to {outputFile}, update frontmatter stepsCompleted to include 'step-03-context', update Generation Progress table (mark step 03 as Complete), then load, read entire file, then execute {nextStepFile}
- IF Any other: help user, then [Redisplay Menu Options](#5-present-menu-options)

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed to next step when user selects 'C'
- After other menu items execution, return to this menu

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN C is selected and all agent context artifacts have been appended to {outputFile} will you then load and read fully `{nextStepFile}` to execute skill generation.

---

## SYSTEM SUCCESS/FAILURE METRICS

### SUCCESS:

- USER.md content generated for every agent in the roster
- MEMORY.md content generated for every agent in the roster
- Schemas followed strictly
- Context categories tailored to each agent's identity and role
- Memory architecture cross-references verified and consistent
- All content appended to workspace-plan.md
- stepsCompleted updated

### SYSTEM FAILURE:

- Skipping any agent in the roster
- Not following USER.md or MEMORY.md schemas
- Generic context categories not tailored to agent identity
- Inconsistent memory architecture references between agents
- Generating artifacts beyond context (skills, config, etc.)
- Not appending content to workspace-plan.md

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
