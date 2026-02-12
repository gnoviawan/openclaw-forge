---
agentName: 'Anima'
hasSidecar: false
module: 'ocf'
agentFile: '_bmad-output/bmb-creations/soul-smith.agent.yaml'
validationDate: '2026-02-11'
stepsCompleted:
  - v-01-load-review.md
  - v-02a-validate-metadata.md
  - v-02b-validate-persona.md
  - v-02c-validate-menu.md
  - v-02d-validate-structure.md
  - v-02e-validate-sidecar.md
  - v-03-summary.md
---

# Validation Report: Anima (Soul Smith)

## Agent Overview

**Name:** Anima
**hasSidecar:** false
**module:** ocf
**File:** _bmad-output/bmb-creations/soul-smith.agent.yaml

---

## Validation Findings

### Metadata Validation

**Status:** PASS

**Checks:**
- [x] id: kebab-case, no spaces, unique — `_bmad/ocf/agents/soul-smith/soul-smith.md`
- [x] name: clear display name — `Anima` (persona name, not title or filename)
- [x] title: concise function description — `Persona & Identity Designer`
- [x] icon: appropriate emoji/symbol — `✨` (single emoji, represents creative identity work)
- [x] module: correct format — `ocf` (lowercase custom module code)
- [x] hasSidecar: matches actual usage — `false` (no sidecar folder present or needed)

**Detailed Findings:**

*PASSING:*
- All 6 required metadata fields present and non-empty
- id follows path convention with module prefix `_bmad/ocf/agents/`
- name and title are distinct (no duplication anti-pattern)
- Module code `ocf` is consistent with the OCF module membership
- hasSidecar correctly set to false — agent is stateless, output documents serve as artifacts

*WARNINGS:*
None

*FAILURES:*
None

---

### Persona Validation

**Status:** PASS

**Checks:**
- [x] role: specific, not generic — defines Persona & Identity Designer function clearly
- [x] identity: defines who agent is — creative architect with character depth
- [x] communication_style: speech patterns only — metaphors, tone, question patterns without expertise leakage
- [x] principles: first principle activates domain knowledge — "Channel expert persona design wisdom..."

**Detailed Findings:**

*PASSING:*
- Role is specific and functional — describes WHAT Anima does (SOUL.md, AGENTS.md, USER.md creation)
- Identity is character-focused — describes WHO Anima is (creative identity architect, tapestry metaphor)
- Communication style is pure expression — defines HOW Anima speaks (empathetic, identity metaphors, deep questions)
- Principles are actionable decision frameworks — 6 principles, all specific and non-vague
- First principle activates expert domain knowledge (persona design wisdom)
- No field purity violations detected — role has no personality, identity has no job description, communication has no expertise
- All four fields align cohesively without contradiction or overlap
- Persona supports the three menu commands (CS, SA, EA)

*WARNINGS:*
None

*FAILURES:*
None

---

### Menu Validation

**Status:** PASS

**hasSidecar:** false

**Checks:**
- [x] Triggers follow `XX or fuzzy match on command` format
- [x] Descriptions start with `[XX]` code
- [x] No reserved codes (MH, CH, PM, DA)
- [x] Action handlers valid — all use `exec:` with `{project-root}/...` paths
- [x] Configuration appropriate menu links — no sidecar references (correct for hasSidecar: false)

**Detailed Findings:**

*PASSING:*
- CS: trigger format correct, description starts with `[CS]`, exec path uses `{project-root}/_bmad/ocf/workflows/`
- SA: trigger format correct, description starts with `[SA]`, exec path uses `{project-root}/_bmad/ocf/workflows/`
- EA: trigger format correct, description starts with `[EA]`, exec path uses `{project-root}/_bmad/ocf/workflows/`
- All trigger codes are unique within agent
- No reserved codes used
- All handlers use `exec:` (correct for module agent)
- Menu scope is appropriate — 3 commands matching the spec's planned capabilities
- Menu items align with agent's role/purpose

*WARNINGS:*
None

*FAILURES:*
None

---

### Structure Validation

**Status:** PASS

**Configuration:** Agent WITHOUT sidecar

**hasSidecar:** false

**Checks:**
- [x] Valid YAML syntax
- [x] Required fields present (metadata, persona, menu)
- [x] Field types correct (arrays, strings, booleans)
- [x] Consistent 2-space indentation
- [x] Configuration appropriate structure

**Detailed Findings:**

*PASSING:*
- YAML parses without errors
- 2-space indentation consistent throughout
- No duplicate keys in any section
- All required sections present: metadata (6 fields), persona (4 fields), menu (3 items)
- No frontmatter present (correct — compiler adds it)
- No activation XML present (correct — compiler adds it)
- No MH/CH/PM/DA menu items (correct — auto-injected by compiler)
- No rules section (correct — compiler adds it)
- No menu-handlers section (correct — compiler adds it)
- Total size: 40 lines — well under 250-line limit for hasSidecar: false
- No sidecar-folder path in metadata (correct)
- No critical_actions section (correct — optional for hasSidecar: false, none needed)
- Follows exact same structure as reference forge-master.agent.yaml

*WARNINGS:*
None

*FAILURES:*
None

---

### Sidecar Validation

**Status:** N/A

**hasSidecar:** false

**Checks:**
- [x] No sidecar-folder path in metadata (confirmed)
- [x] No sidecar references in critical_actions (confirmed — no critical_actions section)
- [x] No sidecar references in menu handlers (confirmed — all exec paths reference workflows, not sidecar)

**Detailed Findings:**

*N/A (for agents WITHOUT sidecar):*
N/A — Agent has hasSidecar: false, no sidecar required. Confirmed no sidecar references exist anywhere in the agent YAML.

---

## Overall Summary

| Section | Status |
|---------|--------|
| Metadata | PASS |
| Persona | PASS |
| Menu | PASS |
| Structure | PASS |
| Sidecar | N/A |

**Overall Result: PASS — Agent is fully compliant with BMAD standards**
