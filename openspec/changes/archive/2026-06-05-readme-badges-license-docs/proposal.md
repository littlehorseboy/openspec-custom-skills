## Why

README 缺少版本徽章與授權徽章，開源慣例上這兩者是讓訪客在第一眼就能掌握專案狀態的必要元素；另外 MIT 授權聲明只停留在 `package.json` 的 `"license"` 欄位，沒有對應的 `LICENSE` 文件，不符合開源規範。此外，`openspec-propose-design-mermaid-html` 和 `openspec-design-html` 的 README 說明對 `design.html` 能產出哪些 Mermaid 圖表類型描述不足，使用者無法預期輸出內容。

## What Changes

- `README.md` 頂部加入兩個 shields.io 徽章：GitHub release 版本號 + MIT 授權
- 新增 `LICENSE` 文件（MIT，2026，littlehorseboy）
- `README.md` 的 `openspec-propose-design-mermaid-html` section 擴充 `design.html` 說明：
  - 必選 section 保留現有表格
  - 按需 section 改成 bullet list，清晰列出各類型
  - 新增圖表類型 table（8 種 Mermaid 圖表，中英對照，附 mermaid.ai 文件連結，標注渲染引擎為 mermaid.js.org）
- `openspec-design-html` section 改為一句話指回 `openspec-propose-design-mermaid-html`，不重複圖表 table
- `package.json` 的 `files` 陣列加入 `"LICENSE"`

## Capabilities

### New Capabilities

- `repo-open-source-metadata`：README 徽章、LICENSE 文件、package.json files 同步，確保 repo 符合 npm publish 與開源發布的基本規範。
- `readme-diagram-type-reference`：README 的 design.html 圖表類型說明，讓使用者在呼叫 skill 之前就能預期可能產出的 Mermaid 圖表種類及對應文件連結。

### Modified Capabilities

（無現有 spec 需異動）

## Impact

- 影響檔案：`README.md`、`LICENSE`（新增）、`package.json`
- 不影響任何 SKILL.md 邏輯或 `assets/page-shell.html`
- `package.json` 加入 `LICENSE` 到 `files` 後，下次 `npm publish` 會一併打包授權文件
