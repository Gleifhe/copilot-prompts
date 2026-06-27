# Copilot Prompts Library

Personal collection of GitHub Copilot prompts, skills, and instructions.

## Structure

```
prompts/          — Prompt files (.prompt.md) → appear as /slash-commands
skills/           — Skills with bundled assets (SKILL.md + scripts/references)
instructions/     — Instruction files (.instructions.md) → auto-loaded by pattern
```

## Index

### Prompts

| Name | Command | Description |
|---|---|---|
| [build-log4j](prompts/build-log4j.prompt.md) | `/build-log4j` | Build Apache Log4j 2.25.4 from source on Windows — installs JDK 17, Maven, VS Code extensions, and compiles all 41 modules |
| [fresh-vscode-setup](prompts/fresh-vscode-setup.prompt.md) | `/fresh-vscode-setup` | Set up a fresh Windows VS Code environment for GitHub Copilot with current prerequisites, recommended extensions, verification steps, and post-install configuration |
| [threat-model](prompts/threat-model.prompt.md) | `/threat-model` | Generate a comprehensive threat model with STRIDE analysis, trust boundaries, attack trees, risk register, and remediation roadmap — delivers HTML and Markdown briefing |
| [pentest](prompts/pentest.prompt.md) | `/pentest` | Comprehensive penetration test guide — OWASP WSTG, PTES, NIST 800-115, MITRE ATT&CK methodology with 50+ test cases, language-specific grep patterns, and executive reporting |
| [work/executive-assistant](prompts/work/executive-assistant.prompt.md) | `/executive-assistant` | Executive Assistant productivity briefing and prioritisation strategy for recent Microsoft 365 activity, meetings, follow-ups, and workload triage |

### Skills

| Name | Command | Description |
|---|---|---|
| [build-log4j](skills/build-log4j/SKILL.md) | `/build-log4j` | Fully automated setup and build of Apache Log4j 2.25.4 — installs JDK 17, Maven, VS Code extensions, clones repo, and compiles all 41 modules. Includes [known issues reference](skills/build-log4j/references/known-issues.md). |

### Instructions

*None yet.*

## Usage

### In any workspace (personal)

Copy prompt files to your VS Code user prompts folder:

```powershell
Get-ChildItem "prompts" -Recurse -Filter "*.prompt.md" | Copy-Item -Destination "$env:APPDATA\Code\User\prompts\" -Force
```

They'll be available as `/slash-commands` in all workspaces.

### In a specific project (team)

Copy into the project's `.github/prompts/` directory:

```powershell
Get-ChildItem "prompts" -Recurse -Filter "*.prompt.md" | Copy-Item -Destination ".github\prompts\" -Force
```

Prompt files can live in subfolders for organization, but the command name still comes from the filename.
