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

### Skills

*None yet.*

### Instructions

*None yet.*

## Usage

### In any workspace (personal)

Copy prompt files to your VS Code user prompts folder:

```powershell
Copy-Item "prompts\*.prompt.md" "$env:APPDATA\Code\User\prompts\" -Force
```

They'll be available as `/slash-commands` in all workspaces.

### In a specific project (team)

Copy into the project's `.github/prompts/` directory:

```powershell
Copy-Item "prompts\build-log4j.prompt.md" ".github\prompts\" -Force
```
