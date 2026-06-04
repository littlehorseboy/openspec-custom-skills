# Spec: SKILL.md mindmap 規則新增

## 範圍

適用於以下兩個檔案（規則內容必須一致）：
- `.claude/skills/openspec-propose-design-mermaid-html/SKILL.md`
- `.claude/skills/openspec-design-html/SKILL.md`

---

## 需求

### R1：Section Selection Guide 新增 mindmap 觸發條件

WHEN design.md 描述的變更橫跨多個維度、或需要「範圍概覽 / 功能分類」的無方向性概覽圖

THEN AI 應在 design.html 中加入 mindmap section

**驗收標準**
- Section Selection Guide 表中有一列，信號欄包含「multiple dimensions」或「conceptual overview」，對應 section 欄為「Mind map」
- 此列出現在 State diagram、Class diagram 等既有列之後

---

### R2：Choosing the Right Diagram Type 新增 mindmap 列

WHEN AI 判斷要使用 mindmap 圖表時

THEN SKILL.md 的 `Choosing the Right Diagram Type` 表應提供選用依據

**驗收標準**
- 表格有一列：Design content 欄為「Conceptual overview, feature taxonomy, requirement breakdown」，Best Mermaid type 欄為 `` `mindmap` ``
- 有說明 Why（Radial hierarchy 掃描效率高於 nested bullets）

---

### R3：Mermaid Diagram Rules 新增 mindmap 語法區塊

WHEN AI 生成 mindmap 時

THEN 必須遵循以下語法規則，避免渲染失敗

**驗收標準**
- 有獨立的 mindmap 語法區塊，包含：
  - 純縮排（2 spaces per level），無箭頭說明
  - 節點形狀：`root((...))` = circle、`root[...]` = box、`root(((... )))` = double circle
  - label 長度建議：< 20 chars
  - 適合放置位置：Scope section 旁，不放在 Before/After 對比框內
  - 明確禁止：`style`、`classDef`、`click`（mindmap 不支援）

---

### R4：兩個 SKILL.md 內容一致

WHEN 上述規則套用完成後

THEN 兩個 SKILL.md 的 mindmap 相關段落必須完全一致，不得有遺漏或差異

**驗收標準**
- 三個區塊（Section Selection Guide、Diagram Type 表、Mermaid Rules）在兩個檔案中的文字相同
