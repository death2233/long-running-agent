# long-running-agent 插件

Claude Code 插件，实现跨多个 context window 的长运行编程 Agent 工作流。

> 基于 [Anthropic 工程博客：Effective harnesses for long-running agents](https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents)

## 安装

```bash
# 本地开发测试（直接用 --plugin-dir 无需安装）
claude --plugin-dir /path/to/long-running-agent-plugin

# 或放到 GitHub 后用 /plugin install 安装
/plugin install your-github/long-running-agent-plugin
```

## 使用方法

### 1. 初始化项目（只需一次）
```
/long-running-agent:init 构建一个 Todo List REST API，使用 .NET Core + SQLite
```

### 2. 每次 coding session
```
/long-running-agent:run
```

### 3. 查看进度
```
/long-running-agent:status
```

## 插件组件

| 组件 | 文件 | 作用 |
|------|------|------|
| Command | commands/init.md | 初始化项目 |
| Command | commands/run.md | 运行一个 coding session |
| Command | commands/status.md | 查看进度 |
| Agent | agents/initializer-agent.md | 初始化专职 agent |
| Agent | agents/coding-agent.md | 编程专职 agent |
| Skill | skills/session-kickoff/ | 自动触发：session 启动规范 |
| Skill | skills/incremental-progress/ | 自动触发：session 结束交接 |
| Hook | hooks/ | 写文件后校验 feature_list.json |

## 项目核心文件

| 文件 | 作用 |
|------|------|
| `feature_list.json` | 功能任务板，passes: true/false 追踪进度 |
| `claude-progress.txt` | 跨 session 进度日志，新 agent 的"交接班文件" |
| `init.sh` | 一键启动开发环境 |
