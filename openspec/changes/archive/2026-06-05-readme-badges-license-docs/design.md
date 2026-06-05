## Context

`openspec-custom-skills` 是一個公開 GitHub repo，目前：
- `package.json` 已聲明 `"license": "MIT"`，但 repo 根目錄沒有 `LICENSE` 文件，不符合開源慣例，`git hub/license` badge 也無法正確讀取
- README 頂部沒有版本號與授權徽章，訪客無法一眼看出專案版本與授權狀態
- `openspec-propose-design-mermaid-html` 和 `openspec-design-html` 的 README 說明只用一個 inline 表格描述 `design.html` 的按需 section，8 種 Mermaid 圖表類型沒有個別列出，也沒有連結到各自的 mermaid.ai 文件

## Goals / Non-Goals

**Goals:**
- README 頂部加入 GitHub release 版本徽章與 MIT 授權徽章
- repo 根目錄新增標準 MIT `LICENSE` 文件
- `package.json` `files` 陣列補上 `"LICENSE"`，確保 npm publish 時一併打包
- README 的 `openspec-propose-design-mermaid-html` section 加入完整 Mermaid 圖表類型 table（8 種，中英對照，連結至 mermaid.ai，標注 mermaid.js.org）
- `openspec-design-html` section 以一句話指回 `openspec-propose-design-mermaid-html`，不重複 table

**Non-Goals:**
- 不修改任何 SKILL.md 邏輯
- 不修改 `assets/page-shell.html`
- 不建立或修改 `openspec/specs/` 下已存在的 spec
- 不涉及 npm publish 或 git tag 的實際操作（使用者自行決定發布時機）

## Decisions

### 決策 1：徽章類型選擇 GitHub release badge 而非靜態 badge

選擇：使用 `https://img.shields.io/github/v/release/littlehorseboy/openspec-custom-skills` 作為版本徽章。

理由：GitHub release badge 在打 tag 後自動更新，不需要每次手動改 README；靜態 badge（`https://img.shields.io/badge/version-1.2.0-blue`）每次版本升級都要回來手動修改，容易遺漏。

授權徽章使用 `https://img.shields.io/github/license/littlehorseboy/openspec-custom-skills`，它會從 repo 的 `LICENSE` 文件自動讀取授權類型，顯示「MIT」。

備選方案（已排除）：
- 靜態 badge：需要手動維護版本號
- npm badge：`package.json` 雖已宣告 npm 名稱，但尚未 publish，badge 會顯示 404

### 決策 2：圖表 table 只在 openspec-propose-mermaid-html 放一次

`openspec-design-html` 和 `openspec-propose-design-mermaid-html` 的 HTML 產生邏輯完全相同，重複放 table 會造成維護負擔（日後新增圖表類型要改兩處）。`openspec-design-html` section 改為一句話 + 錨點指向 `openspec-propose-design-mermaid-html`。

### 決策 3：README 中英對照欄位排版採 table 形式

使用 Markdown table（`| 類型 Type | 中文名稱 | 文件 Docs |`），兼顧掃讀速度與連結可點擊性。純 bullet list 不易對齊圖表名稱和連結。

## Risks / Trade-offs

- [風險] GitHub release badge 需要至少一個 git release tag 才能顯示版本號，若 repo 目前沒有 tag，badge 顯示「No releases」
  → 緩解：任務中補充說明，實作後請使用者建立第一個 tag（`git tag v1.2.0 && git push origin v1.2.0`）

- [取捨] `openspec-design-html` section 指向另一 section 而非重複內容，讀者需要捲動，但維護成本降低

## Migration Plan

純文件變更，無需 rollback 計畫。
`package.json` `files` 的異動在下次 `npm publish` 前不影響任何已安裝使用者。
