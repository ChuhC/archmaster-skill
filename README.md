# ArchMaster Skill

> 渐进式架构设计 Skill（Interactive Architecture Mode）— 通用的 AI 辅助架构设计技能包，适用于 Hermes Agent、Cursor、Cline、Copilot 等主流 AI 编码工具。

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](LICENSE)
[![Platform](https://img.shields.io/badge/Platform-通用-orange)]()

---

## 简介 / Introduction

**ArchMaster** 是一个帮助你与 AI 通过结构化对话，渐进式完成需求分析、PRD 规划、架构设计的 Skill。

ArchMaster **不依赖特定 AI 工具** — 它本质上是一份精心设计的 Markdown 指令集（SKILL.md），你可以将其加载到任何支持自定义指令 / Rules / System Prompt 的 AI 编码工具中。

借助 **SDD（Specification-Driven Development，规约驱动开发）** 的工程化思想，ArchMaster 帮你理清：

- 你到底想做什么？
- 能做到什么程度？
- 怎样合理地设计架构？

核心目标是 **消除 AI 与用户想法预期之间的不一致**，让架构设计从「拍脑袋」变成「有据可循」。

---

## 特性 / Features

- **门控流程**：Phase 1（需求）→ Phase 1.5（PRD，可选）→ Phase 2（架构），严格分步，禁止跳步
- **单议题讨论**：每轮只讨论一个点，形成共识或待验证，不悬空
- **观点交锋**：AI 不只记录，更会挑战假设、指出问题、提出替代方案
- **多方案选型**：技术选型必须对比 ≥2 种方案，说明收益与代价，用户拍板
- **EA 视图成图**：Phase 2 产出五张 EA 风格架构图（PNG 优先）
- **文档沉淀**：所有讨论最终写入 `requirements.md`、`prd-sketch.md`、`architecture.md`

---

## 安装 / 各平台使用方式

ArchMaster 的核心文件只有一个：**SKILL.md**。根据你使用的 AI 工具选择对应的加载方式。

### Hermes Agent

```bash
# 克隆到 skills 目录
git clone https://github.com/ChuhC/archmaster-skill.git ~/.hermes/skills/archmaster

# 或通过 CLI（如支持）
hermes skills install https://github.com/ChuhC/archmaster-skill.git
```

重启会话后自动加载。对话中输入「帮我设计一个 xxx 系统」即可触发。

### Cursor

**方式一：作为 Rule 文件（推荐）**

将 `SKILL.md` 复制到项目的 `.cursor/rules/` 目录：

```bash
# 在项目根目录
mkdir -p .cursor/rules
cp SKILL.md .cursor/rules/archmaster.md
```

然后在 Cursor 设置 → Rules 中启用该规则。使用时在对话中 @ 引用该 rule，或直接说「按照 archmaster 规则帮我设计架构」。

**方式二：作为全局 Rule**

Cursor Settings → General → Rules for AI，将 `SKILL.md` 的内容粘贴进去。全局生效，适用于所有项目。

### Cline (VS Code 扩展)

**方式一：作为自定义指令**

Cline 设置 → Custom Instructions，将 `SKILL.md` 的内容粘贴到「Custom Instructions」文本框中。之后每次对话都会加载这些指令。

**方式二：作为 .clinerules 文件**

```bash
# 在项目根目录
cp SKILL.md .clinerules
```

Cline 会自动读取项目根目录的 `.clinerules` 文件作为系统指令。

### GitHub Copilot / Copilot Chat

**方式一：项目级指令**

```bash
cp SKILL.md .github/copilot-instructions.md
```

Copilot 会自动读取该文件作为项目级指令。

**方式二：VSCode 工作区设置**

在 `.vscode/settings.json` 中配置：

```json
{
  "github.copilot.chat.codeGeneration.instructions": [
    { "file": ".github/copilot-instructions.md" }
  ]
}
```

### Windsurf / Augment / 其他 AI IDE

大多数现代 AI IDE 都支持项目级规则文件。常见文件名：
- `.cursorrules` / `.cursor/rules/*.md`
- `.clinerules`
- `.github/copilot-instructions.md`
- `.windsurfrules`
- `CLAUDE.md`（Claude Code）
- `AGENTS.md`

直接将 `SKILL.md` 的内容复制或重命名为上述文件名放到项目根目录即可。

### 通用方式（任何 AI 工具）

如果上述方式都不适用，最简单的方法是：**开启新对话时，直接粘贴 SKILL.md 的全部内容作为第一条消息**，然后接着描述你的项目需求。

```
（粘贴 SKILL.md 全文）

---
请按照以上规则，帮我设计一个 xxx 系统。
```

---

## 快速开始 / Quick Start

以 Cursor 为例，三步开始：

```bash
# 1. 在项目中创建 rules 目录
mkdir -p .cursor/rules

# 2. 下载 SKILL.md
curl -o .cursor/rules/archmaster.md \
  https://raw.githubusercontent.com/ChuhC/archmaster-skill/main/SKILL.md

# 3. 在 Cursor 对话中说：
# 「按照 archmaster 规则，我想做一个 xxx 系统，帮我开始需求分析」
```

其他工具同理 — 本质都是把 SKILL.md 加载为 AI 的系统指令。

---

## 工作流概览 / Workflow

```text
Phase 1: 需求分析
├─ Step A: 需求理解（AI 复述）
├─ Step B: 需求讨论（逐议题、挑战观点）
├─ Step C: 发散扩视角
├─ Step D: 需求确认并输出 requirements.md
└─ Step E: 询问是否进入 Phase 1.5

Phase 1.5: PRD 界面与交互设计（可选）
├─ Step A: 设计理解
├─ Step B1: 推导议题清单
├─ Step B2: 逐议题讨论
├─ Step C: 撰写 prd-sketch.md
├─ Step D: 定稿 + 需求回写
└─ Step E: 进入 Phase 2

Phase 2: 系统架构设计
├─ Step A: 架构约束与复杂度建模（ATAM 质量属性）
├─ Step B1-B5: 五张 EA 视图交互讨论
│   ├─ B1: 系统上下文图
│   ├─ B2: 模块划分图
│   ├─ B3: 核心流程图
│   ├─ B4: 核心数据流图
│   └─ B5: 物理部署视图
└─ Step C: 输出 architecture.md + 五张 EA 视图图
```

### 输出产物

所有产物默认写入项目 `docs/` 目录：

| 产物 | 路径 | 阶段 |
|------|------|------|
| 需求文档 | `docs/requirements/requirements.md` | Phase 1 |
| PRD 草图 | `docs/design/prd-sketch.md` | Phase 1.5（可选） |
| 架构文档 | `docs/architecture/architecture.md` | Phase 2 |
| 架构视图 | `docs/architecture/images/*.png` | Phase 2 |

---

## 核心规则 / Core Rules

| 规则 | 说明 |
|------|------|
| Rule 1: 门控 | Phase → Step 严格顺序，禁止跳步 |
| Rule 2: 单议题 | 每轮一个讨论点，不跑题 |
| Rule 3: 观点 | AI 必须表达观点、挑战假设 |
| Rule 4: 收敛 | 每议题 ✅ 共识 或 ⚠ 待验证 |
| Rule 5: 简单优先 | 单体 > 微服务，需要证据才升级复杂度 |
| Rule 6: 文档优先 | 对话是过程，文档是结果 |
| Rule 7: 步骤门控 | 每个 Step 等用户确认再继续 |
| Rule 8: 技术选型多方案 | ≥2 方案对比，用户拍板 |

---

## 兼容性说明

SKILL.md 使用 YAML frontmatter + Markdown 格式。不同工具对 frontmatter 的处理：

| 工具 | frontmatter 处理方式 |
|------|---------------------|
| Hermes Agent | 原生解析，读取 name/description/metadata |
| Cursor / Cline | 通常忽略 frontmatter，当作正文的一部分 |
| Copilot | 忽略 YAML，读取全部 Markdown 内容 |
| 通用粘贴 | 全部作为对话上下文读入 |

frontmatter 中的元数据不影响核心指令的生效。如果你使用的工具因 frontmatter 产生异常，删除 `---` 包裹的头部区域即可，不影响功能。

---

## 贡献 / Contributing

欢迎提交 Issue 和 Pull Request！

1. Fork 本仓库
2. 创建特性分支 (`git checkout -b feature/amazing-improvement`)
3. 提交变更 (`git commit -m 'Add amazing improvement'`)
4. 推送到远程 (`git push origin feature/amazing-improvement`)
5. 创建 Pull Request

特别欢迎：
- 补充在其他 AI 工具（Windsurf、Augment、CodeBuddy 等）上的实测经验
- 提交兼容性问题或改进建议

---

## 许可 / License

本项目基于 [Apache License 2.0](LICENSE) 开源。

---

## 作者 / Author

**ChuhC** — [GitHub](https://github.com/ChuhC)

- 原始 Gist: [archMaster](https://gist.github.com/ChuhC/25d2b4c662cd0b7442dfd6b3999cb765)
