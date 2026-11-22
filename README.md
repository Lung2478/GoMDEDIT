# GoMDEDIT — 極輕量全能離線筆記與程式碼編輯器 (Ultra-Light Offline Markdown & Text Editor)

> **語言導覽 / Language**：[繁體中文介紹](#一核心特色與免費下載) | [English Overview](#english-overview) | [快速上手指南 (Quick Start)](./Quick_Start.md) | [AI 自動化操作介面 (AI Interface)](./AI_INTERFACE.md) | [授權條款 (LICENSE)](./LICENSE.md)

**GoMDEDIT** 是 **GoXEDIT** 離線生產力工具家族旗下的單一執行檔 Markdown、筆記與程式碼編輯器。**免安裝、100% 離線運作、零雲端遙測**，同時內建官方 **無頭批次命令列接口（Headless Batch CLI）**，讓個人、企業團隊與各類 AI 代理人皆能直接高效率處理文件。

---

## 一、 核心特色與免費下載

### 立即下載（Windows 10 / 11）
* 前往本倉庫 **[Releases 頁面](https://github.com/Lung2478/GoMDEDIT/releases/latest)** 下載最新版 **`GoMDEDIT.exe`**（免安裝單一執行檔，雙擊即用）。
* 發行包隨附 `Quick_Start.md`、`LICENSE.md`、`LICENSE.zh-TW.md`、`THIRD_PARTY_NOTICES.txt`、`AI_INTERFACE.md` 與 `SHA256SUMS.txt` 校驗檔。

### 核心亮點
1. **三態無縫編輯視角**：
   * **即時預覽 (`Ctrl + 1`)**：點擊任意段落原位展開語法編輯，按 `Esc` 立即渲染。
   * **純原始碼 (`Ctrl + /`)**：行號、縮排輔助線、30+ 種程式語言多彩高亮、HTML 對稱標籤補全與 400ms 離線語法診斷及一鍵修復。
   * **雙欄同步對照 (`Ctrl + \`)**：左欄原始碼、右欄即時預覽，區塊行號錨點雙向對齊捲動。
2. **100% 離線進階排版引擎**：完整內嵌 GFM 表格、互動式待辦清單、5 種 GitHub Alerts (`[!NOTE]`~`[!CAUTION]`)、````carousel` 互動輪播卡、離線 Mermaid 流程圖與離線 KaTeX 數學公式。
3. **辦公與列印效率增強**：
   * **MS Office 剪貼簿智慧分流 (`Ctrl + V`)**：從 Word / Excel / PowerPoint 複製文字貼上不再誤存為圖片快照；Excel / Word 表格自動轉為對齊 Markdown 表格；純截圖自動落地 `./assets/`。
   * **跨頁向量浮水印列印 (`Ctrl + P`)**：支援文字與本地 Logo 圖片浮水印、滿版交錯平鋪或單一置中、即時迷你 A4 預覽，且每次啟動預設關閉浮水印開關防止誤印。
   * **一鍵還原中文亂碼**：自動修復 CP1252 / Latin-1 雙重編碼 UTF-8 亂碼（Mojibake），並支援 `Big5` / `GBK` / `UTF-16` 手動切換重讀。
4. **AI-Ready 無頭批次操作介面 (`GoMDEDIT.exe --cli`)**：
   * 不彈出視窗即可由 AI 模型或自動化腳本批次執行 `inspect`（結構與編碼盤點）、`fix-encoding`（批量亂碼與編碼修復）、`normalize`（換行符正規化）與 `check`（語法與相對圖檔健檢），全程輸出標準 JSON。

---

## 二、 給 AI 模型與自動化工作流的官方入口

本專案官方提供結構化技術規格與 Agent Skill，協助 AI 模型直接操作 `GoMDEDIT.exe` 完成企業舊檔盤點、亂碼還原與完全相容格式重製：
* **完整介面與 JSON Schema 規格書**：[`AI_INTERFACE.md`](./AI_INTERFACE.md)
* **AI 代理人標準技能檔（Skill）**：[`SKILL.md`](./SKILL.md)
* **中英雙語快速上手手冊**：[`Quick_Start.md`](./Quick_Start.md)

```powershell
# 範例：檢查版本與支援之無頭批次子命令
.\GoMDEDIT.exe --version

# 範例：預覽批次修復資料夾內所有檔案的亂碼與舊編碼（不寫入磁碟）
.\GoMDEDIT.exe --cli fix-encoding .\legacy_docs --recursive --dry-run --report .\preview.json
```

---

## 三、 授權條款與商業授權洽詢

本軟體採 **專有免費軟體授權（Proprietary Freeware License）** 發佈，不公開原始碼：
* **英文正式授權條款**：[`LICENSE.md`](./LICENSE.md)
* **繁體中文授權條款**：[`LICENSE.zh-TW.md`](./LICENSE.zh-TW.md)
* **第三方開源元件致謝聲明**：[`THIRD_PARTY_NOTICES.txt`](./THIRD_PARTY_NOTICES.txt)

> **商業授權明文註記**：  
> 本免費授權涵蓋標準版之個人與企業內部使用。若貴公司需要 OEM 內嵌整合、專屬客製開發、企業級大量舊檔重製顧問、或專屬技術支援與 SLA，請聯繫 GoXEDIT 官方取得商業授權。

* **版權歸屬**：`Copyright (c) 2026 GoXEDIT Project (Lung2478). All Rights Reserved.`
* **商業授權聯繫方式**：GoXEDIT 官方網站聯絡表單 / GitHub Issues（商用洽詢標籤：`https://github.com/Lung2478/GoMDEDIT/issues`）

---

## 四、 免責聲明 (Disclaimers)

1. **按「現況」免費提供與無保證聲明（AS-IS / No Warranty）**：本軟體、隨附文件及所有 CLI / AI 接口皆依「現況（AS-IS）」免費提供，不附帶任何明示或默示保證（包括適售性、特定用途適用性或未侵權保證）。
2. **責任限制聲明（Limitation of Liability）**：在適用法律允許之最大範圍內，`GoXEDIT Project (Lung2478)` 不對任何因使用本軟體所引起之資料遺失、檔案損毀、編碼誤差、業務中斷或衍生損害承擔賠償責任。
3. **AI 代理人與批次自動化操作風險提醒**：使用 AI 模型、腳本或 `--cli` 批次修改檔案前，請務必自行備份原始檔案，並優先使用 `--dry-run` 預覽與人工抽檢驗證；授權人不對外部 AI 誤判或腳本覆寫結果承擔責任。
4. **第三方開源元件與非法律意見聲明**：內嵌之第三方開源元件係依其各自原開源授權獨立提供（見 `THIRD_PARTY_NOTICES.txt`）；本說明僅供資訊參考，不構成正式法律意見。

---

## English Overview

**GoMDEDIT** is a portable, single-file, **100% offline** Markdown, note, and code editor from the **GoXEDIT** productivity family. It runs directly on Windows 10/11 with zero installation, zero telemetry, and zero external CDN requests — while providing an official **Headless Batch CLI (`GoMDEDIT.exe --cli`)** and Agent Skill (`SKILL.md`) so AI models and enterprise scripts can automate file inspection, Mojibake encoding repair, normalization, and syntax checks out of the box.

* **Download Latest Portable Executable**: [GitHub Releases](https://github.com/Lung2478/GoMDEDIT/releases/latest)
* **Quick Start Guide (Bilingual)**: [`Quick_Start.md`](./Quick_Start.md)
* **Official AI Automation Interface & Agent Skill**: [`AI_INTERFACE.md`](./AI_INTERFACE.md) | [`SKILL.md`](./SKILL.md)
* **License (Free for Personal & Internal Enterprise Use)**: [`LICENSE.md`](./LICENSE.md) | [`LICENSE.zh-TW.md`](./LICENSE.zh-TW.md) | [`THIRD_PARTY_NOTICES.txt`](./THIRD_PARTY_NOTICES.txt)

> **Commercial Licensing Notice**:  
> This free license covers personal and internal enterprise use of the standard edition. If your organization requires OEM embedding / integration, custom feature development, enterprise-scale legacy file batch conversion consulting, or dedicated technical support and SLA, please contact **GoXEDIT Official** for a Commercial License via the **GoXEDIT Official Website Contact Form / GitHub Issues (`Commercial Inquiry` label)**.

> **Disclaimers**:  
> Provided **"AS IS"** without warranty of any kind. `GoXEDIT Project (Lung2478)` is not liable for data loss, file corruption, business interruption, or consequential damages. Always back up original files and preview with `--dry-run` before running AI or batch CLI modifications. See [`LICENSE.md`](./LICENSE.md) for complete terms.
