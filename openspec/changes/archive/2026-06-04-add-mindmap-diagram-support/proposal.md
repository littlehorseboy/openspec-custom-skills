# Proposal: 新增 mindmap 圖表類型支援

## 問題與動機

`openspec-propose-design-mermaid-html` 和 `openspec-design-html` 兩個 skill 原本提供六種 Mermaid 圖表類型（flowchart、stateDiagram-v2、classDiagram、erDiagram、sequenceDiagram、block-beta/graph），但缺少 **mindmap（心智圖）** 支援。

當一個變更橫跨多個維度，或需要「一眼看懂變更範圍」的概覽時，mindmap 是最自然的表達方式——比巢狀 bullet list 更快掃描，比 flowchart 更適合沒有方向性的分類結構。沒有 mindmap 支援，AI 在產出 design.html 時會略過這類需求，或用不合適的圖表替代，降低頁面的溝通效率。

## What Changes

### SKILL.md（兩個 skill 同步修改）

1. **Section Selection Guide** — 新增一列觸發條件：
   > 「Change spans multiple dimensions / concepts need a conceptual overview → Mind map」

2. **Choosing the Right Diagram Type** — 新增一列：
   > `mindmap` ← Conceptual overview, feature taxonomy, requirement breakdown（Radial hierarchy — scans faster than nested bullets）

3. **Mermaid Diagram Rules** — 新增 mindmap 專屬語法規則區塊，涵蓋：
   - 純縮排語法（2 spaces per level），無箭頭
   - 節點形狀語法（`((...))` / `[...]` / `(((...)))`）
   - label 長度建議（< 20 chars）
   - 適合放置位置（Scope 區旁，不放在 Before/After 對比裡）
   - 明確禁止 `style`、`classDef`、`click`（mindmap 不支援）

### page-shell.html（兩個 skill 同步修改）

1. **Section 列表註解** — 補齊 `⑦ BACKGROUND LOGIC` 和 `⑧ MINDMAP` 兩行說明（⑦ 原本只在 example 裡，未列入索引）

2. **EXAMPLE ⑧** — 新增 mindmap HTML 範例 comment block，示範：
   - 正確的 `<div class="mermaid">` 包法
   - 2-space 縮排結構
   - `root((Change Name))` 語法
   - 使用時機說明

## 非目標（Non-Goals）

- 不修改 Mermaid CDN 版本（Mermaid 11 已原生支援 mindmap，無需升版）
- 不修改 page-shell.html 的 CSS（現有 `.mermaid svg { max-width:100% }` 已足夠）
- 不影響其他五個 skill（openspec-propose、openspec-apply-change 等）

## 受影響範圍

| 檔案 | 類型 |
|------|------|
| `.claude/skills/openspec-propose-design-mermaid-html/SKILL.md` | 修改 |
| `.claude/skills/openspec-design-html/SKILL.md` | 修改 |
| `.claude/skills/openspec-propose-design-mermaid-html/assets/page-shell.html` | 修改 |
| `.claude/skills/openspec-design-html/assets/page-shell.html` | 修改 |

## 風險與取捨

- **風險低**：mindmap 是純加法，不動現有圖表規則，不破壞已有行為
- **取捨**：mindmap 不支援樣式，可視化彈性較低；選用時機需靠 SKILL.md 的觸發條件引導，避免濫用在有方向性需求的場景
