---
description: 'Build Apache Log4j 2.25.4 from source on Windows. Use when: setting up Log4j build environment, cloning and compiling Log4j, installing JDK and Maven for Log4j development.'
---

# Build Log4j 2.25.4 from Source

Set up the complete build environment and compile Apache Log4j 2.25.4 on Windows.

## Procedure

### 1. Install JDK 17

Log4j 2.25.4 enforces JDK version [17,18). JDK 21 will NOT work.

```powershell
winget install EclipseAdoptium.Temurin.17.JDK --accept-package-agreements --accept-source-agreements
```

Refresh PATH after install:

```powershell
$env:JAVA_HOME = "C:\Program Files\Eclipse Adoptium\jdk-17.0.18.8-hotspot"
$env:Path = "$env:JAVA_HOME\bin;" + [System.Environment]::GetEnvironmentVariable("Path", "Machine") + ";" + [System.Environment]::GetEnvironmentVariable("Path", "User")
```

Verify: `java -version` should show 17.x.

### 2. Install VS Code Extensions

- Extension Pack for Java (`vscjava.vscode-java-pack`) — no Red Hat account needed
- XML (`redhat.vscode-xml`)
- GitLens (`eamodio.gitlens`)

### 3. Clone the Repository

```powershell
git clone --branch rel/2.25.4 --depth 1 https://github.com/apache/logging-log4j2.git "c:\repos\Log4j"
cd "c:\repos\Log4j"
```

Shallow clone may miss root files. Restore them:

```powershell
git checkout HEAD -- pom.xml mvnw mvnw.cmd
```

### 4. Install Maven Manually

The Maven Wrapper (`mvnw.cmd`) fails on Windows with `Rename-Item: Access denied`. Install Maven 3.9.8 manually:

```powershell
$mavenDir = "$env:USERPROFILE\.m2\wrapper\dists\apache-maven-3.9.8"
New-Item -ItemType Directory -Path $mavenDir -Force | Out-Null
$zipFile = "$env:TEMP\maven-3.9.8.zip"
Invoke-WebRequest -Uri "https://repo.maven.apache.org/maven2/org/apache/maven/apache-maven/3.9.8/apache-maven-3.9.8-bin.zip" -OutFile $zipFile
Expand-Archive -Path $zipFile -DestinationPath "$env:TEMP\maven-extract" -Force
Copy-Item "$env:TEMP\maven-extract\apache-maven-3.9.8\*" $mavenDir -Recurse -Force
$env:Path = "$mavenDir\bin;" + $env:Path
```

Verify: `mvn -version` should show Maven 3.9.8 and JDK 17.

### 5. Build

SpotBugs reports 97 findings that fail the build. Skip it. Quote `-D` flags in PowerShell.

```powershell
cd "c:\repos\Log4j"
mvn verify "-DskipTests" "-Dspotbugs.skip=true"
```

Expect BUILD SUCCESS after ~7-8 minutes (first run downloads dependencies).

## Output

39 JARs in each module's `target/` directory. Key artifacts:

- `log4j-api\target\log4j-api-2.25.4.jar` (343 KB)
- `log4j-core\target\log4j-core-2.25.4.jar` (1,976 KB)
- `log4j-1.2-api\target\log4j-1.2-api-2.25.4.jar` (351 KB)

## Known Issues

| Issue | Solution |
|---|---|
| JDK 21 rejected by enforcer | Use JDK 17 only |
| `mvnw.cmd` Access Denied on Windows | Install Maven manually (Step 4) |
| SpotBugs fails with 97 findings | Skip with `-Dspotbugs.skip=true` |
| `-D` flags parsed wrong in PowerShell | Quote them: `"-DskipTests"` |
| Root pom.xml missing after shallow clone | `git checkout HEAD -- pom.xml mvnw mvnw.cmd` |
| `java`/`mvn` not recognized after install | Refresh PATH (see Step 1/4) |
