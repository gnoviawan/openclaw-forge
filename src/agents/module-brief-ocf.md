# Module Brief: OCF

**Date:** 2026-02-11
**Author:** Althio
**Module Code:** ocf
**Module Type:** Standalone
**Status:** Ready for Development

---

## Executive Summary

The **OpenClaw Forge (OCF)** is a BMAD-powered module that serves as an end-to-end agent factory for the OpenClaw platform. It takes users from initial concept -- "I want an agent that does X" -- through to a fully deployable, production-hardened multi-agent workspace complete with all artifacts: `AGENTS.md`, `SOUL.md`, `USER.md`, `MEMORY.md`, skills, `openclaw.json` configuration fragments, orchestration patterns, guardrails, and resilience configuration.

OCF eliminates the friction of manually constructing OpenClaw workspaces by providing guided workflows that understand OpenClaw's architecture deeply and generate coherent, interconnected agent systems that work together out of the box. Every generated workspace includes self-correction patterns, memory scaffolding, tool safety policies, resilience configuration, and observability setup -- not just structurally correct, but operationally hardened.

**Module Category:** Developer Tooling / Agent Infrastructure
**Target Users:** OpenClaw developers, agent designers, system integrators
**Complexity Level:** High

---

## Module Identity

### Module Code & Name

- **Code:** `ocf`
- **Name:** `OpenClaw Forge`

### Core Concept

A forge where raw ideas are shaped into fully-formed OpenClaw agent systems. Like a blacksmith's forge transforms raw metal into precision tools, OCF transforms concepts into production-ready multi-agent workspaces. Every artifact -- from persona files to routing configurations to memory scaffolds -- is crafted with coherence and purpose.

### Personality Theme

Industrial craftspersonship meets systems architecture. The agents speak with the confidence of master builders who understand every bolt and beam. There's a sense of creative power -- you're not just configuring files, you're forging intelligent systems that learn, self-correct, and operate safely.

---

## Module Type

**Type:** Standalone

OCF is an independent module focused on the domain of OpenClaw agent system creation. It does not extend an existing module -- it creates a new capability vertical: the automated generation of complete OpenClaw workspaces. It can be installed alongside any other BMAD modules and operates independently.

---

## Unique Value Proposition

**What makes this module special:**

- **Full-Stack Agent Generation** -- Not just one file at a time. OCF produces the complete workspace: AGENTS.md, SOUL.md, USER.md, MEMORY.md scaffolds, skills directory with SKILL.md files, openclaw.json configuration fragments, and inter-agent orchestration patterns.
- **Architecture-Aware** -- Deep knowledge of OpenClaw's binding system, session management, channel routing, sandboxing, and tool policies baked into every generated artifact.
- **Multi-Agent Orchestration by Design** -- Goes beyond single agents. Designs agent teams with spawn/send patterns, session routing, coordinated workflows, handoff failure handling, and loop prevention guardrails.
- **Brief-to-Deployment Pipeline** -- Complete lifecycle from "I have an idea" through structured brief, architecture design, artifact generation, and workspace assembly.
- **Portable Deployment Packages** -- Exports a `.zip` file + companion setup prompt. Users send both to any OpenClaw instance and the receiving agent unpacks, configures, and activates the entire agent system automatically. Zero manual setup.
- **Bidirectional Flow** -- Works both ways: OCF creates packages for export, and an OpenClaw agent can receive packages and self-install. Share agent systems like sharing apps.
- **Production-Ready by Default** -- Every generated workspace includes self-correction patterns, memory scaffolding, tool safety policies, resilience configuration, and observability setup. Not just structurally correct -- operationally hardened.

**Why users would choose this module:**

1. **Speed** -- Generate a complete multi-agent workspace in a fraction of the time it takes to manually create each file
2. **Coherence** -- All generated artifacts are internally consistent -- SOUL.md personality aligns with AGENTS.md directives, memory scaffolds match agent roles, tool policies match responsibilities
3. **Best Practices** -- Built-in knowledge of OpenClaw patterns ensures generated workspaces follow conventions, configure safety properly, and avoid common pitfalls
4. **Iteration** -- Edit and refine individual components while maintaining system-wide coherence
5. **Portability** -- Export complete agent systems as zip + prompt packages, share them, and deploy on any OpenClaw instance with a single message
6. **Production Hardening** -- Users don't need to know how to configure memory backends, tool policies, failover chains, or self-correction patterns. OCF generates best-practice configurations tuned to each agent's specific role.

---

## User Scenarios

### Target Users

1. **OpenClaw Developers** -- Building new agent systems for personal or production use
2. **Agent Designers** -- Focused on persona/behavior design, less comfortable with config plumbing
3. **System Integrators** -- Setting up multi-agent orchestration across channels (WhatsApp, Telegram, Discord, etc.)
4. **Teams** -- Organizations deploying OpenClaw with multiple specialized agents

### Primary Use Case

A developer wants to create a customer support system with three agents: a triage agent that routes inquiries, a technical support agent, and a billing agent. They describe the system concept to OCF, which guides them through persona design, skill selection, routing configuration, memory architecture, and safety policies -- then generates the complete workspace with all agents pre-configured to communicate, hand off between each other, self-correct from mistakes, and operate within role-appropriate safety boundaries.

### User Journey

1. **Concept** -- User describes their agent system idea (single agent or multi-agent)
2. **Brief** -- OCF guides creation of a structured brief covering agents, personas, skills, channels
3. **Architecture** -- OCF designs the agent interaction model, routing, orchestration, memory architecture, resilience strategy, and observability needs
4. **Generation** -- OCF produces all workspace artifacts including production hardening
5. **Assembly** -- OCF structures the complete workspace directory
6. **Configuration** -- OCF generates openclaw.json fragments for integration (agents, bindings, tool policies, memory backends, failover, logging, heartbeat)
7. **Review** -- User reviews, refines, and validates the generated system
8. **Package** -- OCF bundles everything into a `.zip` + setup prompt for portable deployment
9. **Deploy** -- User sends the zip + prompt to an OpenClaw agent, which self-installs the entire system

**Reverse Flow (Import):**

1. **Receive** -- An OpenClaw agent receives a zip package + setup prompt via any channel
2. **Unpack** -- The agent extracts the workspace archive
3. **Configure** -- The agent reads the setup prompt instructions and applies configuration (creates workspaces, registers agents, sets up bindings)
4. **Activate** -- The new agent system comes online, ready to operate

---

## Agent Architecture

### Agent Count Strategy

Three specialized agents form the OCF forge team, each handling a distinct phase of the creation pipeline. This separation ensures deep expertise at each stage while maintaining coherence through shared context.

### Agent Roster

| Agent | Name | Role | Expertise |
|-------|------|------|-----------|
| Forge Master | Vulcan | Lead Architect & Brief Creator | System-level thinking, requirements gathering, agent team design, orchestration planning, memory architecture design, resilience strategy, observability needs |
| Soul Smith | Anima | Persona & Identity Designer | SOUL.md creation, AGENTS.md directives, USER.md context, communication style, personality coherence, self-correction directives, boundary rules, feedback capture patterns |
| Gear Wright | Cog | Skills, Config & Assembly Engineer | SKILL.md generation, openclaw.json config, bindings, routing, tool policies, failover config, heartbeat setup, logging config, MEMORY.md scaffolds, workspace directory assembly, zip packaging, setup prompt generation |

### Agent Interaction Model

**Sequential Pipeline with Review Gates:**

1. **Vulcan** (Forge Master) handles the brief and architecture phase -- gathering requirements, designing the agent roster, planning orchestration patterns, designing memory architecture, resilience strategy, and observability needs
2. **Anima** (Soul Smith) takes the architecture and crafts each agent's identity -- personas, directives, user context, self-correction patterns, boundary rules, and feedback capture
3. **Cog** (Gear Wright) takes the identities and architecture, then generates skills, configuration, tool policies, memory scaffolds, resilience config, and assembles the final workspace

Each handoff includes a user review gate where the user can refine before proceeding.

### Agent Communication Style

- **Vulcan** -- Strategic and methodical. Speaks like a systems architect reviewing blueprints. "Let's map out how these agents will coordinate, where they'll store what they learn, and how they'll recover when things go wrong..."
- **Anima** -- Creative and empathetic. Focuses on personality and human interaction. "What kind of voice should this agent have? When it makes a mistake, how should it learn from that?"
- **Cog** -- Precise and technical. Speaks in terms of configuration and structure. "I'll wire up the bindings so WhatsApp routes to the triage agent first, lock down its tool access to read-only, and configure memory-lancedb with auto-recall..."

---

## Generated Artifact Specification

### Per-Agent Workspace Artifacts

For each agent in the target system, OCF generates:

| Artifact | Description |
|----------|-------------|
| `AGENTS.md` | Behavior directives, role-specific memory directives (e.g., "Log every misroute and the correction" for triage), self-correction directives (error journaling, pre-response checks), context overflow handling rules, session status awareness directives |
| `SOUL.md` | Persona definition, communication style, personality traits, boundary directives (privacy rules, data handling, escalation triggers like "If the user mentions legal action, escalate to human"), feedback capture patterns (recognizing "Actually...", "No, I meant...", "That's wrong") |
| `USER.md` | User context template appropriate to the agent's domain |
| `MEMORY.md` | Pre-seeded structured scaffold with role-relevant sections (e.g., a billing agent gets "Known Account Patterns," "Escalation History," "Common Resolution Paths" -- not empty files, structured scaffolds that teach the agent what to remember) |
| `skills/` | Skill directory with SKILL.md files, executable scaffolds, gating rules -- all passing OpenClaw's security scanner (no eval, no exec unless explicitly required and documented) |
| `REVIEW.md` | Periodic self-improvement prompt: "Review your memory/corrections.md. Are there patterns? Update your AGENTS.md directives to prevent recurring mistakes." |

### System-Level Configuration Artifacts

| Artifact | Description |
|----------|-------------|
| `openclaw.json` fragments | Agent entries, channel bindings, routing rules |
| Tool policies | Per-agent Allow/Deny lists based on role (billing agent: no shell access; triage agent: no file write) |
| Memory plugin config | Memory backend selection (memory-core vs memory-lancedb) with auto-recall and auto-capture enabled where appropriate |
| Failover config | Model fallback provider chains appropriate to use case (customer-facing agents get failover; internal batch agents may not) |
| Heartbeat config | Cron-style heartbeat patterns for long-running agents (memory compaction, status checks) |
| Logging config | Structured logging setup (console for development, JSON for production) |
| Subagent policies | Explicit tool restrictions for spawned subagents beyond OpenClaw's defaults, tightened per role |
| OCF metadata | Version and template metadata in generated artifacts for upgrade-path diffing |

### Self-Correction Directive Patterns

Generated into each agent's AGENTS.md:

- **Error journaling** -- "When a user corrects you, write the correction to memory/corrections.md with the date, what you said, what was wrong, and what's correct."
- **Pre-response checks** -- "Before responding on [domain topic], check MEMORY.md corrections section for known mistakes."
- **Feedback capture** -- Instructions to recognize implicit and explicit corrections ("Actually...", "No, I meant...", "That's wrong") and log them.

### Orchestration Hardening

Generated into multi-agent system configurations:

- **Handoff failure patterns** -- "If [agent] is unavailable, inform the user and log the failure." Fallback directives per agent.
- **Session routing guardrails** -- "Never spawn more than N subagents for a single request." Loop prevention directives.
- **Subagent tool restrictions** -- Explicit policies that tighten OpenClaw's default subagent restrictions based on the specific agent's role.

---

## Workflow Ecosystem

### Core Workflows (Essential)

1. **create-agent-brief** -- Guided discovery of a new OpenClaw agent system (single or multi-agent). Produces a structured brief covering all aspects: agents, personas, skills, channels, orchestration, memory architecture, resilience needs, and safety requirements.

2. **create-agent-system** -- Takes a brief and generates the complete workspace:
   - AGENTS.md for each agent (with memory directives, self-correction patterns, context overflow handling)
   - SOUL.md for each agent (with boundary directives, feedback capture patterns)
   - USER.md templates
   - MEMORY.md scaffolds (pre-seeded with role-relevant sections)
   - Skills directory with SKILL.md files (security-scanner compliant)
   - REVIEW.md (periodic self-improvement prompt)
   - openclaw.json configuration fragments (agents, bindings, tool policies, memory backends, failover, heartbeat, logging)
   - Workspace directory structure

3. **create-single-agent** -- Streamlined workflow for creating a single agent workspace (brief + generation in one flow).

### Feature Workflows (Specialized)

4. **design-orchestration** -- Focused workflow for designing multi-agent communication patterns: spawn/send relationships, session routing, channel bindings, handoff protocols, failure handling, loop prevention, and subagent tool restrictions.

5. **create-skill** -- Generate a complete OpenClaw skill: SKILL.md with proper frontmatter, executable code scaffold, gating rules (OS, binary requirements, env vars). Ensures security scanner compliance.

6. **edit-agent-system** -- Modify an existing generated workspace while maintaining coherence across all artifacts. Change one agent's persona and propagate implications to memory scaffolds, tool policies, and directives.

7. **configure-production-hardening** -- A focused workflow that takes a generated workspace (or an existing workspace) and layers on production features: memory configuration, tool policies, failover chains, heartbeat patterns, logging setup, self-correction directives, and boundary rules. Can be run standalone on workspaces not created by OCF.

### Utility Workflows (Support)

8. **validate-workspace** -- Check a generated workspace for internal consistency:
   - Do SOUL.md personalities match AGENTS.md directives?
   - Are all referenced skills present?
   - Are bindings complete?
   - Does every agent have memory directives?
   - Are tool policies defined for each agent?
   - Are boundaries set in SOUL.md?
   - Is failover configured for customer-facing agents?
   - Are self-correction directives present?

9. **export-config** -- Extract and format openclaw.json fragments ready for merge into an existing OpenClaw installation.

10. **package-export** -- Bundle a completed workspace into a portable `.zip` archive + a companion setup prompt. The zip contains all workspace files (AGENTS.md, SOUL.md, USER.md, MEMORY.md, skills/, REVIEW.md, etc.) and the prompt contains step-by-step instructions for an OpenClaw agent to unpack and activate the system. Includes OCF metadata for upgrade-path tracking. Output: `{agent-system-name}.ocf.zip` + `{agent-system-name}.setup.md`.

11. **package-import** -- The reverse flow. An OpenClaw agent receives an `.ocf.zip` + setup prompt and executes the installation: extracts workspace files to the correct directories, merges openclaw.json configuration, registers agent entries, sets up bindings, and activates the new agent system. Designed to be triggered by simply sending the zip + prompt to a running OpenClaw agent via any channel.

---

## Tools & Integrations

### MCP Tools

- **File system tools** -- For reading existing OpenClaw workspaces and writing generated artifacts
- **Template engine** -- For rendering workspace files from internal templates

### External Services

- None required -- OCF operates entirely locally with the BMAD framework and file system

### Integrations with Other Modules

- **BMB (BMAD Module Builder)** -- OCF is itself built using BMB patterns and can reference BMB conventions
- **Core BMAD** -- Uses standard BMAD workflow execution, step-file architecture, and agent patterns

---

## Creative Features

### Personality & Theming

The forge metaphor runs deep. Agents refer to the creation process as "forging," workspaces as "constructs," the brief as "blueprints," and memory scaffolds as "engrams." The overall tone is one of skilled craftsmanship -- building something with care and precision that will learn and grow over time.

### Easter Eggs & Delighters

- When generating a workspace with 5+ agents, Vulcan comments: "Now that's a proper battalion. Let's make sure they march in formation."
- When creating a solo agent, Anima says: "A lone wolf. Let's give them a soul worth remembering."
- Completing a full workspace generation triggers: "The forge fires cool. Your creation stands ready."
- When packaging for export, Cog says: "Sealed and stamped. This construct is ready to travel."
- On successful import/self-install: "New souls detected. The forge's work lives on in another realm."
- When generating self-correction directives: "A blade that sharpens itself. Now that's proper craftsmanship."
- When configuring failover: "Every good forge has a backup anvil."

### Module Lore

The OpenClaw Forge exists at the intersection of architecture and artistry. Three master crafters -- Vulcan the architect, Anima the soul-giver, and Cog the assembler -- work in concert to transform raw ideas into living agent systems. Each workspace that leaves the forge carries the mark of careful design: agents that know their purpose, skills that serve their masters, memories that teach them to grow, guardrails that keep them safe, and orchestration that flows like a well-oiled machine.

---

## Design Principles

### What OCF Does NOT Do

- **Fine-tuning or model training** -- OpenClaw doesn't support it, and it's not the right layer
- **Automated A/B testing** -- Over-engineering for a forge tool
- **Real-time performance dashboards** -- That's an ops concern, not a generation concern

### Core Insight

OpenClaw already has the machinery for self-learning (memory + directives), self-correction (memory journaling + pre-response checks), guardrails (tool policies + security scanning), and resilience (failover + context management). The gap is that users don't know how to configure all of it properly. OCF closes that gap by generating best-practice configurations for all of it, tuned to each agent's specific role.

---

## Next Steps

1. **Review this brief** -- Ensure the vision is clear
2. **Run create-module workflow** -- Build the module structure
3. **Create agents** -- Use create-agent workflow for each agent (Vulcan, Anima, Cog)
4. **Create workflows** -- Build the 11 workflows defined above
5. **Test module** -- Install and verify with a sample agent system generation

---

_brief created on 2026-02-11 by Althio using the BMAD Module workflow_
