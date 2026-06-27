# Fresh VS Code Setup for GitHub Copilot with Claude

Guide me through setting up a fresh Visual Studio Code installation with GitHub Copilot (Claude) and all recommended extensions and software. Check what's already installed and skip those steps.

## Step 1: Prerequisites — Software to Install on Windows

Check and install the following system-level software (verify each with version commands before installing):

### Required
- **Git** — `winget install Git.Git` (version control — essential for Copilot)
- **Node.js LTS** — `winget install OpenJS.NodeJS.LTS` (JavaScript/TypeScript runtime, npm, build tools)
- **Python 3.13+** — `winget install Python.Python.3.13` (check "Add to PATH" during install)
- **Java JDK 21+** — `winget install EclipseAdoptium.Temurin.21.JDK` (Java development — 21 is current LTS)
- **.NET SDK** — `winget install Microsoft.DotNet.SDK.10` (C#/.NET development)

### Recommended
- **Maven** — Not available via winget. Download from https://maven.apache.org/download.cgi (Binary zip), extract to `C:\Tools`, and add the `bin` folder to your user PATH
- **Docker Desktop** — `winget install Docker.DockerDesktop` (containers, databases, deployment)

After each install, restart the terminal and verify with `--version` commands.

## Step 2: Install GitHub Copilot

1. Open VS Code
2. Go to Extensions (Ctrl+Shift+X)
3. Search for **"GitHub Copilot"** and install it (publisher: GitHub)
4. Sign in with your GitHub account when prompted
5. Ensure you have an active GitHub Copilot subscription (Individual, Business, or Enterprise)
6. In Copilot Chat settings, set the model to **Claude** (click the model picker in the chat panel)

## Step 3: Install Recommended VS Code Extensions

Install these extensions for full language support and tooling that Copilot/Claude can leverage:

### Python
- `ms-python.python` — Python language support
- `ms-python.vscode-pylance` — Python IntelliSense
- `ms-python.debugpy` — Python debugging
- `ms-python.vscode-python-envs` — Python environment management

### Java
- `vscjava.vscode-java-pack` — Java Extension Pack (installs all of the below):
  - `redhat.java` — Java language support
  - `vscjava.vscode-java-debug` — Java debugging
  - `vscjava.vscode-java-test` — Java testing
  - `vscjava.vscode-maven` — Maven support
  - `vscjava.vscode-java-dependency` — Project management
  - `vscjava.vscode-gradle` — Gradle support

### C# / .NET
- `ms-dotnettools.csdevkit` — C# Dev Kit (IntelliSense, debugging, project management)

### Git
- `eamodio.gitlens` — GitLens/GitKraken (advanced Git features, blame, history — enables MCP tools for Claude)

### Web / Markup
- `redhat.vscode-xml` — XML language support
- `redhat.vscode-yaml` — YAML language support (CI/CD pipelines, config files)

### Azure (if using Azure cloud)
- `ms-azuretools.vscode-azureresourcegroups` — Azure Resource Groups
- `ms-azuretools.azure-dev` — Azure Developer CLI
- `ms-azuretools.vscode-docker` — Docker support

### Utilities
- `ms-vscode.powershell` — PowerShell language support (Windows terminal)
- `bierner.markdown-mermaid` — Mermaid diagram rendering in Markdown
- `github.vscode-github-actions` — GitHub Actions workflow support

## Step 4: Verify Everything Works

Run these commands in the VS Code terminal (Ctrl+`) to confirm:

```powershell
git --version
node --version
npm --version
python --version
python -m pip --version
java --version
dotnet --version
mvn --version
docker --version
```

All commands should return version numbers without errors.

## Step 5: Post-Install Settings

1. **Set default terminal** — PowerShell 7+ recommended (`ms-vscode.powershell`)
2. **Sign into GitHub** — Required for Copilot, GitHub Actions, and remote repos
3. **Sign into Azure** — If using Azure extensions
4. **Select Python interpreter** — Ctrl+Shift+P → "Python: Select Interpreter"
5. **Configure Git** — `git config --global user.name "Your Name"` and `git config --global user.email "your@email.com"`

## Notes
- Claude can run terminal commands, read/edit files, search code, and use MCP tools from GitLens
- Language extensions provide IntelliSense and error diagnostics that Claude uses for better code assistance
- Node.js is needed even if you don't write JavaScript — many build tools and linters depend on it
- Maven is not in winget; manual install to C:\Tools is the standard approach on Windows
