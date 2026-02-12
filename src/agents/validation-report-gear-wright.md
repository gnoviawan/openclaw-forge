---
agentName: 'gear-wright'
hasSidecar: false
module: 'ocf'
agentFile: '_bmad-output/bmb-creations/gear-wright.agent.yaml'
validationDate: '2026-02-11'
stepsCompleted:
  - v-01-load-review.md
  - v-02a-validate-metadata.md
  - v-02b-validate-persona.md
  - v-02c-validate-menu.md
  - v-02d-validate-structure.md
---

# Validation Report: Gear Wright (Cog)

## Agent Overview

**Name:** Cog
**Title:** Skills, Config & Assembly Engineer
**hasSidecar:** false
**module:** ocf
**File:** `_bmad-output/bmb-creations/gear-wright.agent.yaml`

---

## Validation Findings

### Metadata Validation

**Status:** ✅ PASS

**Checks:**
- [x] id: `_bmad/ocf/agents/gear-wright/gear-wright.md` — kebab-case, path matches filename pattern
- [x] name: `Cog` — clear persona display name, distinct from title
- [x] title: `Skills, Config & Assembly Engineer` — concise functional description
- [x] icon: `⚙️` — single emoji, represents configuration/engineering
- [x] module: `ocf` — valid module code for OpenClaw Forge
- [x] hasSidecar: `false` — matches actual structure (no sidecar folder, no sidecar references)

**Detailed Findings:**

*PASSING:*
- All 6 required metadata fields present and non-empty
- id follows kebab-case convention with proper path structure
- name (Cog) is distinct from title (not duplicated)
- icon is single emoji matching agent's engineering purpose
- module code matches OCF module membership
- hasSidecar correctly set to false — no sidecar paths referenced anywhere in agent

*WARNINGS:*
- None

*FAILURES:*
- None

---

### Persona Validation

**Status:** ✅ PASS

**Checks:**
- [x] role: specific — "Skills, Config & Assembly Engineer" with clear scope
- [x] identity: defines character — "Precision engineer who turns designs into deployable reality"
- [x] communication_style: speech patterns only — "Precise and technical. Speaks in terms of configuration and structure."
- [x] principles: first principle activates domain knowledge — "Channel expert OpenClaw configuration engineering..."

**Detailed Findings:**

*PASSING:*
- All 4 persona fields present and populated
- Role is specific and functional (not generic "assistant")
- Role aligns with all 6 menu commands (skills, config, packaging)
- Identity defines character without leaking into role or communication
- Communication style focuses purely on speech patterns with example quote
- No forbidden words in communication_style (no "ensures", "experienced", "believes in")
- 5 principles — within recommended 3-7 range
- First principle activates expert domain knowledge per principlesCrafting.md pattern
- All principles are beliefs/philosophy, not job duties
- Field purity maintained: no cross-contamination between role/identity/style/principles
- Persona supports all menu capabilities consistently

*WARNINGS:*
- None

*FAILURES:*
- None

---

### Menu Validation

**Status:** ✅ PASS

**hasSidecar:** false

**Checks:**
- [x] Triggers follow `XX or fuzzy match on command` format — all 6 items correct
- [x] Descriptions start with `[XX]` code — all match trigger codes
- [x] No reserved codes (MH, CH, PM, DA) — codes used: SK, PH, VW, EC, PE, PI
- [x] Action handlers valid — all use `exec:` with `{project-root}` paths (module pattern)
- [x] Configuration appropriate — no sidecar references (hasSidecar: false)

**Detailed Findings:**

*PASSING:*
- Menu section properly formatted with 6 items
- All triggers use correct `XX or fuzzy match on command-name` format
- All 6 trigger codes are unique (SK, PH, VW, EC, PE, PI)
- No reserved codes (MH, CH, PM, DA) used
- All descriptions start with matching `[XX]` code
- All handlers use `exec:` pointing to OCF module workflow files
- All paths use `{project-root}` prefix (never relative)
- No sidecar references in handlers (correct for hasSidecar: false)
- Menu items align with agent's assembly/config/packaging role
- Menu scope appropriate — 6 commands covering full assembly lifecycle

*WARNINGS:*
- Agent defines both `prompts` (6 with IDs matching menu commands) and `exec` handlers. The prompts serve as inline documentation/fallback but the exec handlers will take precedence at runtime. Not a compliance issue but worth awareness.

*FAILURES:*
- None

---

### Structure Validation

**Status:** ✅ PASS

**Configuration:** Agent WITHOUT sidecar

**hasSidecar:** false

**Checks:**
- [x] Valid YAML syntax — parses without errors
- [x] Required sections present (metadata, persona, prompts, menu)
- [x] Field types correct (arrays, strings, booleans)
- [x] Consistent 2-space indentation throughout
- [x] Configuration appropriate structure — no sidecar artifacts

**Detailed Findings:**

*PASSING:*
- YAML parses cleanly with no syntax errors
- 2-space indentation used consistently throughout all 126 lines
- Special characters properly handled (& in title)
- No duplicate keys in any section
- All required sections present: agent.metadata (6 fields), agent.persona (4 fields), agent.prompts (6 entries), agent.menu (6 entries)
- No frontmatter included (correct — compiler adds it)
- No activation/XML blocks included (correct — compiler adds them)
- No MH/CH/PM/DA menu items (correct — compiler auto-injects)
- No rules section (correct — compiler adds it)
- hasSidecar: false with no sidecar-folder in metadata
- No critical_actions section (appropriate for stateless agent)
- No sidecar file references anywhere in agent
- Total size: 126 lines — well under 250 line recommendation
- All path references use `{project-root}` format

*WARNINGS:*
- None

*FAILURES:*
- None

---

### Sidecar Validation

**Status:** N/A

**hasSidecar:** false

**Checks:**
- [x] No sidecar-folder path in metadata — confirmed absent
- [x] No sidecar references in critical_actions — no critical_actions section present
- [x] No sidecar references in menu handlers — all exec paths point to OCF workflows, not sidecar files
- [x] No sidecar file references anywhere in agent YAML — clean

**Detailed Findings:**

*N/A (for agents WITHOUT sidecar):*
N/A — Agent has hasSidecar: false, no sidecar required. Confirmed zero sidecar path references across all agent sections (metadata, prompts, menu).

---

### Fix Applied

**Warning resolved:** Removed `prompts` section (6 entries). Agent now follows clean Module agent pattern with `exec` handlers only. Reduced from 126 to 57 lines.

---

## Final Result: ALL CHECKS PASSED — 0 Failures, 0 Warnings
