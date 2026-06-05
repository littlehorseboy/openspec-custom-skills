## ADDED Requirements

### Requirement: README 頂部顯示版本與授權徽章

README.md 第一行標題下方 SHALL 緊接兩個 shields.io 徽章：GitHub release 版本號徽章與 MIT 授權徽章，均帶有超連結。

#### Scenario: 顯示版本徽章

- **WHEN** 訪客開啟 GitHub README 頁面
- **THEN** 看到版本徽章，顯示最新 GitHub release tag 的版本號（若無 tag 則顯示「No releases」）

#### Scenario: 顯示授權徽章

- **WHEN** 訪客開啟 GitHub README 頁面
- **THEN** 看到 MIT 授權徽章，點擊後導向 repo 根目錄的 `LICENSE` 文件

### Requirement: repo 根目錄存在標準 MIT LICENSE 文件

repo 根目錄 SHALL 包含一份 `LICENSE` 文件，內容為標準 MIT License 文字，年份為 2026，著作人為 littlehorseboy。

#### Scenario: LICENSE 文件可被讀取

- **WHEN** 訪客點擊 GitHub repo 的 License 顯示區域
- **THEN** 顯示 MIT License 完整文字，包含正確年份與著作人名稱

#### Scenario: shields.io 授權徽章自動識別

- **WHEN** GitHub 讀取 repo 根目錄的 `LICENSE` 文件
- **THEN** `img.shields.io/github/license/littlehorseboy/openspec-custom-skills` 顯示「MIT」

### Requirement: package.json files 陣列包含 LICENSE

`package.json` 的 `files` 陣列 SHALL 包含 `"LICENSE"`，確保 npm publish 時授權文件被打包進 tarball。

#### Scenario: npm pack 包含 LICENSE

- **WHEN** 執行 `npm pack`
- **THEN** 產生的 tarball 內包含 `LICENSE` 文件
