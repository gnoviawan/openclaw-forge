---
name: 'step-04-hardening-checks'
description: 'Verify security, resilience, and operational hardening'

nextStepFile: './step-05-report.md'
validationRules: '../data/workspace-validation-rules.md'
validationReportOutput: '{validationReportOutput}'
---

# Step 4: Hardening Checks

## STEP GOAL:

To verify that the workspace has proper security, resilience, and operational hardening — including memory directives, tool policies, boundaries, failover configuration, self-correction directives, and safety rules.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 🛑 DO NOT BE LAZY - CHECK EVERY HARDENING RULE
- 📖 CRITICAL: Read the complete step file before taking any action
- 🔄 CRITICAL: When loading next step, ensure entire file is read
- ✅ Validation does NOT stop for user input - auto-proceed through all checks
- ⚙️ If any instruction references a subprocess, subagent, or tool you do not have access to, you MUST still achieve the outcome in your main context
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`

### Role Reinforcement:

- ✅ You are the **Quality Assurance** specialist — security and resilience audit
- ✅ Read files deeply to verify hardening directives are present and meaningful

### Step-Specific Rules:

- 🎯 Focus ONLY on hardening checks
- 🚫 FORBIDDEN to re-check structural or coherence issues
- 💬 Report findings as [PASS], [FAIL], or [WARN] per check
- 📖 You MUST actually read AGENTS.md, SOUL.md, and openclaw.json content

## EXECUTION PROTOCOLS:

- 🎯 Load validation rules and check every hardening rule
- 📖 Read AGENTS.md, SOUL.md, and openclaw.json content
- 💾 Append findings to {validationReportOutput}
- 📖 Save report before loading next step
- 🚫 DO NOT halt for user input

## CONTEXT BOUNDARIES:

- Previous steps confirmed file existence and coherence
- Focus on whether hardening directives are PRESENT and MEANINGFUL
- If a required file was missing, mark checks involving it as [SKIP]
- Dependencies: steps 02 and 03 must be complete

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise.

### 1. Load Validation Rules

Load {validationRules} and focus on the "## Hardening Checks" section.

### 2. Read Workspace Files

Read (if they exist and haven't been read already):
- AGENTS.md — full content
- SOUL.md — full content
- openclaw.json — full content (if exists)

### 3. Check Memory Directives

Read AGENTS.md and check for memory management directives:

**Daily log directive:**
- Search for references to daily logs: "memory/YYYY-MM-DD.md", "daily notes", "Daily notes", "daily logs"
- Verify there are instructions about writing to daily log files
- Record: [PASS] or [FAIL]

**Long-term memory directive:**
- Search for references to MEMORY.md as long-term/curated storage
- Verify there are instructions about maintaining MEMORY.md
- Record: [PASS] or [FAIL]

**Write-it-down rule:**
- Search for the "write it down" / "no mental notes" pattern or equivalent
- Look for: "write it down", "mental notes", "Text > Brain", or similar
- Record: [PASS] or [WARN]

### 4. Check Memory Backend Configuration

**If openclaw.json exists:**
- Check if `memory` section is present
- Check if `backend` is configured (or explicitly disabled)
- Record: [PASS] if configured, [WARN] if missing

**If openclaw.json does not exist:**
- Record: [WARN] "No openclaw.json found — cannot verify memory backend"

### 5. Check Tool Policies

**If openclaw.json exists:**
- Check if `tools` section is present
- Check if a `profile` is set or explicit `allow`/`deny` rules exist
- Record: [PASS] if configured, [WARN] if missing

**If openclaw.json does not exist:**
- Record: [WARN] "No openclaw.json found — cannot verify tool policies"

### 6. Check Boundaries

Read SOUL.md Boundaries section:

**Privacy boundaries:**
- Search for privacy-related directives: "private", "privacy", "stay private", "confidential"
- Record: [PASS] or [FAIL]

**External action rules:**
- Search for external action rules: "ask before", "ask first", "external", "sending", "emails", "public"
- Record: [PASS] or [FAIL]

**Scope limits:**
- Search for scope/domain limitations in SOUL.md or AGENTS.md
- Look for: references to what the agent should and should NOT do
- Record: [PASS] or [WARN]

### 7. Check Failover Configuration

**If openclaw.json exists:**
- Check if `model` section has `fallbacks` array
- If agent is customer-facing (bound to channels), failover is more critical
- Record: [PASS] if configured, [WARN] if missing

**If openclaw.json does not exist:**
- Record: [WARN] "No openclaw.json found — cannot verify failover"

### 8. Check Self-Correction Directives

Read AGENTS.md for self-correction patterns:

**Error journaling:**
- Search for: "mistake", "error", "wrong", "correction", "document it", "log"
- Verify there are instructions about recording errors
- Record: [PASS] or [WARN]

**Learning loop:**
- Search for: "review", "past mistakes", "recurring", "patterns", "adjust"
- Verify there are instructions about learning from past errors
- Record: [PASS] or [WARN]

### 9. Check Safety Directives

Read AGENTS.md Safety section:

**No-exfiltration rule:**
- Search for: "exfiltrate", "private data", "don't exfiltrate", "Don't exfiltrate"
- Verify there is a clear directive against data exfiltration
- Record: [PASS] or [FAIL]

**Destructive command warning:**
- Search for: "destructive", "rm", "trash", "delete", "careful"
- Verify there are guidelines about destructive operations
- Record: [PASS] or [WARN]

### 10. Check Group Chat Behavior

**If agent is bound to group channels (check openclaw.json bindings):**
- Read AGENTS.md for group chat behavior rules
- Search for: "group chat", "group", "when to speak", "stay silent", "HEARTBEAT_OK"
- Record: [PASS] or [WARN]

**If not bound to group channels:**
- Record: [PASS] — not applicable

### 11. Append Findings to Report

Replace the "## Hardening Checks" section in {validationReportOutput} with actual findings. Use a subsection per category (Memory Directives, Memory Backend, Tool Policies, Boundaries, Failover, Self-Correction, Safety, Group Chat Behavior) with a table of `| Check | Status | Details |` per subsection. End with:

`**Hardening Summary:** {pass_count} passed, {fail_count} failed, {warn_count} warnings`

### 12. Save Report and Auto-Proceed

"**Hardening checks complete.** {pass_count} passed, {fail_count} failed, {warn_count} warnings. Proceeding to final report..."

Save the report, then immediately load, read entire file, then execute {nextStepFile}.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- Every hardening rule checked
- AGENTS.md, SOUL.md, openclaw.json read and analyzed
- Memory, tool, boundary, failover, self-correction, safety all checked
- Findings appended to report
- Report saved before proceeding
- Auto-proceeded to next step

### ❌ SYSTEM FAILURE:

- Skipping any hardening check
- Not reading file contents deeply
- Not saving report before proceeding
- Halting for user input

**Master Rule:** Hardening checks require READING and SEARCHING file contents for specific directives. DO NOT BE LAZY. Check EVERY rule. Auto-proceed.
