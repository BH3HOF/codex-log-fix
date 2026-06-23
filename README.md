# Codex Log Fix / Codex 日志修复工具

作者 / Author: `BH3HOF`

一个 Windows 单文件小工具，用来缓解 Codex 诊断日志数据库 `logs_2.sqlite` 持续写入 SSD 的问题。

This is a one-file Windows utility that mitigates excessive SSD writes caused by Codex diagnostic logging to `logs_2.sqlite`.

## 下载 / Download

下载并双击运行：

Download and double-click:

```text
CodexLogFix-OneClick-Safe.cmd
```

## 功能 / Features

- 生效：阻止新的 Codex 日志写入
- 恢复默认：允许 Codex 日志写入
- 查看状态：显示日志库大小、WAL 文件状态、日志行数和补丁状态
- 单文件分发：不内嵌可执行文件，降低杀毒软件误报概率

- Apply fix: block new Codex log inserts
- Restore default: allow Codex log inserts again
- Check status: show database size, WAL status, row count, and patch status
- Single-file distribution: does not embed executable binaries, reducing antivirus false positives

## 它做了什么 / What It Does

工具会在下面的 SQLite 数据库里创建一个触发器：

The tool creates a SQLite trigger in:

```text
%USERPROFILE%\.codex\logs_2.sqlite
```

触发器名称：

Trigger name:

```text
block_log_inserts
```

触发器逻辑：

Trigger logic:

```sql
CREATE TRIGGER IF NOT EXISTS block_log_inserts
BEFORE INSERT ON logs
BEGIN
  SELECT RAISE(IGNORE);
END;
```

这会让新的诊断日志插入被忽略。恢复默认时，工具会删除这个触发器。

This ignores new diagnostic log inserts. Restoring the default behavior removes the trigger.

## 使用方法 / Usage

1. 关闭多余的 Codex 桌面窗口、VSCode Codex 会话和 Codex CLI。
2. 双击 `CodexLogFix-OneClick-Safe.cmd`。
3. 在菜单里选择：
   - `1` 生效
   - `2` 恢复默认
   - `3` 查看状态
   - `4` 退出
4. 建议重启 Codex。

1. Close extra Codex Desktop windows, VSCode Codex sessions, and Codex CLI processes.
2. Double-click `CodexLogFix-OneClick-Safe.cmd`.
3. Choose from the menu:
   - `1` Apply fix
   - `2` Restore default
   - `3` Check status
   - `4` Exit
4. Restart Codex if possible.

## sqlite3.exe 来源 / sqlite3.exe Source

这个工具不把 `sqlite3.exe` 嵌进脚本里。首次运行时，如果本机找不到 `sqlite3.exe`，会从 SQLite 官方网站下载 Windows x64 工具包，并缓存到：

This tool does not embed `sqlite3.exe`. On first run, if `sqlite3.exe` is not found locally, it downloads the official Windows x64 SQLite tools package and caches it at:

```text
%LOCALAPPDATA%\CodexLogFix\sqlite3.exe
```

官方页面 / Official page:

```text
https://www.sqlite.org/download.html
```

如果你不希望运行时联网，也可以手动把官方 `sqlite3.exe` 放到脚本同目录。

If you do not want the tool to download anything at runtime, place the official `sqlite3.exe` next to the script.

## 安全说明 / Safety Notes

- 这个工具不会删除你的对话历史。
- 它只修改 Codex 的诊断日志数据库。
- 如果之后需要向 Codex 官方反馈问题，可以先选择“恢复默认”，重新允许日志写入。
- 如果提示数据库被占用，请关闭 Codex 相关进程后再试。

- This tool does not delete your conversation history.
- It only modifies the Codex diagnostic log database.
- If you need to report a Codex issue later, choose "Restore default" first to allow logging again.
- If the database is locked, close Codex-related processes and try again.

## 免责声明 / Disclaimer

这是一个社区临时缓解工具，不是 OpenAI 官方工具。使用前请自行判断风险。

This is a community workaround, not an official OpenAI tool. Use it at your own discretion.
