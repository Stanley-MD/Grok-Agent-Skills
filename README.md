# 🧠 AI Skill System

一套为 Grok / Claude 设计的模块化技能体系，通过结构化的技能文件让 AI 稳定执行复杂任务。

---

## 概览

本体系由**技能文件**和**内容库文件**两类组件构成。技能文件定义 AI 的执行逻辑，内容库文件存放跨技能共享的静态内容。所有技能通过 `skill-router` 统一调度。

```
用户输入 → skill-router → 匹配技能 → 结构化输出
```

---

## 技能列表

### 🗂 体系管理

| 技能 | 版本 | 说明 |
|------|------|------|
| [`skill-router`](skill-router.md) | v1.1 | 统一入口，将用户输入路由到最合适的技能 |
| [`skill-framework`](skill-framework.md) | v1.3 | 创建、修改、审查技能文件的管理工具 |
| [`content-library`](content-library.md) | v1.1 | 创建和维护跨技能共享的内容库文件 |

### 🖼 图像提示词生成（Grok Imagine）

| 技能 | 版本 | 说明 |
|------|------|------|
| [`image-prompt-portrait`](image-prompt-portrait.md) | v1.1 | 单张东亚人物写真提示词 |
| [`image-prompt-catalog`](image-prompt-catalog.md) | v1.1 | 日系时尚目录排版图提示词（四格 inset + 全身主图） |
| [`image-prompt-video`](image-prompt-video.md) | v1.1 | 图生视频提示词，描述动态变化与故事性演进 |

### 📖 互动小说

| 技能 | 版本 | 说明 |
|------|------|------|
| [`novel-setup`](novel-setup.md) | v1.1 | 生成互动小说的完整设定文档 |
| [`novel-narrator`](novel-narrator.md) | v1.1 | 基于设定文档执行叙述、状态管理与选项生成 |

### ⚙️ 实用工具

| 技能 | 版本 | 说明 |
|------|------|------|
| [`task-scheduler`](task-scheduler.md) | v1.1 | 将定期任务需求转化为结构化定时任务指令 |
| [`web-research`](web-research.md) | v1.1 | 多源交叉验证的网络信息研究与事实核查 |
| [`fengshui-analyzer`](fengshui-analyzer.md) | v1.1 | 基于峦头形法与玄空飞星的阳宅风水分析 |

### 👤 用户偏好

| 技能 | 版本 | 说明 |
|------|------|------|
| [`preference-profiler`](preference-profiler.md) | v1.1 | 渐进式访谈，生成结构化个人偏好画像 |
| [`preference-override`](preference-override.md) | v1.1 | 对话级临时偏好覆盖，不影响持久化设定 |

### 📦 内容库

| 文件 | 版本 | 说明 |
|------|------|------|
| [`core-anchors`](core-anchors.md) | v1.1 | 共享内容库：用户偏好锚点、防卡死总则、视觉合规红线 |

---

## 快速开始

**1. 启动路由**

将所需技能文件的内容粘贴到对话上下文中，告知 AI「启动 skill-router」，路由器即就绪，后续请求会自动匹配并激活对应技能。

**2. 新建或修改技能**

触发 `skill-framework`，描述你的需求，它会引导你完成定义、审查和测试全流程。

**3. 运行互动小说**

```
步骤一：触发 novel-setup，按引导生成设定文档
步骤二：将设定文档发给 AI 并说「开始游戏」
步骤三：novel-narrator 接管叙述，持续推进剧情
```

---

## 技能文件结构

每个技能文件遵循统一规范：

```markdown
---
name: skill-name
description: 触发条件与功能说明
---

# 技能名称
## 角色设定
## 核心工作流
## 约束
## 输出规格
## 版本演进
```

详见 [`skill-framework.md`](skill-framework.md) 中的完整写法参考。

---

## 版本管理

所有文件内置版本演进表，记录每次变更的内容与原因。版本号由用户确认保存后正式生效，草稿输出不计入历史记录。

当前版本：`skill-framework` 为 **v1.3**，其余所有技能与内容库均为 **v1.1**。

---

## 合规机制

本体系在两个层面内置合规保障：

- **视觉合规红线**（`core-anchors` 章节3）：适用于所有图像生成技能，规定角色视觉年龄、禁止内容类型及描写边界
- **防卡死总则**（`core-anchors` 章节2）：适用于互动小说技能，防止叙述陷入循环或卡死状态

两个层面独立运作，由各技能在执行前主动读取并遵守。

---

## 未来展望

当前体系已覆盖图像生成、叙事创作、信息研究、任务调度等核心场景，架构演进方向包括：

- **技能分层**：将体系管理类（skill-router、skill-framework）与执行类技能明确分层，支持更复杂的嵌套调用与组合模式
- **内容库扩展**：core-anchors 目前承载用户偏好、防卡死规则、视觉合规三类内容，随体系规模增长，考虑按职责拆分为独立内容库文件，降低耦合
- **跨平台适配**：现有提示词技能针对 Grok Imagine 优化，后续计划扩展对 Midjourney、DALL·E、Stable Diffusion 等平台的专项支持
- **技能自测框架**：在 skill-framework 的测试流程基础上，建立标准化的 eval 用例集，让每个技能都有可复现的质量基准
