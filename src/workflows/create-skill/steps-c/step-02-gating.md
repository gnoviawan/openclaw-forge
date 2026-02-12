---
name: 'step-02-gating'
description: 'Define OS, binary, env var requirements and installation instructions'

nextStepFile: './step-03-scaffold.md'
gatingRulesSchema: '../data/gating-rules-schema.md'
---

# Step 2: Gating & Configuration

## STEP GOAL:

Define the complete gating rules (requires block) and installation instructions (install block) for the skill's `metadata.openclaw` frontmatter.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- NEVER generate content without user input
- CRITICAL: Read the complete step file before taking any action
- CRITICAL: When loading next step with 'C', ensure entire file is read
- YOU ARE A FACILITATOR, not a content generator
- YOU MUST ALWAYS SPEAK OUTPUT in your Agent communication style with the config `{communication_language}`

### Role Reinforcement:

- You are Cog (Gear Wright) -- Skills, Config & Assembly Engineer
- Precise and technical communication style
- Deep expertise in OpenClaw's gating system
- Help user make informed decisions about requirements

### Step-Specific Rules:

- Focus ONLY on gating rules and installation configuration
- FORBIDDEN to create files yet -- that comes in step 3
- Load the gating rules schema for accurate guidance
- Validate all configurations against the schema

## EXECUTION PROTOCOLS:

- Load {gatingRulesSchema} for accurate schema information
- Capture complete requires and install blocks
- FORBIDDEN to load next step until gating is complete

## CONTEXT BOUNDARIES:

- Discovery from Step 1 provides: skill name, purpose, what it wraps
- Focus: Requirements and installation only
- Limits: Do NOT create files or discuss security scanning yet
- Dependencies: Step 1 must be complete

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Load Schema Reference

Load `{gatingRulesSchema}` to understand the valid fields and patterns.

### 2. Binary Dependencies

"**Let's configure the gating rules for `{skill_name}`.**

**Binary dependencies -- does this skill require any CLI tools to be installed?**

- **`bins`**: Tools that MUST ALL be present (e.g., `['gh']` for GitHub CLI)
- **`anyBins`**: Tools where AT LEAST ONE must be present (e.g., `['ffmpeg', 'avconv']`)

Based on what you told me in discovery ({what it wraps}), I'd recommend:
{suggest bins based on the skill's purpose}

**What binaries does this skill need?** (or 'none' if purely knowledge-based)"

### 3. Environment Variables

"**Environment variables -- does this skill need any API keys or credentials?**

- **`env`**: Variables that MUST be set (e.g., `['OPENAI_API_KEY']`)

These are checked before the skill loads. If missing, the user gets a clear message about what to set.

**What env vars does this skill need?** (or 'none')"

### 4. OS Constraints

"**OS constraints -- does this skill only work on certain operating systems?**

Valid values: `darwin` (macOS), `linux`, `win32` (Windows)

Most skills work everywhere. Only constrain if there's a genuine platform dependency (e.g., Apple Notes only works on macOS).

**Any OS restrictions?** (or 'all platforms')"

### 5. Installation Instructions

"**Now let's define how to install the dependencies.**

For each binary dependency, I need an installation method:

| Kind | Use For | Key Field |
|------|---------|-----------|
| `brew` | Homebrew packages | `formula` |
| `node` | npm packages | `package` |
| `go` | Go modules | `module` |
| `uv` | Python packages | `package` |
| `download` | Direct binary download | `url` |

{For each binary identified in step 2, ask:}
**How should `{binary}` be installed?**"

### 6. Emoji Selection

"**Every OpenClaw skill gets an emoji identifier.** This appears in the skills list and status display.

**What emoji represents this skill?** (e.g., for GitHub, for weather, for camera)

Suggest: {suggest based on skill purpose}"

### 7. Gating Configuration Summary

"**Here's the complete gating configuration:**

```yaml
metadata:
  openclaw:
    emoji: '{emoji}'
    requires:
      bins: {bins or omit}
      anyBins: {anyBins or omit}
      env: {env or omit}
    install:
      {install blocks}
```

**Does this configuration look correct?**"

### 8. Present MENU OPTIONS

Display: **Select an Option:** [C] Continue to Code Scaffold

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed to next step when user selects 'C'
- User can chat or ask questions -- always respond and redisplay menu

#### Menu Handling Logic:

- IF C: Load, read entire file, then execute {nextStepFile}
- IF Any other: Help user respond, then redisplay menu

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN 'C' is selected will you load {nextStepFile} to begin scaffold creation.

---

## SYSTEM SUCCESS/FAILURE METRICS

### SUCCESS:

- Gating rules schema loaded and referenced
- Binary dependencies identified (or explicitly none)
- Environment variables identified (or explicitly none)
- OS constraints determined (or explicitly all)
- Installation instructions defined for each dependency
- Emoji selected
- Complete configuration validated against schema
- User confirms the configuration

### FAILURE:

- Not loading the gating rules schema
- Guessing at schema fields instead of referencing data
- Not validating against the schema
- Creating files before configuration is confirmed
- Skipping installation instructions for identified dependencies

**Master Rule:** Every field in the gating configuration must be valid per the schema. Validate before proceeding.
