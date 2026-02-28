---
name: incremental-progress
description: 当 coding session 即将结束、context 接近上限，或用户说"记录进度"/"保存进度"/"收尾"时自动激活。确保交接材料完整，下一个 agent 能无缝接班。
triggers:
  - "记录进度"
  - "保存进度"
  - "收尾"
  - "session 结束"
  - "context 不足"
---

## Session 收尾规范

在结束当前 session 前，必须完成以下交接材料：

### 第一步：更新 feature_list.json

若当前功能已完成，将对应条目的 `passes` 改为 `true`（仅改这一个字段，禁止修改其他内容）。

若功能未完成，保持 `passes: false`，不做任何修改。

### 第二步：Git 提交

```bash
# 功能完成
git add . && git commit -m "feat: [功能描述]"

# 功能未完成（WIP）
git add . && git commit -m "wip: [功能描述] - [做到哪一步]"
```

### 第三步：追加 claude-progress.txt

在文件末尾追加本次 session 记录：

```
────────────────────────────────────
Session #N  [ISO时间]  编程 Agent
────────────────────────────────────
完成功能：[描述] ✅  /  未完成：[描述] 🚧
测试结果：[命令] → [输出]
Git commit: [hash] "[message]"
遗留问题：[如有，详细说明做到哪一步]
下一步：[下个功能或继续当前功能]（priority=N）
```

### 完成后告知用户

```
✅ Session 收尾完成

进度已记录，git 已提交。
下次运行 /long-running-agent:run 继续开发。
```
