## 1. 授權文件與 package.json

- [x] 1.1 在 repo 根目錄新增 `LICENSE` 文件，內容為標準 MIT License，年份 2026，著作人 littlehorseboy
- [x] 1.2 `package.json` 的 `files` 陣列加入 `"LICENSE"`

## 2. README 徽章

- [x] 2.1 在 `README.md` 第一行標題（`# openspec-custom-skills`）下方插入 GitHub release 版本徽章，連結至 repo releases 頁
- [x] 2.2 在版本徽章後插入 MIT 授權徽章，連結至 `LICENSE` 文件
- [x] 2.3 確認兩個徽章的 `img.shields.io` URL 使用正確 repo 名稱（`littlehorseboy/openspec-custom-skills`）

## 3. README design.html 內容說明改進

- [x] 3.1 `openspec-propose-design-mermaid-html` section：在現有必選 table 下方，把「按需 section」改為 bullet list（Detail cards、Mapping table、衍生圖、Full diagrams 子項、Background logic）
- [x] 3.2 在 bullet list 下方新增圖表類型 table（8 種 Mermaid 圖表，中英對照，各附 mermaid.ai 文件連結），並在 table 前一句說明圖表由 [Mermaid](https://mermaid.js.org/) 渲染
- [x] 3.3 `openspec-design-html` section：加入一句引導文字，附錨點連結，指向 `openspec-propose-design-mermaid-html` section 的圖表說明

## 4. 驗證

- [x] 4.1 確認 `LICENSE` 文件存在且內容完整
- [x] 4.2 GitHub 上確認 release badge 顯示正確（若尚無 git tag，執行 `git tag v1.2.0 && git push origin v1.2.0` 建立第一個 tag）
- [x] 4.3 README 在 GitHub preview 上徽章正常顯示、連結可點擊
- [x] 4.4 README 圖表 table 的 mermaid.ai 連結均可正常開啟
