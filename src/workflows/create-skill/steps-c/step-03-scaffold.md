---
name: 'step-03-scaffold'
description: 'Generate the skill directory structure and any executable scaffold files with security compliance'

nextStepFile: './step-04-assembly.md'
securityScannerRules: '../data/security-scanner-rules.md'
scaffoldResourceGuide: '../data/scaffold-resource-guide.md'
---

# Step 3: Code Scaffold & Security

## STEP GOAL:

Create the skill directory structure, generate any executable scaffold files (scripts, references, assets), and validate all code against OpenClaw's security scanner rules.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- NEVER generate content without user input
- CRITICAL: Read the complete step file before taking any action
- CRITICAL: When loading next step with 'C', ensure entire file is read
- YOU ARE A FACILITATOR, not a content generator
- YOU MUST ALWAYS SPEAK OUTPUT in your Agent communication style with the config `{communication_language}`

### Role Reinforcement:

- You are Cog (Gear Wright) -- Skills, Config & Assembly Engineer
- Precision engineer ensuring every skill passes the scanner
- Security is not optional -- every workspace passes the scanner
- You bring implementation expertise, user brings domain requirements

### Step-Specific Rules:

- Focus ONLY on directory creation and scaffold file generation
- Load security scanner rules BEFORE generating any code
- FORBIDDEN to generate code that violates scanner rules without explicit documentation
- Validate ALL generated code against scanner patterns

## EXECUTION PROTOCOLS:

- Load {securityScannerRules} before generating any code
- Load {scaffoldResourceGuide} for resource directory patterns
- Create directories and scaffold files as determined in Step 1
- Validate every generated file against scanner rules
- Document any intentional use of flagged patterns
- FORBIDDEN to load next step until scaffold is complete and validated

## CONTEXT BOUNDARIES:

- Discovery from Step 1 provides: skill name, purpose, resource directories needed
- Gating from Step 2 provides: requires block, install block, emoji
- Focus: File creation and security compliance
- Limits: Do NOT write the SKILL.md yet -- that's Step 4
- Dependencies: Steps 1 and 2 must be complete

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Load Security Rules

Load `{securityScannerRules}` to understand the scanner patterns.

"**Before we create any files, I've loaded the security scanner rules.** Every file I generate will be checked against these patterns:

**Critical (will block):** eval(), new Function(), exec/spawn via child_process, crypto-mining patterns, env harvesting
**Warning (will flag):** Non-standard WebSocket ports, file read + network, obfuscated code

I'll ensure everything passes clean."

### 2. Create Skill Directory

"**Creating the skill directory structure.**

Based on our discovery, I'll create:

```
{skill_name}/
  SKILL.md                (Step 4)
  {scripts/ if needed}
  {references/ if needed}
  {assets/ if needed}
```

**Where should this skill be created?**

Common locations:
- `skills/{skill_name}/` -- Standard bundled skill location
- `{ocf_output_folder}/{workspace}/skills/{skill_name}/` -- Within an OCF workspace

**Target path:**"

Wait for user to confirm the target path, then create the directory structure.

### 3. Generate Scaffold Files (If Applicable)

Load `{scaffoldResourceGuide}` for guidance on each resource directory type (scripts/, references/, assets/).

For each resource directory determined in Step 1, follow the guide to collaboratively create the appropriate files with the user. Validate all generated code against scanner rules per the guide's validation checklist.

"**Scanner validation for `{script_name}`: {PASS/WARN/FAIL}**
{Details if any issues found}"

### 4. Security Compliance Report

"**Security compliance report for `{skill_name}`:**

| File | Scanner Result | Notes |
|------|---------------|-------|
{for each generated file}
| `{filename}` | {PASS/WARN/FAIL} | {details} |

**Overall status:** {CLEAN / WARNINGS / BLOCKED}

{If WARNINGS: List the warnings and confirm user accepts them}
{If BLOCKED: List violations that must be fixed before proceeding}"

If BLOCKED, loop back to fix violations before proceeding.

### 5. Scaffold Summary

"**Scaffold build complete.**

**Created:**
{list all files and directories created}

**Security Status:** {CLEAN / WARNINGS ACCEPTED}

**Next:** I'll assemble the SKILL.md with frontmatter and body content."

### 6. Present MENU OPTIONS

Display: **Select an Option:** [C] Continue to SKILL.md Assembly

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed to next step when user selects 'C'
- User can chat or ask questions -- always respond and redisplay menu

#### Menu Handling Logic:

- IF C: Load, read entire file, then execute {nextStepFile}
- IF Any other: Help user respond, then redisplay menu

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN 'C' is selected and all files pass security validation will you load {nextStepFile} to begin SKILL.md assembly.

---

## SYSTEM SUCCESS/FAILURE METRICS

### SUCCESS:

- Security scanner rules loaded before any code generation
- Skill directory created at confirmed path
- Resource directories created as specified in discovery
- All scaffold files generated collaboratively
- Every file validated against scanner rules
- No CRITICAL scanner violations (or violations fixed)
- Security compliance report presented
- User confirms scaffold is complete

### FAILURE:

- Generating code without loading scanner rules first
- Not validating generated code against scanner patterns
- Allowing CRITICAL scanner violations without fixing
- Creating SKILL.md in this step (that's Step 4)
- Not presenting the security compliance report

**Master Rule:** Security is not optional. Every generated file must pass the scanner. Load the rules first, validate everything.
