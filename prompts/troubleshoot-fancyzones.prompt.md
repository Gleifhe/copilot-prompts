---
description: 'Troubleshoot intermittent PowerToys FancyZones failures with MSScout or Copilot and collect privacy-aware diagnostic evidence before recovery.'
agent: 'agent'
---

# Troubleshoot FancyZones and Collect Diagnostic Evidence

## Mission

Troubleshoot an intermittent PowerToys FancyZones failure on this Windows PC using MSScout or the current agent's available tools.

Symptom: FancyZones sometimes disappears or stops functioning. Zones no longer appear and windows no longer snap into them.

Distinguish a process exit or crash, hang, input or activation problem, elevation mismatch, or monitor, virtual-desktop, or layout problem. Collect enough evidence for a useful PowerToys GitHub bug report.

## Safety and Preconditions

- Start read-only, except for creating the requested local evidence files. Do not restart PowerToys, toggle FancyZones, terminate processes, reset settings, reinstall, or change elevation until initial evidence is saved and the user approves recovery.
- Do not download or install diagnostic tools without permission.
- Do not collect credentials, clipboard contents, document contents, or unrelated application data.
- Do not upload anything. Keep evidence local and flag potentially sensitive information.
- If a capability or log is unavailable, say so. Do not fabricate results or bypass access restrictions.
- Ask whether the failure is happening now. If not, collect a baseline and explain what to capture during the next occurrence.
- Use available tools rather than assuming MSScout-specific commands exist.

## Workflow

### 1. Capture the Current State

- Record local time, UTC time, time zone, Windows version and build, PowerToys version, installation location, and available uptime information.
- Inspect `PowerToys.exe`, `PowerToys.FancyZones.exe`, and `PowerToys.FancyZonesEditor.exe`.
- Record PIDs, parent PIDs, start times, executable paths, CPU and memory usage, and elevation level where accessible.
- Check whether FancyZones is enabled in its persisted settings.
- Explain that the layout editor need not remain running, and that a process being present does not establish responsiveness.
- Record connected monitors, resolutions, scaling, primary monitor, and current virtual desktop where accessible.
- Ask for the approximate failure time and whether it followed sleep or resume, unlock, docking, monitor changes, virtual-desktop switching, or an update.

### 2. Preserve Relevant Evidence

Resolve the user's actual Desktop location, including redirection where applicable. Create a new timestamped evidence folder without overwriting existing files.

- Locate PowerToys data under `%LOCALAPPDATA%\Microsoft\PowerToys`, verifying actual paths rather than assuming the installed version's directory structure.
- Copy relevant FancyZones engine and editor logs and PowerToys runner logs, including the session before the failure where available. Preserve originals.
- Copy FancyZones settings and layout configuration needed for diagnosis. Treat application-history files and paths as potentially sensitive; omit them unless needed and explain any inclusion.
- If possible, generate the official PowerToys diagnostic ZIP through its supported Report Bug action. If this requires interaction, guide the user. Inventory its contents and flag privacy concerns. Keep the original archive separate from the curated evidence ZIP to avoid silently including unrelated data.
- Export relevant Windows Application events around the failure time, preferably plus or minus 30 minutes. If the time is unknown, use the last 24 hours.
- Focus on Application Error, Application Hang, Windows Error Reporting, and .NET Runtime entries mentioning PowerToys or FancyZones. Include timestamps, event IDs, faulting application and module, exception codes, and report IDs.
- Inspect available Windows Error Reporting metadata for matching failures. Do not copy memory dumps without asking.
- Avoid exporting entire unrelated event logs.

### 3. Run Non-destructive Functional Checks

With the user's cooperation:

- Test Shift-dragging a normal, non-elevated window.
- Test launching the FancyZones layout editor.
- Verify the selected layout for each affected monitor.
- Inspect activation settings, excluded applications, and relevant policy settings without changing them.
- Determine whether all applications fail or only specific or elevated applications.
- Record exact results. Separate observations from hypotheses.

### 4. Investigate a Possible Hang

If the engine is running but appears hung:

- Preserve its PID and logs first.
- Ask before capturing a process dump. Explain that a dump can contain private in-memory information and should not be attached directly to a public GitHub issue.
- Use only available, supported diagnostic facilities. Do not install tools or attach intrusive tracing automatically.

### 5. Recover Only After Approval

- Try toggling FancyZones off and on first.
- If necessary, exit and relaunch PowerToys normally.
- Record before and after process IDs and which step restored functionality.
- Do not delete layouts or reset configuration.
- Do not claim a root cause solely because restarting fixes the problem.

## Deliverables

Save a diagnostic summary and evidence inventory in the evidence folder. Provide:

1. A concise observed-facts summary.
2. The most likely failure category, confidence, and supporting evidence.
3. Alternative explanations and missing evidence.
4. Relevant error excerpts with timestamps.
5. Exact commands and actions performed, including failures or access restrictions.
6. An inventory identifying each file's source, collection time, and privacy concerns.
7. A ZIP of the curated collected files, excluding dumps unless approved.
8. A privacy warning identifying files that need review before public sharing.
9. The smallest useful next reproduction or diagnostic step.
10. Absolute paths to the summary, evidence folder, and ZIP.

Verify that the ZIP opens and contains the intended files. Report unavailable evidence explicitly rather than declaring collection complete.
