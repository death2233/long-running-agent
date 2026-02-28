---
description: 初始化长运行 Agent 项目。分析需求，生成功能清单、项目骨架、init.sh 和进度文件，为后续 coding session 铺路。用法：/long-running-agent:init <需求描述>
---

使用 initializer-agent 来初始化本项目。

## 用户需求
$ARGUMENTS

## 必须按顺序完成

### 第一步：生成 feature_list.json
将需求拆解为细粒度功能清单，每条功能 1-3 小时可完成。
格式：
```json
{
  "project": "项目名称",
  "created_at": "日期",
  "features": [
    {
      "category": "infrastructure",
      "priority": 1,
      "description": "功能描述",
      "steps": ["curl http://... → 返回200", "验证字段X存在"],
      "passes": false
    }
  ]
}
```
所有 passes 必须为 false。至少拆解 5 个功能点。

### 第二步：创建项目骨架
根据技术栈创建目录结构和配置文件，不要实现业务逻辑。

### 第三步：创建 init.sh
```bash
#!/bin/bash
# 安装依赖
# 启动开发服务器
# 健康检查
```

### 第四步：创建 claude-progress.txt
```
=== Session #1 [时间]  初始化 Agent ===
完成内容：生成 N 个功能点，创建项目骨架
下一步建议：从 priority=1 开始
```

### 第五步：Git 初始化
```bash
git init && git add . && git commit -m "init: 项目初始化，共 N 个功能待实现"
```

## 完成后告知用户
- 生成了多少功能点
- 运行 `/long-running-agent:run` 开始第一个 session
