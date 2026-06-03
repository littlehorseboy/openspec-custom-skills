# openspec-custom-skills

基於 [OpenSpec](https://github.com/Fission-AI/OpenSpec/) 的個人擴充 skills，加了視覺化設計頁面與一鍵 archive 流程，並搭配繁體中文輸出的 config。

## 使用方式

把想要的 skill 複製到你的專案 `.claude/skills/` 目錄下即可。  
`openspec/config.yaml` 可複製到你的專案 `openspec/config.yaml` 覆蓋語言設定。

需要先安裝 [OpenSpec CLI](https://github.com/Fission-AI/OpenSpec/)。

---

## Skills

### OpenSpec 原生（由 `openspec init` 產生）

| Skill | 說明 |
|-------|------|
| `openspec-propose` | 建立新 change，產生 proposal、design、specs、tasks |
| `openspec-apply-change` | 從現有 change 開始實作任務 |
| `openspec-archive-change` | 封存單一完成的 change |
| `openspec-explore` | 思考夥伴模式，適合 change 前後的探索與釐清 |

### 擴充 Skills

#### `openspec-propose-design-mermaid-html`

`openspec-propose` 的擴充版。執行完全相同的 proposal → design → specs → tasks 流程，**所有 artifacts 完成後**，再額外產生一份 `design.html`，以互動式 Mermaid 圖表呈現設計內容。

頁面結構由 `assets/page-shell.html`（隨 skill 附帶）提供 CSS 與元件範本，依 design.md 內容挑選適合的 section：

- **必選**：Scope（Goals / Non-Goals）、Before vs After、Decisions + Risks
- **按需**：Detail cards（多入口點，含程式碼片段）、Full diagram（class / ER / sequence / state）、Mapping table + 衍生圖、Background logic（共用但不修改的邏輯）

讓 reviewer 掃一眼就能理解 change 的全貌，不需要逐段讀 Markdown。

適合用在：有多個入口點、狀態轉換、資料流向需要視覺化說明的 change。

#### `openspec-complete-archive-change`

一鍵完成已部署 change 的收尾工作：把所有未打勾的 tasks 標為完成、把 delta specs 同步回主 specs、執行 archive。不會問確認——設計給「已上 production，補紙本」的場景。

觸發語：`驗證打勾`、`幫我打勾`、`archive 完成的 change`、`close out`、`finalize change`。

---

## Config（`openspec/config.yaml`）

- 預設以繁體中文（zh-TW）輸出所有文件與回覆
- 程式碼識別字、指令、API 名稱等保留英文原文
- 各 artifact（proposal、spec、tasks）有對應的品質規則：具體可驗證、不得弱化約束條件
