---
name: 'step-03-coherence-checks'
description: 'Validate cross-artifact consistency across workspace files'

nextStepFile: './step-04-hardening-checks.md'
validationRules: '../data/workspace-validation-rules.md'
validationReportOutput: '{validationReportOutput}'
---

# Step 3: Coherence Checks

## STEP GOAL:

To validate cross-artifact consistency — ensuring that SOUL.md personality aligns with AGENTS.md directives, session startup references are complete, skill references resolve to actual files, identity is consistent, and bindings are complete.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 🛑 DO NOT BE LAZY - READ AND CROSS-REFERENCE EVERY ARTIFACT
- 📖 CRITICAL: Read the complete step file before taking any action
- 🔄 CRITICAL: When loading next step, ensure entire file is read
- ✅ Validation does NOT stop for user input - auto-proceed through all checks
- ⚙️ If any instruction references a subprocess, subagent, or tool you do not have access to, you MUST still achieve the outcome in your main context
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`

### Role Reinforcement:

- ✅ You are the **Quality Assurance** specialist — cross-referencing artifacts
- ✅ Read files deeply to understand their content relationships

### Step-Specific Rules:

- 🎯 Focus ONLY on cross-artifact consistency
- 🚫 FORBIDDEN to check hardening — that's step 04
- 🚫 FORBIDDEN to re-check structural issues — that was step 02
- 💬 Report findings as [PASS], [FAIL], or [WARN] per check
- 📖 You MUST actually read the content of SOUL.md and AGENTS.md to perform these checks

## EXECUTION PROTOCOLS:

- 🎯 Load validation rules and check every coherence rule
- 📖 Read SOUL.md and AGENTS.md content for cross-referencing
- 💾 Append findings to {validationReportOutput}
- 📖 Save report before loading next step
- 🚫 DO NOT halt for user input

## CONTEXT BOUNDARIES:

- Structural checks from step 02 confirmed which files exist
- Focus on relationships BETWEEN files, not file existence
- If a required file was missing in step 02, mark coherence checks involving it as [SKIP] "File not found in structural checks"
- Dependencies: step 02 must be complete

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise.

### 1. Load Validation Rules

Load {validationRules} and focus on the "## Coherence Checks" section.

### 2. Read Workspace Files

Read the following files (if they exist):
- SOUL.md — full content
- AGENTS.md — full content
- IDENTITY.md — full content (if exists)
- TOOLS.md — full content (if exists)
- openclaw.json — full content (if exists)

List all directories under skills/ (if exists).

### 3. Check Personality-Directive Consistency

**SOUL.md Boundaries section:**
- Read SOUL.md and check for a "## Boundaries" section (or similar heading)
- Verify it is non-empty and contains actual boundary rules
- Record: [PASS] or [FAIL]

**Tone consistency:**
- Compare the tone/personality described in SOUL.md with directives in AGENTS.md
- Look for contradictions (e.g., SOUL says "be bold and take initiative" but AGENTS says "always ask permission for everything")
- Record: [PASS] or [WARN] with specific contradictions noted

### 4. Check Session Startup References

Read AGENTS.md and look for the session startup sequence (typically under "## Every Session" or "## First Run"):

**References SOUL.md:**
- Check if AGENTS.md instructs the agent to read SOUL.md at session start
- Look for: "Read SOUL.md", "Read `SOUL.md`", or equivalent
- Record: [PASS] or [FAIL]

**References USER.md:**
- Check if AGENTS.md instructs the agent to read USER.md at session start
- Look for: "Read USER.md", "Read `USER.md`", or equivalent
- Record: [PASS] or [FAIL]

**References memory files:**
- Check if AGENTS.md instructs the agent to read daily memory files
- Look for: "memory/YYYY-MM-DD.md", "daily notes", "memory files", or equivalent
- Record: [PASS] or [FAIL]

**References MEMORY.md:**
- Check if AGENTS.md mentions reading MEMORY.md (for main sessions)
- Record: [PASS] or [WARN]

### 5. Check Skill References

**Extract skill references:**
- Search AGENTS.md and TOOLS.md for mentions of skills or SKILL.md files
- List all referenced skill names

**Verify skill files exist:**
- For each referenced skill, check if a corresponding directory exists under skills/
- Within each skill directory, check for SKILL.md
- Record: [PASS] per matched skill, [FAIL] per unmatched reference

**Check for orphan skills:**
- List skill directories that are NOT referenced in any workspace file
- Record: [PASS] if none, [WARN] per orphan with directory name

### 6. Check Identity Consistency

**If both IDENTITY.md and SOUL.md exist:**
- Read the agent name from IDENTITY.md
- Check if SOUL.md references the same name (if any name is mentioned)
- Record: [PASS] or [WARN] if names don't match

**If only SOUL.md exists:**
- Record: [PASS] — no consistency issue possible

### 7. Check Binding Completeness

**If openclaw.json exists and has bindings:**
- For each binding that references this workspace's agent:
  - Verify binding has a `channel` defined
  - Verify binding has a target (`accountId` or `peer`)
  - Record: [PASS] per complete binding, [WARN] per incomplete binding

**If no openclaw.json or no bindings:**
- Record: [PASS] — no binding consistency issue

### 8. Append Findings to Report

Replace the "## Coherence Checks" section in {validationReportOutput} with actual findings:

```markdown
## Coherence Checks

### Personality-Directive Consistency
| Check | Status | Details |
|-------|--------|---------|
| SOUL.md Boundaries section | [PASS/FAIL] | {details} |
| Tone consistency (SOUL↔AGENTS) | [PASS/WARN] | {details} |

### Session Startup References
| Check | Status | Details |
|-------|--------|---------|
| AGENTS.md → SOUL.md | [PASS/FAIL] | {details} |
| AGENTS.md → USER.md | [PASS/FAIL] | {details} |
| AGENTS.md → memory files | [PASS/FAIL] | {details} |
| AGENTS.md → MEMORY.md | [PASS/WARN] | {details} |

### Skill References
| Check | Status | Details |
|-------|--------|---------|
| {skill_name} | [PASS/FAIL] | {found/not found at path} |
| Orphan skills | [PASS/WARN] | {list or "none"} |

### Identity Consistency
| Check | Status | Details |
|-------|--------|---------|
| IDENTITY↔SOUL name match | [PASS/WARN/SKIP] | {details} |

### Binding Completeness
| Check | Status | Details |
|-------|--------|---------|
| {binding_description} | [PASS/WARN] | {details} |

**Coherence Summary:** {pass_count} passed, {fail_count} failed, {warn_count} warnings
```

### 9. Save Report and Auto-Proceed

"**Coherence checks complete.** {pass_count} passed, {fail_count} failed, {warn_count} warnings. Proceeding to hardening checks..."

Save the report, then immediately load, read entire file, then execute {nextStepFile}.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- SOUL.md and AGENTS.md read and cross-referenced
- Session startup references verified
- All skill references checked
- Identity consistency verified
- Binding completeness checked
- Findings appended to report
- Report saved before proceeding
- Auto-proceeded to next step

### ❌ SYSTEM FAILURE:

- Not reading file contents (just checking existence)
- Skipping any coherence check
- Not cross-referencing between files
- Not saving report before proceeding
- Halting for user input

**Master Rule:** Coherence checks require READING and UNDERSTANDING file contents. DO NOT BE LAZY. Cross-reference everything. Auto-proceed.
