# Design: 新增 mindmap 圖表類型支援

## Goals / Non-Goals

**Goals**
- 讓 AI 在產出 design.html 時，能正確選用 mindmap 呈現多維概覽
- 提供明確的 mindmap 語法規則，避免生出不合法的 Mermaid 語法
- 兩個 skill（openspec-propose-design-mermaid-html、openspec-design-html）行為對齊

**Non-Goals**
- 不升級 Mermaid CDN 版本
- 不修改 page-shell.html 的 CSS 或 JS
- 不影響其他五個 skill

---

## Context

### Skill 架構

兩個 skill 各自有：
- `SKILL.md` — AI 執行指令，含圖表選用邏輯與 Mermaid 語法規則
- `assets/page-shell.html` — HTML 模板，含 CSS 和各 section 的 example comment

兩個 page-shell.html 在修改前完全相同（MD5 一致），設計上應保持同步。

### 現有圖表類型覆蓋

修改前，SKILL.md 的 `Choosing the Right Diagram Type` 表有六種類型：

| 類型 | 適用場景 |
|------|---------|
| flowchart | 資料流、程式路徑 |
| stateDiagram-v2 | 狀態轉換 |
| classDiagram | 服務 / 類別結構 |
| erDiagram | 資料模型 |
| sequenceDiagram | API 時序 |
| block-beta / graph | 設定樹、巢狀分類 |

**缺口**：當變更橫跨多維（例如「同時影響 SQL SP、C# 服務、前端 API 三層」），或設計者需要一個無方向性的概覽圖時，以上六種都不合適。flowchart 強制有方向，block-beta 語法複雜，nested bullets 在 HTML 呈現中掃描效率低。

### mindmap 的特性

- Mermaid 11 原生支援，無需額外載入
- 純縮排語法，沒有箭頭、沒有特殊字元需要 quote
- 不支援 `style`、`classDef`、`click`
- 適合呈現「範圍概覽、分類層次、功能分組」，不適合有方向性的流程

---

## Decisions

### D1：以純加法修改，不改現有規則結構

在 SKILL.md 的兩張表各補一列、在 Mermaid Diagram Rules 加一個新語法區塊，不重寫現有段落。

**理由**：風險最低，不影響已有圖表行為；AI 在閱讀 SKILL.md 時，mindmap 規則在獨立區塊中，不會和其他圖表規則混淆。

**棄用**：把 mindmap 併入 block-beta 那列說明 → 語意模糊，AI 不易區分兩者的適用場景。

### D2：在 Section Selection Guide 新增觸發訊號，而非僅在圖表表格列出

同時在兩張表都加入 mindmap：
1. Section Selection Guide（什麼情境下加這個 section）
2. Choosing the Right Diagram Type（確認語法）

**理由**：AI 閱讀 SKILL.md 的順序是先看 Section Selection Guide 決定「加不加」，再看 Diagram Type 表決定「用哪種」。只改後者，前者沒有觸發條件，AI 不會主動選用。

### D3：mindmap 定位為 Scope 區旁的概覽，不進 Before/After

SKILL.md 中明確說明：mindmap 適合放在 Scope section 旁，不適合放在 Before/After 對比框。

**理由**：mindmap 無法表達紅/綠樣式（不支援 style），Before/After 的視覺對比靠 `cmp-panel.before/after` 配色；強行放入會破壞對比結構，失去 mindmap 的概覽意義。

### D4：page-shell.html 補 EXAMPLE ⑧，同步更新兩個 skill

新增 mindmap 的 example comment block，讓 AI 生成 HTML 時有模板可對照。同時在 section 索引列表補齊 ⑦ Background Logic 和 ⑧ Mindmap（⑦ 原本只在 example 中，未進索引）。

---

## Risks / Trade-offs

| 風險 | 說明 | 緩解 |
|------|------|------|
| mindmap label 過長導致 radial layout 破版 | mindmap 節點文字超長時，SVG 渲染會溢出或重疊 | SKILL.md 明確限制 label < 20 chars |
| AI 濫用 mindmap 取代 flowchart | mindmap 沒有方向，若誤用在有流程的場景，會失去因果關係的表達 | Section Selection Guide 的觸發訊號寫「多維概覽」，與 flowchart 的「資料流/程式路徑」明確區分 |
| 兩個 page-shell.html 未來不同步 | 兩個 skill 的 shell 邏輯上應相同，手動維護易漂移 | 此次同步更新；建議未來考慮共用單一 shell 檔案（Non-Goal for this change） |
