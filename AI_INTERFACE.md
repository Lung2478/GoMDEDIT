# GoMDEDIT Official AI & Automation Interface Specification

> **Language / 語言導覽**：[繁體中文操作規格](#繁體中文-ai-自動化操作介面規格) | [English AI Interface Specification](#english-ai-interface-specification)  
> **Documentation Notice**: This public interface specification may be freely read and integrated into AI agent workflows with attribution to `GoXEDIT Project (Lung2478)`. The `GoMDEDIT.exe` executable itself remains proprietary freeware governed by [`LICENSE.md`](./LICENSE.md) / [`LICENSE.zh-TW.md`](./LICENSE.zh-TW.md).

---

## 繁體中文 AI 自動化操作介面規格

### 1. 無頭批次命令列介面（Headless Batch CLI — 零 GUI 靜默執行）

AI 代理人與企業自動化腳本可直接呼叫 `GoMDEDIT.exe` 執行 100% 離線批次作業，完全不彈出桌面視窗，並輸出標準 UTF-8 JSON。

> **Windows 執行與輸出可靠性建議**：由於 `GoMDEDIT.exe` 採 Windows GUI 子系統封裝，於 PowerShell 互動環境直接執行時系統預設會非同步返回。請務必：
> 1. 一律加上 **`--report <輸出路徑.json>`** 取得完整 UTF-8 JSON 報告；
> 2. 在 **PowerShell** 腳本中搭配 `Start-Process -Wait -PassThru`（或管線 `| Out-Null`）確保等待執行完畢再讀取報告，讀取時加上 `-Encoding UTF8`；在 **Python `subprocess.run(...)`** 或 **Node.js `execFileSync(...)`** 呼叫則會自動同步等待。

#### 1.1 版本與指令探測
```powershell
Start-Process -FilePath .\GoMDEDIT.exe -ArgumentList '--version','--report','.\version.json' -Wait -PassThru
Get-Content -Encoding UTF8 .\version.json
```

#### 1.2 `inspect`：批次盤點編碼、亂碼、換行符、大綱與問題數
```powershell
.\GoMDEDIT.exe --cli inspect <檔案或資料夾路徑> [--recursive] [--report .\inspect.json]
```
* **回傳 JSON 結構摘要**：
  ```json
  {
    "ok": true,
    "command": "inspect",
    "version": "1.2.0",
    "filesScanned": 1,
    "files": [
      {
        "path": "C:\\path\\to\\doc.md",
        "name": "doc.md",
        "sizeBytes": 2048,
        "encoding": "UTF-8",
        "mojibakeDetected": false,
        "hasBom": false,
        "eol": "LF",
        "lines": 64,
        "chars": 1950,
        "issueCount": 0,
        "headings": [{ "level": 1, "line": 1, "text": "Title" }]
      }
    ]
  }
  ```

#### 1.3 `fix-encoding`：批次還原 UTF-8 雙重編碼亂碼（Mojibake）與舊編碼轉 UTF-8
支援自動辨識並還原 `CP1252 / Latin-1` 雙重編碼亂碼，以及將 `Big5 (CP950)`、`GBK (GB18030)`、`UTF-16`、`UTF-8-BOM` 批次轉為乾淨無 BOM 的 `UTF-8`。
```powershell
# 步驟 1：強烈建議先以 --dry-run 預覽將受影響的檔案
.\GoMDEDIT.exe --cli fix-encoding <路徑> --recursive --dry-run --report .\fix_preview.json

# 步驟 2：確認無誤後執行轉換（建議加上 --backup 自動保留 .bak 備份）
.\GoMDEDIT.exe --cli fix-encoding <路徑> --recursive --backup --report .\fix_result.json
```

#### 1.4 `normalize`：批次正規化換行符（LF / CRLF）與清理 BOM
```powershell
.\GoMDEDIT.exe --cli normalize <路徑> --eol lf --recursive --dry-run --report .\norm_preview.json
.\GoMDEDIT.exe --cli normalize <路徑> --eol lf --recursive --backup --report .\norm_result.json
```

#### 1.5 `check`：離線語法、相對圖片與編碼相容性健檢
驗證項目包含：Markdown 未閉合程式碼圍欄、失效之本地相對圖片路徑 (`./assets/...`)、JSON 語法錯誤（精準至行列）、HTML/XML/SVG 未成對標籤、以及非 UTF-8 或亂碼警示。
```powershell
.\GoMDEDIT.exe --cli check <路徑> --recursive --report .\check_report.json
```
* **Exit Code 規範**：`0` = 零問題通過；`1` = 檢出問題或執行錯誤；`2` = CLI 參數錯誤。

---

### 2. GUI 模式外部呼叫與單一視窗多頁籤 IPC
* **一次開啟單一或多個檔案／資料夾**：
  ```powershell
  .\GoMDEDIT.exe "C:\docs\report.md" "C:\docs\notes.md"
  ```
* **指定行號跳轉**：支援 `file:///C:/docs/report.md#L42` 格式。
* **單一實例自動合併分頁**：當畫面上已有執行中的 `GoMDEDIT.exe` 時，再次以檔案路徑呼叫會透過本機 `127.0.0.1` Loopback IPC 自動在原視窗新增分頁並喚醒視窗。

---

### 3. GoMDEDIT 完全相容 Markdown 文件撰寫規範（供 AI 生成文件使用）
當 AI 代理人負責將公司舊文件重製為 100% 相容 GoMDEDIT 渲染的 `.md` 檔時，請遵循以下規範：
1. **編碼與換行**：一律輸出乾淨無 BOM 之 `UTF-8`，換行統一 `LF`。
2. **相對圖片路徑**：圖片集中存於同目錄 `./assets/`，以 `![描述](./assets/image.png)` 引用，確保單檔離線預覽與匯出 HTML 100% 正常顯示。
3. **支援之進階離線區塊語法**：
   * GitHub Alerts：`> [!NOTE]`、`> [!TIP]`、`> [!IMPORTANT]`、`> [!WARNING]`、`> [!CAUTION]`
   * 離線 Mermaid 圖表：使用 ```` ```mermaid ```` 圍欄（支援 `flowchart`、`sequenceDiagram`、`stateDiagram-v2`、`classDiagram`、`erDiagram`、`gantt`、`pie`）。
   * 離線 KaTeX 數學公式：行內 `$...$`、獨立區塊 `$$...$$`；一般金額字面 `$` 請跳脫為 `\$100` 或放入反引號 `` `$100` ``。
   * 互動多頁輪播卡：使用四個反引號 ````` ````carousel ````` 搭配 `<!-- slide -->` 分隔投影片。
   * 本地檔案行號連結：`[檔名](file:///C:/path/to/file.md#L10)`。

---

### 4. 本機偏好設定結構 (`%USERPROFILE%\.gomdedit\config.json`)
`GoMDEDIT.exe` 僅將使用者偏好存於本機家目錄，包含：`theme` (`"light"` | `"dark"`)、`language` (`"zh"` | `"en"`)、`autoSave`、`editorMode` (`"live"` | `"source"` | `"split"`)、`focusMode`、`typewriterMode`、`recentFiles`、`watermark`（每次重啟軟體 `watermark.enabled` 皆強制重置為 `false`）。

---

### 5. AI 自動化操作免責聲明
> 使用 AI 模型或自動化腳本呼叫 `GoMDEDIT.exe --cli` 批次修改檔案前，**使用者須自行完成原始檔案備份並優先執行 `--dry-run` 與人工抽檢驗證**。本軟體依「現況（AS-IS）」免費提供，`GoXEDIT Project (Lung2478)` 不對任何由外部 AI 誤判、覆寫、資料遺失或衍生損害承擔賠償責任（完整條款見 [`LICENSE.zh-TW.md`](./LICENSE.zh-TW.md)）。

---

## English AI Interface Specification

### 1. Headless Batch CLI (Zero-GUI Offline Execution)
AI agents and enterprise scripts can invoke `GoMDEDIT.exe` directly without launching a desktop window. Always pass `--report <path.json>` on Windows for guaranteed UTF-8 JSON capture regardless of console subsystem attachment.

| Command | Purpose | Key Flags |
| :--- | :--- | :--- |
| `GoMDEDIT.exe --version` | Return version, license summary, and supported subcommands as JSON | `--report <file>` |
| `GoMDEDIT.exe --help` | Print CLI usage summary | None |
| `GoMDEDIT.exe --cli inspect <path>` | Inspect encoding, Mojibake, EOL, line/char counts, headings, and issue counts | `--recursive`, `--report <file>` |
| `GoMDEDIT.exe --cli fix-encoding <path>` | Restore CP1252/Latin-1 double-encoded UTF-8 Mojibake and convert Big5/GBK/UTF-16/BOM to clean UTF-8 | `--recursive`, `--dry-run`, `--backup`, `--report <file>` |
| `GoMDEDIT.exe --cli normalize <path>` | Normalize line endings (`lf` or `crlf`) and strip UTF-8 BOM | `--eol lf\|crlf`, `--recursive`, `--dry-run`, `--backup`, `--report <file>` |
| `GoMDEDIT.exe --cli check <path>` | Validate Markdown fences, broken local relative `./assets/` image links, JSON syntax, HTML/XML tags, and encoding health | `--recursive`, `--report <file>` |

**Standard Exit Codes**: `0` = success / zero issues; `1` = validation issues detected or runtime error; `2` = invalid CLI arguments.

### 2. Recommended Safe AI Batch Workflow
1. Run `--cli inspect <dir> --recursive --report inspect.json` to map all files, encodings, and Markdown headings.
2. Run `--cli fix-encoding <dir> --recursive --dry-run --report fix_preview.json` to preview encoding/Mojibake changes without touching disk.
3. Back up the target folder, then execute `--cli fix-encoding <dir> --recursive --backup --report fix_result.json` and `--cli normalize <dir> --eol lf --recursive --report norm_result.json`.
4. Run `--cli check <dir> --recursive --report check.json` and verify `totalIssues == 0` before handing files back to users.

### 3. Future Planned Interfaces (Roadmap Preview)
Future GoXEDIT releases and Enterprise Editions may add additional headless batch interfaces (e.g., offline batch HTML export, multi-format Office document migration pipelines, and MCP server integration). For enterprise batch migration consulting or custom interfaces, contact **GoXEDIT Official Website Contact Form / GitHub Issues (`Commercial Inquiry` label)**.

### 4. Disclaimers
Provided **"AS IS"** without warranty of any kind. Users and AI operators are solely responsible for backing up original files, previewing changes with `--dry-run`, and verifying output integrity prior to production deployment. See [`LICENSE.md`](./LICENSE.md) for full terms.
