---
name: 'step-02-structural-checks'
description: 'Verify all required files exist and are well-formed'

nextStepFile: './step-03-coherence-checks.md'
validationRules: '../data/workspace-validation-rules.md'
validationReportOutput: '{validationReportOutput}'
---

# Step 2: Structural Checks

## STEP GOAL:

To verify all required workspace files exist and are well-formed, checking presence of required files, optional files, directories, and that files which should NOT exist are absent.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 🛑 DO NOT BE LAZY - CHECK EVERY FILE AND DIRECTORY
- 📖 CRITICAL: Read the complete step file before taking any action
- 🔄 CRITICAL: When loading next step, ensure entire file is read
- ✅ Validation does NOT stop for user input - auto-proceed through all checks
- ⚙️ If any instruction references a subprocess, subagent, or tool you do not have access to, you MUST still achieve the outcome in your main context
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`

### Role Reinforcement:

- ✅ You are the **Quality Assurance** specialist — thorough, systematic
- ✅ Check EVERY item in the rules, do not skip any

### Step-Specific Rules:

- 🎯 Focus ONLY on structural checks (file existence and well-formedness)
- 🚫 FORBIDDEN to check cross-artifact consistency — that's step 03
- 🚫 FORBIDDEN to check hardening — that's step 04
- 💬 Report findings as [PASS], [FAIL], or [WARN] per check

## EXECUTION PROTOCOLS:

- 🎯 Load validation rules and check every structural rule
- 💾 Append findings to {validationReportOutput}
- 📖 Save report before loading next step
- 🚫 DO NOT halt for user input - validation runs to completion

## CONTEXT BOUNDARIES:

- Workspace inventory from step 01 is available
- Focus ONLY on file/directory existence and basic well-formedness
- Do NOT read file contents deeply — just check they exist and have structure
- Dependencies: step 01 must be complete (workspace inventoried, report initialized)

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise.

### 1. Load Validation Rules

Load {validationRules} and focus on the "## Structural Checks" section.

### 2. Check Required Files

For each file in the Required Files table:

**SOUL.md:**
- Check: exists in workspace root
- Check: is non-empty (has content beyond frontmatter)
- Record: [PASS] or [FAIL] with details

**AGENTS.md:**
- Check: exists in workspace root
- Check: is non-empty
- Record: [PASS] or [FAIL] with details

**USER.md:**
- Check: exists in workspace root
- Record: [PASS] or [FAIL] with details

**IDENTITY.md:**
- Check: exists in workspace root
- If absent: check if SOUL.md has an identity/name section
- Record: [PASS] or [WARN] with details

### 3. Check Optional Files

For each file in the Optional Files table:

**TOOLS.md:**
- Check: exists in workspace root
- Record: [PASS] or [WARN] "Not found — consider adding if agent uses tools"

**HEARTBEAT.md:**
- Check: exists in workspace root
- Record: [PASS] or [WARN] "Not found — consider adding if heartbeat is configured"

**MEMORY.md:**
- Check: exists in workspace root
- Record: [PASS] or [WARN] "Not found — consider adding for long-term memory"

### 4. Check Files That Should NOT Exist

**BOOTSTRAP.md:**
- Check: does NOT exist in workspace root
- If exists: [WARN] "BOOTSTRAP.md still present — should be deleted after first run"
- If absent: [PASS]

### 5. Check Required Directories

**memory/:**
- Check: directory exists
- Record: [PASS] or [WARN] with details

### 6. Check Optional Directories

**skills/:**
- Check: directory exists
- Record: [PASS] or [WARN] with details (note if skill references found but no directory)

### 7. Check Well-Formedness

For each existing file, do a basic structural check:

**SOUL.md:**
- Has `##` level sections (Core Truths, Boundaries, etc.)
- Record: [PASS] or [WARN]

**AGENTS.md:**
- Has `##` level sections (Every Session, Memory, Safety, etc.)
- Record: [PASS] or [WARN]

**USER.md:**
- Is non-empty (has some content)
- Record: [PASS] or [WARN]

### 8. Append Findings to Report

Replace the "## Structural Checks" section in {validationReportOutput} with actual findings:

```markdown
## Structural Checks

### Required Files
| File | Status | Details |
|------|--------|---------|
| SOUL.md | [PASS/FAIL] | {details} |
| AGENTS.md | [PASS/FAIL] | {details} |
| USER.md | [PASS/FAIL] | {details} |
| IDENTITY.md | [PASS/WARN] | {details} |

### Optional Files
| File | Status | Details |
|------|--------|---------|
| TOOLS.md | [PASS/WARN] | {details} |
| HEARTBEAT.md | [PASS/WARN] | {details} |
| MEMORY.md | [PASS/WARN] | {details} |

### Prohibited Files
| File | Status | Details |
|------|--------|---------|
| BOOTSTRAP.md | [PASS/WARN] | {details} |

### Directories
| Directory | Status | Details |
|-----------|--------|---------|
| memory/ | [PASS/WARN] | {details} |
| skills/ | [PASS/WARN] | {details} |

### Well-Formedness
| File | Status | Details |
|------|--------|---------|
| SOUL.md structure | [PASS/WARN] | {details} |
| AGENTS.md structure | [PASS/WARN] | {details} |
| USER.md content | [PASS/WARN] | {details} |

**Structural Summary:** {pass_count} passed, {fail_count} failed, {warn_count} warnings
```

### 9. Save Report and Auto-Proceed

"**Structural checks complete.** {pass_count} passed, {fail_count} failed, {warn_count} warnings. Proceeding to coherence checks..."

Save the report, then immediately load, read entire file, then execute {nextStepFile}.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- Every required file checked
- Every optional file checked
- Every directory checked
- Well-formedness assessed
- Findings appended to report
- Report saved before proceeding
- Auto-proceeded to next step

### ❌ SYSTEM FAILURE:

- Skipping any file check
- Not checking well-formedness
- Not saving report before proceeding
- Halting for user input

**Master Rule:** Validation is systematic and thorough. DO NOT BE LAZY. Check EVERY file and directory. Auto-proceed.
