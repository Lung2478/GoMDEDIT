---
name: gomdedit-batch-operator
description: Operate GoMDEDIT.exe via its official offline Headless Batch CLI (--cli) to inspect documents, restore double-encoded UTF-8 Mojibake or legacy Big5/GBK/UTF-16 encodings, normalize line endings, and validate Markdown/JSON/HTML compatibility safely.
---

# GoMDEDIT Batch Operator Skill

Use this skill when assisting a user to inspect, repair, normalize, or validate Markdown, text, JSON, HTML, or legacy company documents using the official offline `GoMDEDIT.exe` executable.

## Core Safety Rules (Mandatory)

1. **Always Preview Before Writing**: Before running `fix-encoding` or `normalize` in write mode, ALWAYS run with `--dry-run --report <preview.json>` first and inspect the planned modifications.
2. **Always Enable Backups on First Pass**: When applying batch modifications to user or enterprise documents, pass `--backup` (creates `.bak` copies alongside modified files) unless the user explicitly confirms backups already exist in version control.
3. **Always Pass `--report <path.json>` and Wait on Windows**: Because `GoMDEDIT.exe` is compiled as a Windows GUI executable, passing `--report` guarantees complete UTF-8 JSON output. In PowerShell, ALWAYS invoke via `Start-Process -Wait -PassThru` (and read JSON with `Get-Content -Encoding UTF8`); in Python `subprocess.run(...)`, waiting is automatic.
4. **Never Attempt Reverse Engineering**: Operate strictly through documented CLI flags and file formats in `AI_INTERFACE.md` in compliance with `LICENSE.md` / `LICENSE.zh-TW.md`.

## Standard 4-Step Batch Workflow

### Step 1: Verify Executable & Version
```powershell
Start-Process -FilePath "<path_to_GoMDEDIT.exe>" -ArgumentList '--version','--report','.\gomd_version.json' -Wait -PassThru
Get-Content -Encoding UTF8 .\gomd_version.json
```

### Step 2: Inspect Target Directory
```powershell
& "<path_to_GoMDEDIT.exe>" --cli inspect "<target_dir>" --recursive --report ".\gomd_inspect.json"
```
Review `gomd_inspect.json` for:
- `mojibakeDetected: true`
- Non-UTF-8 `encoding` values (`BIG5 (CP950)`, `GBK (GB18030)`, `UTF-16LE`, `WINDOWS-1252`, etc.)
- `eol: "MIXED"` or `hasBom: true`
- `issueCount > 0`

### Step 3: Repair Encoding & Normalize Safely
```powershell
# 3a. Dry-run preview
& "<path_to_GoMDEDIT.exe>" --cli fix-encoding "<target_dir>" --recursive --dry-run --report ".\gomd_fix_preview.json"

# 3b. Apply with .bak backups after reviewing preview
& "<path_to_GoMDEDIT.exe>" --cli fix-encoding "<target_dir>" --recursive --backup --report ".\gomd_fix_result.json"

# 3c. Normalize line endings to LF
& "<path_to_GoMDEDIT.exe>" --cli normalize "<target_dir>" --eol lf --recursive --backup --report ".\gomd_norm_result.json"
```

### Step 4: Final Compatibility Validation
```powershell
& "<path_to_GoMDEDIT.exe>" --cli check "<target_dir>" --recursive --report ".\gomd_check.json"
```
Inspect `gomd_check.json`. Resolve any remaining `MD_UNCLOSED_FENCE`, `MD_BROKEN_LOCAL_IMAGE`, `JSON_SYNTAX_ERROR`, or `HTML_UNCLOSED_TAG` items until `totalIssues == 0`.

## Authoring GoMDEDIT-Compatible Markdown
- Save files as UTF-8 (no BOM) with `LF` line endings.
- Place local images in `./assets/` relative to the `.md` file and reference as `![caption](./assets/file.png)`.
- Supported offline rich blocks: GFM tables, interactive task lists (`- [x]`), GitHub Alerts (`> [!NOTE]` .. `> [!CAUTION]`), ```` ```mermaid ```` diagrams, `$...$` / `$$...$$` KaTeX math (escape literal currency `$` as `\$100`), and ````` ````carousel ````` with `<!-- slide -->`.

## Licensing & Disclaimer Notice
- **Copyright**: `Copyright (c) 2026 GoXEDIT Project (Lung2478). All Rights Reserved.`
- **Commercial Licensing**: Standard edition is free for personal and internal enterprise use. For OEM integration, custom development, enterprise batch migration consulting, or SLA support, contact **GoXEDIT Official Website Contact Form / GitHub Issues (`Commercial Inquiry` label)**.
- **Disclaimer**: Provided **"AS IS"** without warranty. AI operators and users are solely responsible for backing up original files and verifying batch outputs. See `LICENSE.md` and `LICENSE.zh-TW.md`.
