# Release Notes / 发布说明

## v0.1.2

- 增加 `CodexLogFix-OneClick-Safe.zip`，作为普通用户推荐下载入口。
- 更新 README，说明 raw `.cmd` 链接会在浏览器显示源码，这是 GitHub 的正常行为。

## v0.1.2

- Added `CodexLogFix-OneClick-Safe.zip` as the recommended download for most users.
- Updated the README to explain that raw `.cmd` links may open as source text in the browser, which is normal GitHub behavior.

## v0.1.1

- 修复菜单交互模式，去掉 PowerShell `-NonInteractive` 参数。

## v0.1.1

- Fixed interactive menu mode by removing the PowerShell `-NonInteractive` flag.

## v0.1.0

- 单文件 Windows `.cmd` 工具。
- 中文菜单和中文状态提示。
- 支持生效、恢复默认、查看状态。
- 不内嵌 `sqlite3.exe`，首次运行按需从 SQLite 官方下载。
- 对 Codex `logs_2.sqlite` 添加或删除 `block_log_inserts` 触发器。

## v0.1.0

- Single-file Windows `.cmd` utility.
- Chinese menu and status output.
- Supports apply, restore, and status checks.
- Does not embed `sqlite3.exe`; downloads it from the official SQLite site when needed.
- Adds or removes the `block_log_inserts` trigger in Codex `logs_2.sqlite`.
