# Spec: page-shell.html mindmap example 新增

## 範圍

適用於以下兩個檔案（內容必須保持同步）：
- `.claude/skills/openspec-propose-design-mermaid-html/assets/page-shell.html`
- `.claude/skills/openspec-design-html/assets/page-shell.html`

---

## 需求

### R1：Section 索引列表補齊 ⑦ 和 ⑧

WHEN AI 讀取 page-shell.html 的 section 索引 comment 時

THEN 應能在列表中看到全部可用的 section 類型，包含 Background Logic 和 Mindmap

**驗收標準**
- `SECTIONS GO HERE` comment block 的索引列表包含：
  - `⑦ BACKGROUND LOGIC (shared/unchanged algorithm — context for Before vs After)`
  - `⑧ MINDMAP (conceptual overview — change scope at a glance, feature taxonomy)`
- 兩行出現在 `⑥ DECISIONS + RISKS` 之後

---

### R2：新增 EXAMPLE ⑧ mindmap comment block

WHEN AI 要生成包含 mindmap 的 design.html section 時

THEN 應有可參考的 HTML 模板

**驗收標準**
- 有 `<!-- EXAMPLE ⑧ — Mindmap ... -->` comment block
- Block 內包含：
  - 使用時機說明（spans multiple dimensions，place after Scope section）
  - 明確說明 indentation is the ONLY structure
  - 節點形狀對照說明
  - 一個可直接複製的完整 `<section>` HTML 範例，內含 `<div class="mermaid">` 和 mindmap 語法
- EXAMPLE ⑧ 位置：在 `EXAMPLE ⑥` 之前（與 SKILL.md 的說明順序一致）

---

### R3：兩個 page-shell.html 保持同步

WHEN 修改完成後

THEN 兩個 page-shell.html 的 mindmap 相關段落必須完全一致

**驗收標準**
- 兩個檔案的 section 索引列表和 EXAMPLE ⑧ block 文字相同
- MD5 hash 相同（或 diff 為零）
