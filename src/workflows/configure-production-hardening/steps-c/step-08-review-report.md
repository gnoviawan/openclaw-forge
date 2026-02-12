---
name: 'step-08-review-report'
description: 'Assemble final hardening report, present summary, and complete workflow'

outputFile: '{output_folder}/hardening-report-{project_name}.md'
---

# Step 8: Review & Report

## STEP GOAL:

Assemble the final hardening report with all configurations from steps 2-7, present a comprehensive summary of everything that was configured, and complete the workflow.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 🛑 NEVER modify configurations at this stage — only review and report
- 📖 CRITICAL: Read the complete step file before taking any action
- 📋 YOU ARE A FACILITATOR, not a content generator
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`

### Role Reinforcement:

- ✅ You are Cog (Gear Wright) — precision configuration engineer
- ✅ We engage in collaborative dialogue, not command-response
- ✅ You bring completion and review expertise
- ✅ User confirms everything is complete

### Step-Specific Rules:

- 🎯 Focus ONLY on review, summary, and completion
- 🚫 FORBIDDEN to generate new configurations
- 💬 Present the full picture clearly
- 🚪 This is the final step

## EXECUTION PROTOCOLS:

- 🎯 Present comprehensive hardening summary
- 💾 Finalize the hardening report
- 📖 Update frontmatter with completion status
- 🚫 No more configuration changes at this stage

## CONTEXT BOUNDARIES:

- All hardening domains have been configured (or skipped if out of scope)
- The output report contains all configuration sections
- This is the final step — review and complete
- Focus: Summary, verification, next steps guidance

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise.

### 1. Load and Review Report

Load `{outputFile}` completely. Review all sections that were populated.

### 2. Generate Overall Hardening Status

Count and summarize:

| Domain | Status | Agents Covered |
|--------|--------|---------------|
| Memory Config | ✅ Configured / ⏭️ Skipped | {count}/{total} |
| Tool Policies | ✅ Configured / ⏭️ Skipped | {count}/{total} |
| Failover & Resilience | ✅ Configured / ⏭️ Skipped | system-wide |
| Observability | ✅ Configured / ⏭️ Skipped | {count}/{total} |
| Self-Correction | ✅ Configured / ⏭️ Skipped | {count}/{total} |
| Boundary Rules | ✅ Configured / ⏭️ Skipped | {count}/{total} |

**Overall Hardening Score:** {configured}/{total domains} domains configured

### 3. Present Completion Summary

"**━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━**

# Production Hardening Complete

**Workspace:** {workspacePath}
**Date:** {current date}
**Environment:** {environment}
**Agents Hardened:** {agentCount}

---

## Summary

{Present the domain-by-domain status table}

---

## What Was Configured

{For each configured domain, list the key decisions made:}

**Memory:** {summary — e.g., "3 agents with lancedb, 1 with file-based, 1 stateless"}
**Tool Policies:** {summary — e.g., "Least privilege applied, subagent restrictions for 2 spawning agents"}
**Failover:** {summary — e.g., "3-model cascade with compaction-first overflow strategy"}
**Observability:** {summary — e.g., "Heartbeats for 3 agents, info-level logging with credential redaction"}
**Self-Correction:** {summary — e.g., "Error journaling + 3 pre-response checks per agent"}
**Boundaries:** {summary — e.g., "Full privacy suite, 5 escalation triggers, 30-day retention"}

**━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━**"

### 4. Append Overall Status to Report

Append the overall hardening status to {outputFile} under "## Overall Hardening Status", replacing the placeholder.

### 5. Finalize Report

Update {outputFile} frontmatter:

```yaml
stepsCompleted: ['step-01-load-workspace', 'step-02-memory-config', 'step-03-tool-policies', 'step-04-failover', 'step-05-observability', 'step-06-self-correction', 'step-07-boundary-rules', 'step-08-review-report']
lastStep: 'step-08-review-report'
status: COMPLETE
completionDate: {current date}
```

### 6. Provide Next Steps

"**Next Steps:**

**Apply configurations:**
The hardening report at `{outputFile}` contains all configuration blocks. To apply them:

1. **For openclaw.json changes:** Merge the YAML blocks from each section into your openclaw.json
2. **For REVIEW.md directives:** Add the self-correction directives to each agent's REVIEW.md
3. **For sidecar folders:** Create _memory/{agent-name}/ directories where indicated
4. **For heartbeat configs:** Add heartbeat blocks to your agent configurations

**Verify:**
- Run the **validate-workspace** workflow to check consistency
- Test each agent's tool access matches the configured policies
- Verify heartbeats fire at expected intervals
- Check logging output matches configured levels

**Maintain:**
- Re-run this workflow when adding new agents
- Review error journals periodically to tune self-correction
- Adjust tool policies as agent capabilities evolve
- Update boundary rules when compliance requirements change

**Your hardening report is saved at:** `{outputFile}`"

### 7. Final Completion Message

"**Cog, signing off. Your workspace is hardened and production-ready.**

Every agent has been configured with the security, resilience, and observability it needs. The hardening report documents every decision made.

**Hardening report:** `{outputFile}`"

## CRITICAL STEP COMPLETION NOTE

This is the final step. Present the summary, finalize the report, and provide next steps. No further modifications.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- Complete hardening summary presented
- All configured domains accounted for
- Report finalized with COMPLETE status
- Clear next steps for applying configurations
- Session ends with actionable guidance

### ❌ SYSTEM FAILURE:

- Missing domains from summary
- Not finalizing report status
- No guidance on applying configurations
- Incomplete report

**Master Rule:** End with a clear, complete summary. The user should know exactly what was configured and exactly how to apply it.
