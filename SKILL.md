---
name: session-kickoff
description: 当用户开始编程任务、说"继续上次"/"接着做"/"下一个功能"，或项目目录存在 claude-progress.txt 和 feature_list.json 时自动激活。提供 session 启动标准流程。
---

## Long-Running Agent Session 启动规范

开始工作前完成"接班检查"：

```bash
# 1. 确认工作目录
pwd && ls -la

# 2. 读取进度日志（重点：上次做了什么？有什么遗留问题？）
cat claude-progress.txt

# 3. 查看 Git 历史
git log --oneline -10

# 4. 读取功能清单，找 priority 最小且 passes=false 的功能
cat feature_list.json

# 5. 验证开发环境
bash init.sh
```

### 接班检查完成后汇报

```
📋 接班检查完成

项目进度：N/M 功能完成
上次工作：[描述]
遗留问题：[如有]
本次目标：priority=N [功能描述]
开发环境：正常 ✅

开始实现...
```
