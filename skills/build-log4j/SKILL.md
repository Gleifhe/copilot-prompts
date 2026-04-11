---
name: build-log4j
description: 'Build Apache Log4j 2.25.4 from source on Windows. Use when: setting up Log4j build environment, cloning and compiling Log4j, installing JDK 17 and Maven, troubleshooting Log4j build failures, SpotBugs errors, Maven wrapper issues.'
argument-hint: 'Optionally specify a Log4j version or module to build'
---

# Build Apache Log4j from Source

Fully automated setup and build of Apache Log4j 2.25.4 on Windows.

## When to Use

- Setting up a Log4j development environment from scratch
- Cloning and building Log4j for the first time
- Troubleshooting Log4j build failures
- Onboarding a new developer to the Log4j codebase

## Procedure

### 1. Check Prerequisites

Verify Git is installed. If not, install it:

```powershell
git --version
```

### 2. Install JDK 17

Log4j 2.25.4 enforces JDK `[17,18)`. JDK 21 will be rejected by the Maven enforcer plugin.

```powershell
winget install EclipseAdoptium.Temurin.17.JDK --accept-package-agreements --accept-source-agreements
```

Set environment variables (required in every new terminal session):

```powershell
$env:JAVA_HOME = "C:\Program Files\Eclipse Adoptium\jdk-17.0.18.8-hotspot"
$env:Path = "$env:JAVA_HOME\bin;" + [System.Environment]::GetEnvironmentVariable("Path", "Machine") + ";" + [System.Environment]::GetEnvironmentVariable("Path", "User")
```

Verify: `java -version` must show 17.x.

### 3. Install VS Code Extensions

Install these three extensions:
- `vscjava.vscode-java-pack` (Extension Pack for Java — no Red Hat account needed)
- `redhat.vscode-xml` (XML support for pom.xml)
- `eamodio.gitlens` (Git history)

### 4. Clone the Repository

```powershell
git clone --branch rel/2.25.4 --depth 1 https://github.com/apache/logging-log4j2.git "c:\repos\Log4j"
cd "c:\repos\Log4j"
```

**Fix:** Shallow clone misses root files. Restore them:

```powershell
git checkout HEAD -- pom.xml mvnw mvnw.cmd
```

### 5. Install Maven Manually

**Known issue:** The Maven Wrapper (`mvnw.cmd`) fails on Windows with `Rename-Item: Access denied`.

Download and install Maven 3.9.8 manually:

```powershell
$mavenDir = "$env:USERPROFILE\.m2\wrapper\dists\apache-maven-3.9.8"
New-Item -ItemType Directory -Path $mavenDir -Force | Out-Null
$zipFile = "$env:TEMP\maven-3.9.8.zip"
Invoke-WebRequest -Uri "https://repo.maven.apache.org/maven2/org/apache/maven/apache-maven/3.9.8/apache-maven-3.9.8-bin.zip" -OutFile $zipFile
Expand-Archive -Path $zipFile -DestinationPath "$env:TEMP\maven-extract" -Force
Copy-Item "$env:TEMP\maven-extract\apache-maven-3.9.8\*" $mavenDir -Recurse -Force
$env:Path = "$mavenDir\bin;" + $env:Path
```

Verify: `mvn -version` must show Maven 3.9.8 and JDK 17.

### 6. Build

**Known issue:** SpotBugs reports 97 findings that fail the build. Skip it.
**Known issue:** PowerShell parses `-D` flags incorrectly. Quote them.

```powershell
cd "c:\repos\Log4j"
mvn verify "-DskipTests" "-Dspotbugs.skip=true"
```

Build takes ~7-8 minutes on first run (downloads dependencies). All 41 modules should report BUILD SUCCESS.

### 7. Verify

Check output JARs:

```powershell
Get-ChildItem "c:\repos\Log4j\*\target\*.jar" | Where-Object { $_.Name -notmatch "sources|javadoc|original" } | Select-Object @{N='Module';E={$_.Directory.Parent.Name}}, Name | Sort-Object Module | Format-Table -AutoSize
```

## Known Issues Reference

See [known-issues.md](./references/known-issues.md) for the full troubleshooting guide.

## Expected Output

39 JARs across 41 modules. Key artifacts:
- `log4j-api\target\log4j-api-2.25.4.jar` (343 KB) — Public API
- `log4j-core\target\log4j-core-2.25.4.jar` (1,976 KB) — Core implementation
- `log4j-1.2-api\target\log4j-1.2-api-2.25.4.jar` (351 KB) — 1.x compatibility
