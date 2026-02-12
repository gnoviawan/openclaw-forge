# Gating Rules Schema Reference

This document defines the valid schemas for OpenClaw skill gating rules and installation blocks used in SKILL.md frontmatter.

## Requirements Block (`requires`)

The `requires` block lives inside `metadata.openclaw` in SKILL.md frontmatter. It defines prerequisites that must be satisfied before the skill can be used.

### Available Fields

| Field | Type | Description |
|-------|------|-------------|
| `bins` | `string[]` | Binary names that MUST ALL be present in PATH |
| `anyBins` | `string[]` | Binary names where AT LEAST ONE must be present |
| `env` | `string[]` | Environment variables that MUST be set |
| `config` | `string[]` | Configuration keys (in openclaw.json) that MUST be present |

### Usage Rules

- Use `bins` when the skill requires specific CLI tools (e.g., `["gh"]` for GitHub CLI)
- Use `anyBins` when multiple tools can satisfy the requirement (e.g., `["ffmpeg", "avconv"]`)
- Use `env` for API keys or credentials (e.g., `["OPENAI_API_KEY"]`)
- Use `config` for OpenClaw-specific configuration (e.g., `["obsidian.vault_path"]`)
- All fields are optional -- omit if the skill has no requirements
- Do NOT include `os` in requires -- OS constraints go in the `install` block's `os` field

### Examples

**CLI tool wrapper:**
```yaml
"requires": { "bins": ["gh"] }
```

**API-based skill:**
```yaml
"requires": { "env": ["OPENAI_API_KEY"] }
```

**Multiple alternatives:**
```yaml
"requires": { "anyBins": ["ffmpeg", "avconv"] }
```

**Combined requirements:**
```yaml
"requires": { "bins": ["curl"], "env": ["API_TOKEN"] }
```

---

## Installation Block (`install`)

The `install` block defines how to install dependencies. It is an array of installation steps.

### Installation Step Fields

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `id` | `string` | No | Unique identifier for this step |
| `kind` | `string` | Yes | Installation method: `brew`, `node`, `go`, `uv`, `download` |
| `label` | `string` | No | Human-readable label |
| `bins` | `string[]` | No | Binaries provided by this installation |
| `os` | `string[]` | No | OS constraints: `darwin`, `linux`, `win32` |
| `formula` | `string` | brew only | Homebrew formula name |
| `package` | `string` | node only | npm package name |
| `module` | `string` | go only | Go module path |
| `url` | `string` | download only | Direct URL to binary/archive |
| `archive` | `string` | download only | Archive filename if inside URL |
| `extract` | `boolean` | download only | Whether to extract archive |
| `stripComponents` | `number` | download only | tar --strip-components equivalent |
| `targetDir` | `string` | download only | Directory to install into |

### Kind-Specific Examples

**brew:**
```yaml
{ "id": "brew", "kind": "brew", "formula": "gh", "bins": ["gh"], "label": "Install GitHub CLI (brew)" }
```

**node (npm):**
```yaml
{ "id": "npm", "kind": "node", "package": "typescript", "bins": ["tsc"], "label": "Install TypeScript" }
```

**go:**
```yaml
{ "id": "go", "kind": "go", "module": "github.com/user/tool@latest", "bins": ["tool"], "label": "Install tool (go)" }
```

**download:**
```yaml
{ "id": "download", "kind": "download", "url": "https://example.com/tool.tar.gz", "extract": true, "bins": ["tool"], "label": "Download tool binary" }
```

**Multiple installers (cross-platform):**
```yaml
"install": [
  { "id": "brew", "kind": "brew", "formula": "gh", "bins": ["gh"], "label": "Install GitHub CLI (brew)", "os": ["darwin"] },
  { "id": "apt", "kind": "apt", "package": "gh", "bins": ["gh"], "label": "Install GitHub CLI (apt)", "os": ["linux"] }
]
```

---

## Complete Frontmatter Example

```yaml
---
name: my-skill
description: "Description of what this skill does. Use when..."
metadata:
  {
    "openclaw":
      {
        "emoji": "icon",
        "requires": { "bins": ["tool-name"] },
        "install":
          [
            {
              "id": "brew",
              "kind": "brew",
              "formula": "tool-name",
              "bins": ["tool-name"],
              "label": "Install tool (brew)",
            },
          ],
      },
  }
---
```
