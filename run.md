---
description: 开始一个 coding session。从功能清单中选最高优先级的未完成功能，实现、测试，提交并更新进度日志。每次调用推进一个功能。
---

使用 coding-agent 执行一个完整的 coding session。

$ARGUMENTS

## Session 启动流程（必须按顺序执行）

1. `pwd && ls` 确认工作目录
2. 读取 `claude-progress.txt` 了解上次进度
3. `git log --oneline -10` 查看提交历史
4. 读取 `feature_list.json`，选 priority 最小且 passes=false 的功能
5. 执行 `init.sh` 验证开发环境（有问题先修复）

---

## 严格规则

- ❌ 禁止删除或修改 feature_list.json 的任何条目
- ❌ 禁止未测试就标记 passes: true
- ✅ 每次只实现一个功能
- ✅ 按 steps 字段逐步测试

---

## Session 结束前必须完成

1. 将完成功能的 passes 改为 true（只改这一个字段）
2. `git add . && git commit -m "feat: [功能描述]"`
3. 在 claude-progress.txt 末尾追加：
```
────────────────────────────
Session #N  [时间]  编程 Agent
────────────────────────────
完成功能：[描述] ✅
测试结果：[命令] → [输出] ✅
Git commit: [hash] "[message]"
遗留问题：无
下一步：[下个功能]（priority=N）
```

若所有 passes 均为 true，告知用户项目已完成。
