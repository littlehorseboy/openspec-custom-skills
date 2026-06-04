# Tasks: 新增 mindmap 圖表類型支援

## T1：更新 openspec-propose-design-mermaid-html/SKILL.md

- [x] 在 `Section Selection Guide` 觸發條件表新增一列：「Change spans multiple dimensions / concepts need a conceptual overview → Mind map」
- [x] 在 `Choosing the Right Diagram Type` 表新增一列：`mindmap` ← Conceptual overview, feature taxonomy, requirement breakdown（Why: Radial hierarchy）
- [x] 在 `Mermaid Diagram Rules` 新增 mindmap 語法規則區塊，涵蓋縮排語法、節點形狀、label 長度、放置位置、禁用指令（style / classDef / click）

## T2：更新 openspec-design-html/SKILL.md

- [x] 同 T1，將相同的三個段落套用到 `openspec-design-html/SKILL.md`
- [x] 確認兩個 SKILL.md 的 mindmap 相關段落文字一致

## T3：更新 openspec-propose-design-mermaid-html/assets/page-shell.html

- [x] 在 `SECTIONS GO HERE` 索引列表補齊 `⑦ BACKGROUND LOGIC` 和 `⑧ MINDMAP` 兩行
- [x] 在 `EXAMPLE ⑥` 之前新增 `EXAMPLE ⑧` mindmap comment block（含使用時機說明、完整 `<section>` HTML 範例）

## T4：更新 openspec-design-html/assets/page-shell.html

- [x] 同 T3，套用相同變更到 `openspec-design-html/assets/page-shell.html`
- [x] 確認兩個 page-shell.html 的 mindmap 相關段落一致（可用 MD5 hash 驗證）

## T5：驗證

- [x] 開一個測試用 design.md，內含「多維概覽需求」，用 `openspec-design-html` 產出 design.html，確認 mindmap section 被正確生成且瀏覽器渲染無誤
- [x] 確認 mindmap 語法不包含 `style` 或 `classDef`，Mermaid 不報錯
