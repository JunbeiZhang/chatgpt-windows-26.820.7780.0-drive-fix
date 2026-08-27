# ChatGPT/Codex Windows 26.820.7780.0 — Codex CLI Not Found on Non-System Drive

## Overview

This repository documents a workaround for the following ChatGPT/Codex Windows startup error:

```text
ChatGPT failed to start.

Unable to locate the Codex CLI binary.
Set CODEX_CLI_PATH or ensure the Electron resources include bin/codex.
```

In my case, the issue appeared with:

```text
OpenAI.Codex 26.820.7780.0
```

The application had been working normally the previous day. On August 27, 2026, after starting Windows, ChatGPT suddenly failed to launch.

The key detail was that the ChatGPT/Codex Windows app had been installed or moved to a **non-system drive (D:)**.

Moving the app back to the **C: drive** immediately fixed the problem.

---

## Environment

- OS: Windows
- Application: ChatGPT / OpenAI Codex Windows app
- Version: `26.820.7780.0`
- System drive: `C:`
- Problematic app location: `D:` / non-system drive
- Working app location: `C:`
- Timezone: UTC+8

---

## Timeline

### Last known working

```text
2026-08-26
```

ChatGPT/Codex was working normally.

### Failure observed

```text
2026-08-27 ~11:23 UTC+8
```

After starting Windows, ChatGPT failed to launch with:

```text
Unable to locate the Codex CLI binary
```

The exact time when version `26.820.7780.0` was automatically installed or updated is **unknown**.

### Troubleshooting attempted

On August 27, 2026:

- Windows **Repair** was attempted — did not fix the issue.
- Windows **Reset** was attempted — did not fix the issue.
- No manual `CODEX_CLI_PATH` configuration was required.
- No WindowsApps permission modification was required.

### Fix

The ChatGPT app was moved from the **D: drive back to the C: drive** using Windows Settings.

Windows then created the application directory on C: at approximately:

```text
CreationTime:  2026-08-27 11:32:58 UTC+8
LastWriteTime: 2026-08-27 11:33:17 UTC+8
```

These timestamps correspond to the application directory on the C: drive after moving the app and should **not** be interpreted as the exact original automatic update time.

After moving the app back to C:, ChatGPT/Codex launched normally again.

---

## PowerShell Information

The installed version can be checked with:

```powershell
Get-AppxPackage OpenAI.Codex |
Select-Object Name, Version, InstallLocation
```

After moving the application back to C:, the result was:

```text
Name         Version       InstallLocation
----         -------       ---------------
OpenAI.Codex 26.820.7780.0 C:\Program Files\WindowsApps\OpenAI.Codex_26.820.7780.0_x64__2p2nqsd0c76g0
```

The directory timestamps were checked with:

```powershell
$pkg = Get-AppxPackage OpenAI.Codex

Get-Item $pkg.InstallLocation |
Select-Object FullName, CreationTime, LastWriteTime
```

Result:

```text
FullName:
C:\Program Files\WindowsApps\OpenAI.Codex_26.820.7780.0_x64__2p2nqsd0c76g0

CreationTime:
2026/8/27 11:32:58

LastWriteTime:
2026/8/27 11:33:17
```

Again, these timestamps were obtained **after moving the application back to C:**.

---

## Workaround

If you encounter:

```text
Unable to locate the Codex CLI binary
```

and ChatGPT/Codex is installed on a non-system drive, try moving it back to the C: drive.

### Steps

1. Open **Windows Settings**.
2. Go to:

   ```text
   Apps
   → Installed apps
   ```

3. Find **ChatGPT**.
4. Click the **three-dot menu**.
5. Select:

   ```text
   Move
   ```

6. Choose:

   ```text
   C:
   ```

7. Wait for Windows to finish moving the application.
8. Launch ChatGPT again.

In my case, this fixed the problem immediately.

---

## What Did Not Work

| Method | Result |
|---|---|
| Repair | ❌ Did not work |
| Reset | ❌ Did not work |
| Reinstall Codex CLI | Not required |
| Set `CODEX_CLI_PATH` manually | Not required |
| Modify WindowsApps permissions | Not required |
| Move ChatGPT from D: to C: | ✅ Fixed |

---

## Important Detail

This report is specifically about the following combination:

```text
ChatGPT / OpenAI Codex
Version 26.820.7780.0
        +
Windows app located on a non-system drive
        ↓
Unable to locate the Codex CLI binary
        ↓
Move app back to C:
        ↓
Application starts normally
```

The same error message may have other causes.

Therefore, this workaround should not be interpreted as a universal fix for every `Unable to locate the Codex CLI binary` error.

However, if the problem appeared after an update and the application is currently installed on `D:`, `E:`, or another non-system drive, checking the installation drive may be worth doing before:

- manually setting `CODEX_CLI_PATH`,
- changing WindowsApps permissions,
- reinstalling CLI components,
- or performing more invasive troubleshooting.

---

## Short Version

If ChatGPT/Codex `26.820.7780.0` suddenly shows:

```text
Unable to locate the Codex CLI binary
```

on Windows, and the app is installed on `D:` or another non-system drive:

```text
Windows Settings
→ Apps
→ Installed apps
→ ChatGPT
→ ...
→ Move
→ C:
```

Moving the app back to the system drive fixed the issue in my case.

---

## Status

```text
Affected version:        26.820.7780.0
Last known working:      2026-08-26
Failure observed:        2026-08-27 ~11:23 UTC+8
Move to C: completed:    2026-08-27 ~11:33 UTC+8
Current status:          Working
Workaround:              Move ChatGPT/Codex back to C:
```
