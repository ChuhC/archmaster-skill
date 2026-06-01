# ArchMaster Skill

> 渐进式架构设计 Skill（Interactive Architecture Mode）— 通用的 AI 辅助架构设计 Skill，支持 Cursor、Hermes、Cline、Copilot、Windsurf 等平台。

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](LICENSE)
[![Platform](https://img.shields.io/badge/Platform-通用-orange)]()

---

## 简介 / Introduction

**ArchMaster** 是一个帮助你与 AI 通过结构化对话，渐进式完成需求分析、PRD 规划、架构设计的 Skill。

ArchMaster 不依赖特定工具 — 本质是一份精心设计的 SKILL.md，可以加载到任何支持 Skill 机制（或等效方式）的 AI 编码工具中。

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

## 安装 / 各平台加载方式

ArchMaster 是一个 **Skill**，核心文件只有一个：**SKILL.md**。不同 AI 工具加载 Skill 的方式如下。

### Cursor

Cursor 原生支持 Skill。放到项目目录即可：

```bash
mkdir -p .cursor/skills/archmaster
cp SKILL.md .cursor/skills/archmaster/SKILL.md
```

Cursor 会自动识别。对话中输入 `/archmaster` 激活，或直接描述需求触发。

也可通过界面管理：Settings → Features → Skills → Add Skill。

### Hermes Agent

Hermes 原生支持 Skill 目录：

```bash
mkdir -p ~/.hermes/skills/archmaster
curl -o ~/.hermes/skills/archmaster/SKILL.md \
  https://raw.githubusercontent.com/ChuhC/archmaster-skill/main/SKILL.md
```

重启会话后自动加载。

### Cline

Cline 原生支持 Skills 机制（需在 Cline Settings → Features 中开启 **Enable Skills**）。

**项目级加载**（仅在当前工作区生效）：

```bash
mkdir -p .cline/skills/archmaster
cp SKILL.md .cline/skills/archmaster/SKILL.md
```

**全局加载**（所有项目均可调用）：

```bash
# macOS / Linux
mkdir -p ~/.cline/skills/archmaster
cp SKILL.md ~/.cline/skills/archmaster/SKILL.md
```

### GitHub Copilot

```bash
cp SKILL.md .github/copilot-instructions.md
```

Copilot 会自动读取该文件作为 Skill 加载。

### Claude Code

Claude Code 原生支持 Skill：

```bash
mkdir -p .claude/skills/archmaster
cp SKILL.md .claude/skills/archmaster/SKILL.md
```

对话中 `/archmaster` 激活。

### 通用方式（任何 AI 工具）

如果以上方式都不适用：开启新对话时，将 SKILL.md 全文粘贴作为第一条消息，然后接着描述项目需求即可。

---

## 快速开始 / Quick Start

三步在你的项目中加载 ArchMaster Skill：

```bash
# 1. 创建 Skill 目录（以 Cursor 为例）
mkdir -p .cursor/skills/archmaster

# 2. 下载 SKILL.md
curl -o .cursor/skills/archmaster/SKILL.md \
  https://raw.githubusercontent.com/ChuhC/archmaster-skill/main/SKILL.md

# 3. 在 AI 对话中说：
# 「我想做一个 xxx 系统，帮我开始需求分析」
```

其他工具同理 — 把 SKILL.md 放到对应位置即可（见上方各平台加载方式）。

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

> 💡 `templates/` 目录中提供了上述三个文档的空白模板，可直接复制到项目中使用。

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

SKILL.md 使用 YAML frontmatter + Markdown 格式，不同工具对它的处理方式：

| 工具 | Skill 加载方式 |
|------|---------------|
| Cursor | 原生 Skill 机制（`.cursor/skills/`） |
| Claude Code | 原生 Skill 机制（`.claude/skills/`） |
| Hermes Agent | 原生 Skill 机制（`~/.hermes/skills/`） |
| Cline | 原生 Skill 机制（`.cline/skills/`，需在设置中开启） |
| Copilot | 通过 `.github/copilot-instructions.md` 等效加载 |
| 其他工具 | 将 SKILL.md 全文粘贴到对话开头即可 |

如果你使用的工具因 frontmatter 产生异常，删除 `---` 包裹的头部区域即可，不影响核心功能。

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
