# GoMDEDIT Quick Start / 快速上手指南

> **語言導覽 / Language Navigation**：[繁體中文快速指南](#繁體中文快速指南) | [English Quick Start Guide](#english-quick-start-guide)

---

## 繁體中文快速指南

### 1. 零安裝立即啟動（100% 離線運作）
1. **直接執行**：雙擊本資料夾內的 `GoMDEDIT.exe` 即可開啟，無需安裝、無需網路連線、不需額外環境設定。
2. **隨身攜帶**：只需複製 `GoMDEDIT.exe` 單一執行檔至任何 Windows 10 / 11 電腦即可使用（內建 Edge WebView2 支援）。
3. **體驗這份指南**：可直接將本 `Quick_Start.md` 拖進 `GoMDEDIT.exe` 視窗，或從左上角「檔案 -> 開啟檔案」開啟，立即體驗即時渲染效果。
4. **設為預設開啟程式（選用）**：對任意 `.md` 檔案按右鍵 ->「開啟檔案」->「選擇其他應用程式」-> 選取 `GoMDEDIT.exe` 並勾選「一律使用」。後續在已開啟視窗時再次雙擊其他 `.md` 檔案，會自動於同一視窗新增分頁開啟。

### 2. 三種核心編輯模式與寫作輔助
* **即時預覽模式 (`Ctrl + 1`)**：預設所見即所得排版，點擊任意段落、表格、Mermaid 流程圖或 KaTeX 公式即可原位展開語法編輯，按 `Esc` 或點擊外部立即重新渲染。
* **純原始碼模式 (`Ctrl + /`)**：顯示行號、縮排輔助線與 30+ 種程式語言/設定檔多彩語法高亮；輸入 HTML 標籤自動補全 `</tag>`，輸入無圍欄程式碼自動辨識語言並可一鍵套用圍欄標記。
* **雙欄同步對照 (`Ctrl + \`)**：左欄編輯原始碼、右欄即時預覽，雙向智慧錨點對齊捲動。
* **專注模式與打字機模式**：於底部狀態列左側一鍵切換，聚焦當前編輯段落並保持游標位於螢幕中央。
* **MS Office 智慧貼上 (`Ctrl + V`)**：
  * 從 Word / Excel / PowerPoint 複製文字貼上時，自動過濾 Office 附帶的圖片快照並正確貼上文字。
  * 在 Markdown 文件貼上 2 格以上的 Excel / Word 表格時，自動轉換為對齊的 Markdown 表格。
  * 貼上純螢幕截圖（如 `Win + Shift + S`）時，自動儲存至同目錄 `./assets/` 並插入圖片語法。
* **列印與浮水印 (`Ctrl + P`)**：支援「文字浮水印（含範本、日期與檔名副標）」與「圖片 / Logo 浮水印」、滿版交錯平鋪或單一置中、即時迷你 A4 預覽，並可列印或匯出 PDF（每次重啟軟體時浮水印開關預設重置為關閉，避免誤印）。

### 3. 常用快捷鍵速查表

| 快捷鍵 | 功能說明 |
| :--- | :--- |
| `Ctrl + 1` | 切換至即時預覽模式 (Live Preview) |
| `Ctrl + /` | 切換至純原始碼模式 (Source Mode) |
| `Ctrl + \` | 切換至雙欄同步對照模式 (Split View) |
| `Shift + Alt + F` | 一鍵自動排版與縮排格式化 |
| `Ctrl + N` / `Ctrl + O` | 新增空白分頁 / 開啟檔案 |
| `Ctrl + S` / `Ctrl + Shift + S` | 儲存檔案 / 另存新檔 |
| `Ctrl + W` | 關閉目前分頁 |
| `Ctrl + Tab` / `Ctrl + Shift + Tab` | 快速循環切換分頁（亦可滑鼠拖曳分頁排序） |
| `Ctrl + F` / `Ctrl + H` | 搜尋關鍵字 / 尋找與取代 |
| `Ctrl + P` | 開啟列印與浮水印設定視窗 / 匯出 PDF |
| `Ctrl + Shift + L` | 展開 / 收合左側檔案樹與大綱側邊欄 |
| `Esc` | 完成單一區塊編輯並即時重新渲染 |

### 4. AI 代理人與無頭批次命令列（Headless CLI）
除桌面圖形介面外，`GoMDEDIT.exe` 亦提供零視窗靜默執行之批次命令列介面，方便 AI 模型與企業腳本自動化處理大量檔案（完整規格見 `AI_INTERFACE.md`）：
```powershell
# 查看版本與支援指令
.\GoMDEDIT.exe --version --report .\version.json

# 預覽修復資料夾內所有檔案的亂碼與舊編碼（不寫入磁碟）
.\GoMDEDIT.exe --cli fix-encoding .\docs_folder --recursive --dry-run --report .\preview.json

# 離線檢查 Markdown 圍欄、相對圖片連結、JSON 與 HTML 語法
.\GoMDEDIT.exe --cli check .\docs_folder --recursive --report .\check.json
```

### 5. 隱私、授權與免責聲明
* **100% 離線隱私**：`GoMDEDIT.exe` 不連線至任何遠端伺服器、不回傳任何遙測或使用紀錄；偏好設定僅存於本機 `%USERPROFILE%\.gomdedit\config.json`。
* **授權與商業洽詢**（完整條文見 `LICENSE.zh-TW.md` / `LICENSE.md` 與 `THIRD_PARTY_NOTICES.txt`）：
  > 本免費授權涵蓋標準版之個人與企業內部使用。若貴公司需要 OEM 內嵌整合、專屬客製開發、企業級大量舊檔重製顧問、或專屬技術支援與 SLA，請聯繫 GoXEDIT 官方取得商業授權。
  * 版權歸屬：`Copyright (c) 2026 GoXEDIT Project (Lung2478). All Rights Reserved.`
  * 商業授權聯繫方式：GoXEDIT 官方網站聯絡表單 / GitHub Issues（商用洽詢標籤）
* **免責聲明**：本軟體及其 CLI / AI 接口皆依「現況（AS-IS）」免費提供，不附帶任何明示或默示保證；`GoXEDIT Project (Lung2478)` 不對資料遺失、檔案損毀或業務中斷承擔賠償責任。執行 AI 或批次命令列修改前請務必自行備份原始檔案並先以 `--dry-run` 預覽驗證。

---

## English Quick Start Guide

### 1. Zero-Install Instant Launch (100% Offline)
1. **Run Directly**: Double-click `GoMDEDIT.exe` in this folder to start immediately — no installation, no internet connection, and no external runtime setup required.
2. **Portable Single File**: Copy `GoMDEDIT.exe` alone to any Windows 10 / 11 PC (uses the built-in Edge WebView2 engine).
3. **Try It with This Guide**: Drag `Quick_Start.md` into `GoMDEDIT.exe` (or open it via `File -> Open File`) to experience live Markdown rendering immediately.
4. **Set as Default `.md` App (Optional)**: Right-click any `.md` file -> `Open with` -> `Choose another app` -> select `GoMDEDIT.exe` and check `Always`. Double-clicking additional `.md` files while a window is open automatically opens them as new tabs in the same window.

### 2. Core Editing Modes & Smart Assistants
* **Live Preview (`Ctrl + 1`)**: Clean rendered view by default; click any paragraph, table, Mermaid diagram, or KaTeX formula to edit Markdown inline, then press `Esc` or click outside to re-render.
* **Source Mode (`Ctrl + /`)**: Line numbers, indentation guides, and syntax highlighting for Markdown plus 30+ programming and config languages, with `<tag></tag>` auto-closing, 400ms offline syntax diagnostics with one-click quick fixes, and automatic code language detection.
* **Split View (`Ctrl + \`)**: Side-by-side source and live preview with bidirectional line-anchor synchronized scrolling.
* **Focus Mode & Typewriter Mode**: Toggle from the bottom-left status bar to dim surrounding paragraphs and keep the active typing line centered vertically.
* **Smart Clipboard Paste (`Ctrl + V`)**:
  * Copying text from MS Word, Excel, or PowerPoint pastes clean text instead of Office's bundled bitmap snapshot.
  * Pasting multi-cell tables from Excel or Word into a Markdown file automatically converts them into formatted GFM Markdown tables.
  * Pasting screenshots (e.g., `Win + Shift + S`) saves the image to `./assets/` next to the document and inserts a relative Markdown image link.
* **Print & Watermark (`Ctrl + P`)**: Configure text watermarks (with presets, date/filename subtitles, and color swatches) or local image/logo watermarks in tiled or centered layout with a live mini A4 preview before printing or exporting to PDF (watermark toggle resets to off on every app launch).

### 3. Essential Keyboard Shortcuts

| Shortcut | Action |
| :--- | :--- |
| `Ctrl + 1` | Switch to Live Preview Mode |
| `Ctrl + /` | Switch to Source Code Mode |
| `Ctrl + \` | Switch to Split View Mode |
| `Shift + Alt + F` | Auto-format and indent document or code |
| `Ctrl + N` / `Ctrl + O` | New tab / Open file |
| `Ctrl + S` / `Ctrl + Shift + S` | Save / Save As |
| `Ctrl + W` | Close current tab |
| `Ctrl + Tab` / `Ctrl + Shift + Tab` | Cycle through open tabs (also drag tabs to reorder) |
| `Ctrl + F` / `Ctrl + H` | Find / Find & Replace |
| `Ctrl + P` | Open Print & Watermark dialog / Export PDF |
| `Ctrl + Shift + L` | Toggle Files / Outline sidebar |
| `Esc` | Commit inline block edit and re-render in Live Preview |

### 4. AI Agent & Headless Batch CLI
Beyond the desktop GUI, `GoMDEDIT.exe` provides a zero-window offline CLI for AI models and enterprise batch scripts (see `AI_INTERFACE.md` for full schemas):
```powershell
.\GoMDEDIT.exe --version --report .\version.json
.\GoMDEDIT.exe --cli fix-encoding .\docs_folder --recursive --dry-run --report .\preview.json
.\GoMDEDIT.exe --cli check .\docs_folder --recursive --report .\check.json
```

### 5. Privacy, Licensing & Disclaimers
* **100% Offline Privacy**: `GoMDEDIT.exe` operates with zero external CDN requests, zero telemetry, and zero cloud uploads. Local preferences live strictly at `%USERPROFILE%\.gomdedit\config.json`.
* **Licensing & Commercial Inquiries** (see `LICENSE.md`, `LICENSE.zh-TW.md`, and `THIRD_PARTY_NOTICES.txt`):
  > This free license covers personal and internal enterprise use of the standard edition. If your organization requires OEM embedding / integration, custom feature development, enterprise-scale legacy file batch conversion consulting, or dedicated technical support and SLA, please contact **GoXEDIT Official** for a Commercial License.
  * Copyright: `Copyright (c) 2026 GoXEDIT Project (Lung2478). All Rights Reserved.`
  * Contact: GoXEDIT Official Website Contact Form / GitHub Issues (`Commercial Inquiry` label)
* **Disclaimers**: Provided **"AS IS"** without warranty of any kind. `GoXEDIT Project (Lung2478)` is not liable for data loss, file corruption, or consequential damages. Always back up original files and preview with `--dry-run` before running AI or batch CLI commands.
