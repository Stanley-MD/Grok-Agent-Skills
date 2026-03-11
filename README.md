# 🧠 AI Skill System

一套为 Grok / Claude 设计的模块化技能体系。

- `skill-router`：统一入口，路由所有请求
- `skill-framework`：创建和维护技能文件
- `content-library`：创建和维护共享内容库

## 建议使用方式（最少上下文）

为保证路由与约束口径一致，建议在同一对话上下文中同时提供：
- `skill-router.md`
- 你要用到的目标技能文件（如 `image-prompt-portrait.md` / `novel-narrator.md`）
- `core-anchors.md`（被多技能引用的共享锚点）
