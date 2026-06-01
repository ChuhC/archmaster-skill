# ArchMaster Skill

> 渐进式架构设计 Skill（Interactive Architecture Mode）— 一个面向 Hermes Agent 的 AI 辅助架构设计技能包。

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](LICENSE)
[![Hermes Agent](https://img.shields.io/badge/Hermes%20Agent-Skill-green)](https://hermes-agent.nousresearch.com)

---

## 简介 / Introduction

**ArchMaster** 是一个帮助你与 AI 通过结构化对话，渐进式完成需求分析、PRD 规划、架构设计的 Skill。

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

## 安装 / Installation

### 前置要求

- [Hermes Agent](https://hermes-agent.nousresearch.com) 已安装并正常运行

### 方式一：直接克隆

```bash
# 克隆到 Hermes 的 skills 目录
git clone https://github.com/ChuhC/archmaster-skill.git ~/.hermes/skills/archmaster
```

### 方式二：通过 Hermes CLI 安装（如支持）

```bash
hermes skills install https://github.com/ChuhC/archmaster-skill.git
```

安装后重启 Hermes Agent 会话，Skill 自动加载。

---

## 快速开始 / Quick Start

在 Hermes Agent 对话中，输入类似以下内容即可触发 ArchMaster：

```
帮我设计一个 xxx 系统的架构
```

或者更直接：

```
激活 archmaster skill，我要做一个 xxx 项目
```

ArchMaster 会从 **Phase 1 Step A** 开始，逐步引导你完成整个设计流程。

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

## 贡献 / Contributing

欢迎提交 Issue 和 Pull Request！

1. Fork 本仓库
2. 创建特性分支 (`git checkout -b feature/amazing-improvement`)
3. 提交变更 (`git commit -m 'Add amazing improvement'`)
4. 推送到远程 (`git push origin feature/amazing-improvement`)
5. 创建 Pull Request

如果你在使用中发现问题或有改进建议，也欢迎在 [Issues](https://github.com/ChuhC/archmaster-skill/issues) 中讨论。

---

## 许可 / License

本项目基于 [Apache License 2.0](LICENSE) 开源。

---

## 作者 / Author

**ChuhC** — [GitHub](https://github.com/ChuhC)

- 原始 Gist: [archMaster](https://gist.github.com/ChuhC/25d2b4c662cd0b7442dfd6b3999cb765)

---

## 致谢 / Acknowledgments

- [Hermes Agent](https://hermes-agent.nousresearch.com) — 强大的 AI Agent 平台
- [SEI ATAM](https://resources.sei.cmu.edu/library/asset-view.cfm?assetid=5177) — 架构权衡分析方法论
