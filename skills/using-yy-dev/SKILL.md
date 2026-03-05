---
name: using-yy-dev
description: Use when starting any conversation in a project with yy-dev — introduces available workflows and guides skill selection
---

# yy-dev: 规格驱动开发工作流

yy-dev 提供结构化的开发工作流，包含项目记忆（steering）和规格驱动流程。

## 可用工作流

### 日常开发
| 命令 | 使用场景 |
|------|---------|
| `/yy:init` | 首次设置 — 创建项目 steering（产品、技术、结构） |
| `/yy:feature "描述"` | 实现功能 — 自动评估规模，走 TDD 直接实现或生成计划 |
| `/yy:fix "描述"` | 修复 Bug — TDD 修复 + 自动代码审查 |
| `/yy:investigate "描述"` | 诊断问题 — 4 阶段系统化调试 |
| `/yy:steering` | 初始化或同步项目 steering |
| `/yy:status [名称]` | 查看规格状态和进度 |

### 正式规格流水线（大功能 / 新项目）
| 命令 | 使用场景 |
|------|---------|
| `/yy:spec-requirements <名称>` | 生成 EARS 格式需求文档 |
| `/yy:spec-design <名称> [-y]` | 生成技术设计（含调研） |
| `/yy:spec-tasks <名称> [-y]` | 生成实现任务列表 |
| `/yy:spec-impl <名称> [任务号]` | TDD 实现任务 |

### 验证
| 命令 | 使用场景 |
|------|---------|
| `/yy:validate-gap <名称>` | 需求与现有代码的差距分析 |
| `/yy:validate-design <名称>` | 技术设计质量评审（GO/NO-GO） |
| `/yy:validate-impl <名称>` | 验证实现是否符合规格 |

## 工作原理

1. **Steering**（`.yy-dev/steering/`）= 持久化项目记忆（产品、技术、结构）
2. **Specs**（`.yy-dev/specs/`）= 决策记录和功能文档
3. **工作流**委托 superpowers 技能执行（TDD、代码审查、头脑风暴、计划）

## 技能选择指南

- 用户说"加 X" / "实现 Y" / "搞一个 Z" → 调用 `yy:feature`
- 用户说"修复" / "bug" / "坏了" / "报错" → 调用 `yy:fix`
- 用户说"调查" / "为什么" / "诊断" / "debug" → 调用 `yy:investigate`
- 用户提到"需求" / "设计" / "规格" → 调用对应的 spec 技能
- 用户说"状态" / "进度" → 调用 `yy:status`

## 核心原则

yy-dev 负责编排；superpowers 负责执行。当工作流需要 TDD、代码审查、头脑风暴或计划执行时，委托给对应的 superpowers 技能。
