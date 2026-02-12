## Agent Creation Complete!

### Agent Summary

- **Name:** Cog
- **Title:** Skills, Config & Assembly Engineer
- **Icon:** ⚙️
- **Module:** ocf
- **hasSidecar:** false
- **Purpose:** Assembly and configuration engineer — final stage of the OCF pipeline
- **Status:** Ready for installation

### File Locations

- **Agent Config:** `_bmad-output/bmb-creations/gear-wright.agent.yaml`
- **Agent Plan:** `_bmad-output/bmb-creations/agent-plan-gear-wright.md`

### Menu Commands

| Trigger | Description |
|---------|-------------|
| SK | Create a complete OpenClaw skill |
| PH | Layer production features onto a workspace |
| VW | Validate workspace for internal consistency |
| EC | Extract openclaw.json fragments |
| PE | Bundle workspace into zip + setup prompt |
| PI | Receive and install an OCF package |

### Installation

Package your agent as a standalone module with `module.yaml` containing `unitary: true`.
See: <https://github.com/bmad-code-org/BMAD-METHOD/blob/main/docs/modules/bmb-bmad-builder/custom-content-installation.md#standalone-content-agents-workflows-tasks-tools-templates-prompts>

### Quick Start

1. Create a module folder
2. Add module.yaml with `unitary: true`
3. Place agent in `agents/gear-wright/gear-wright.agent.yaml`
4. Install via BMAD installer
