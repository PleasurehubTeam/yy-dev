---
name: init
description: Use when initializing a new project with yy-dev — creates .yy-dev/ directory and steering files
---

<EXTREMELY-IMPORTANT>
## 你必须生成的 5 个文件（缺一个 = 失败）

1. `.yy-dev/steering/product.md`
2. `.yy-dev/steering/tech.md`
3. `.yy-dev/steering/structure.md`
4. `.yy-dev/steering/user.md` — 用户称呼
5. `CLAUDE.md` — 项目根目录

路径是 `.yy-dev/steering/` 不是 `.yy-dev/`。

## 你必须问的问题（在写任何文件之前）

- 至少 2 个业务澄清问题（多选题，一次一个）
- 1 个称呼问题："我怎么称呼你？" 选项：baby（默认）/ 自定义

问完这些才能写文件。之前不许创建任何文件/目录。
</EXTREMELY-IMPORTANT>

**Announce:** "我正在使用 yy:init 技能来初始化项目。让我先了解一下你的需求。"

## Checklist（创建 task 逐项完成）

1. **检查项目状态** — Glob 检查 `.yy-dev/` 和项目文件
2. **澄清问题 1** — 多选题，等回答
3. **澄清问题 2** — 多选题，等回答
4. **问称呼** — 多选题："我怎么称呼你？" 选项 baby（默认）/ 自定义
5. **生成 5 个文件** — 见下方详细说明
6. **展示摘要 + 建议下一步**

## 澄清问题方向

Prefer multiple choice questions when possible. Only one question per message.

- 产品方向 / 技术偏好 / 功能范围 / 设计风格 / 集成需求

## 文件生成详细说明

先创建目录：`mkdir -p .yy-dev/steering .yy-dev/specs`

先读取模板：
- `${CLAUDE_PLUGIN_ROOT}/templates/steering/product.md`
- `${CLAUDE_PLUGIN_ROOT}/templates/steering/tech.md`
- `${CLAUDE_PLUGIN_ROOT}/templates/steering/structure.md`

### 文件 1: `.yy-dev/steering/product.md`
产品定位、目标用户、核心价值。简体中文。

### 文件 2: `.yy-dev/steering/tech.md`
技术栈、架构决策、开发规范。简体中文。

### 文件 3: `.yy-dev/steering/structure.md`
项目结构、目录组织、命名约定。简体中文。

### 文件 4: `.yy-dev/steering/user.md`

```markdown
# 用户偏好

## 称呼
{nickname}
```

### 文件 5: `CLAUDE.md`（项目根目录，已存在则追加）

```markdown
# yy-dev 规格驱动开发

## 用户称呼
称呼用户为：{nickname}

## 项目记忆
- Steering: `.yy-dev/steering/` — 加载全部文件作为项目上下文
- Specs: `.yy-dev/specs/` — 查看活跃规格

## 工作流

### 自动工作流（端到端）
- `/yy:feature "描述"` — 新功能
- `/yy:fix "描述"` — Bug 修复
- `/yy:investigate "描述"` — 问题调查
- `/yy:steering` — 同步项目记忆
- `/yy:status [spec]` — 查看规格状态

### 正式流水线（逐步控制）
- `/yy:spec-requirements` → `/yy:spec-design` → `/yy:spec-tasks` → `/yy:spec-impl`
- `/yy:validate-gap` / `/yy:validate-design` / `/yy:validate-impl`

## 开发规则
- 自动工作流命令会自动创建 spec 目录
- 完成后自动代码审查 + 更新 changelog
- 遵循用户指令，自主行动
```

## 建议下一步（只建议真实存在的命令）

- `/yy:feature "描述"` — 直接开始实现功能
- `/yy:spec-requirements <名称>` — 走正式需求规格流程
- `/yy:fix "描述"` — 修复 bug
