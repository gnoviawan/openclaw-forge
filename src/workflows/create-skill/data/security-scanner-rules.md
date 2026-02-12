# Security Scanner Rules Reference

This document defines the security scanner patterns that OpenClaw enforces on all skill code. Any skill with executable code (scripts/) must comply with these rules.

## Scanner Scope

The scanner checks files with extensions: `.js`, `.ts`, `.mjs`, `.cjs`, `.mts`, `.cts`, `.jsx`, `.tsx`

Python scripts (`.py`) and shell scripts (`.sh`, `.bash`) are NOT scanned by the automated scanner but should still follow security best practices.

---

## Critical Severity Rules (Will Block Skill)

| Rule ID | What It Detects | Pattern |
|---------|----------------|---------|
| `dangerous-exec` | Shell command execution via child_process | `exec(`, `execSync(`, `spawn(`, `spawnSync(`, `execFile(`, `execFileSync(` combined with `child_process` import |
| `dynamic-code-execution` | Dynamic code execution | `eval(` or `new Function(` |
| `crypto-mining` | Crypto-mining protocols or libraries | `stratum+tcp`, `stratum+ssl`, `coinhive`, `cryptonight`, `xmrig` |
| `env-harvesting` | Environment variable access combined with network requests | `process.env` combined with `fetch`, `post`, or `http.request` |

## Warning Severity Rules (Will Flag for Review)

| Rule ID | What It Detects | Pattern |
|---------|----------------|---------|
| `suspicious-network` | WebSocket connections to non-standard ports | `new WebSocket('ws://...:PORT')` where PORT is not 80, 443, 8080, 8443, or 3000 |
| `potential-exfiltration` | File reading combined with network requests | `readFileSync` or `readFile` combined with `fetch`, `post`, or `http.request` |
| `obfuscated-code` | Long hex-encoded strings | 6+ consecutive `\xNN` sequences |
| `obfuscated-code` | Large Base64 payloads being decoded | `atob('...')` or `Buffer.from('...')` with 200+ character Base64 strings |

---

## Compliance Guidelines for Skill Authors

### DO:
- Use `bash` commands via the SKILL.md instructions (the AI agent runs commands, not the skill code)
- Keep scripts focused on data transformation, not system interaction
- Use well-known npm packages for complex operations
- Document any legitimate use of flagged patterns in SKILL.md

### DO NOT:
- Use `eval()` or `new Function()` in any skill code
- Use `child_process` functions (exec, spawn) in TypeScript/JavaScript skill code
- Access `process.env` and make network requests in the same file
- Include long hex-encoded or Base64-encoded strings in code
- Connect to WebSocket servers on non-standard ports without documentation

### If You Must Use Flagged Patterns:
1. Document the use case explicitly in SKILL.md body
2. Explain why the flagged pattern is necessary
3. The skill will still trigger scanner warnings -- this is expected
4. Users will see the warning and can make an informed decision

### Preferred Alternatives:
- Instead of `exec()` in JS: Document the shell command in SKILL.md and let the AI agent run it
- Instead of `eval()`: Use JSON.parse() for data, or pre-computed values
- Instead of `process.env` + network: Split into separate concerns (config file for env, separate module for network)
