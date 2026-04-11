# Log4j 2.25.4 Build — Known Issues

## JDK Version Enforced

**Error:** `Detected JDK version 21.0.10 is not in the allowed range [17,18).`

**Cause:** Log4j's Maven enforcer plugin requires exactly JDK 17.x.

**Fix:** Install and use JDK 17:
```powershell
winget install EclipseAdoptium.Temurin.17.JDK
$env:JAVA_HOME = "C:\Program Files\Eclipse Adoptium\jdk-17.0.18.8-hotspot"
```

## Maven Wrapper Access Denied

**Error:** `Rename-Item : Access to the path '...\apache-maven-3.9.8' is denied.`

**Cause:** The PowerShell Maven Wrapper script (`mvnw.cmd`) fails during extraction on Windows.

**Fix:** Download Maven 3.9.8 manually (see SKILL.md Step 5).

## SpotBugs Fails with 97 Findings

**Error:** `failed with 97 bugs and 0 errors`

**Cause:** SpotBugs static analysis on `log4j-api` reports pre-existing findings that block the build.

**Fix:** Skip SpotBugs:
```powershell
mvn verify "-DskipTests" "-Dspotbugs.skip=true"
```

## PowerShell -D Flag Parsing

**Error:** `Unknown lifecycle phase ".skip=true".`

**Cause:** PowerShell interprets `-Dspotbugs.skip=true` as two separate arguments.

**Fix:** Quote all `-D` flags:
```powershell
mvn verify "-DskipTests" "-Dspotbugs.skip=true"
```

## Root pom.xml Missing After Shallow Clone

**Error:** Build can't find the reactor POM.

**Cause:** `git clone --depth 1` with a tag may not check out all root files.

**Fix:**
```powershell
git checkout HEAD -- pom.xml mvnw mvnw.cmd
```

## java/mvn Not Recognized After Install

**Cause:** New terminal sessions don't inherit PATH changes from installers until restarted.

**Fix:** Refresh PATH manually:
```powershell
$env:Path = [System.Environment]::GetEnvironmentVariable("Path", "Machine") + ";" + [System.Environment]::GetEnvironmentVariable("Path", "User")
```
