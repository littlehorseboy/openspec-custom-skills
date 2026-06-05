## ADDED Requirements

### Requirement: openspec-propose-design-mermaid-html section 列出完整 design.html 圖表類型

README.md 的 `openspec-propose-design-mermaid-html` section SHALL 包含一份圖表類型 table，列出 design.html 可能產出的 8 種 Mermaid 圖表，每種圖表 SHALL 提供中英對照名稱與 mermaid.ai 文件連結，並標注渲染引擎來源為 mermaid.js.org。

#### Scenario: 使用者查看 README 預期輸出

- **WHEN** 使用者在 GitHub 閱讀 `openspec-propose-design-mermaid-html` section
- **THEN** 看到 8 種圖表類型的 table，每列包含英文類型名稱、中文名稱、可點擊的 mermaid.ai 文件連結

#### Scenario: 按需 section 改為 bullet list

- **WHEN** 使用者閱讀「按需」說明
- **THEN** 看到 bullet list 格式（非 inline 表格），包含 Detail cards、Mapping table、衍生圖、Full diagrams（子項）、Background logic

#### Scenario: 標注 Mermaid 渲染引擎

- **WHEN** 使用者閱讀圖表說明區塊
- **THEN** 在 table 前或說明文字中看到 mermaid.js.org 的連結說明，清楚表示圖表由 Mermaid 渲染

### Requirement: openspec-design-html section 指向圖表說明而非重複

README.md 的 `openspec-design-html` section SHALL 以一句話指向 `openspec-propose-design-mermaid-html` section 的圖表 table，不重複列出相同內容。

#### Scenario: 讀者從 openspec-design-html 尋找圖表說明

- **WHEN** 使用者閱讀 `openspec-design-html` section
- **THEN** 看到一句引導文字，附有可跳轉的錨點連結，指向 `openspec-propose-design-mermaid-html` 的圖表 table
