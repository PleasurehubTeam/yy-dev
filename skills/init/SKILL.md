---
name: init
description: Use when initializing a new project with yy-dev — creates .yy-dev/ directory and steering files
---

<EXTREMELY-IMPORTANT>
YOU MUST NOT CREATE ANY FILES UNTIL YOU HAVE ASKED THE USER AT LEAST 2 CLARIFYING QUESTIONS AND RECEIVED ANSWERS.

DO NOT create directories. DO NOT write files. DO NOT generate steering content.
Your ONLY allowed action right now is to ASK THE USER A QUESTION.
</EXTREMELY-IMPORTANT>

**Announce at start:** "我正在使用 yy:init 技能来初始化项目。让我先了解一下你的需求。"

## Checklist

You MUST create a task for each of these items and complete them in order:

1. **检查项目状态** — 检查 `.yy-dev/` 是否已存在，扫描项目文件
2. **第一轮澄清** — 多选题，等回答
3. **第二轮澄清** — 多选题，等回答
4. **生成 steering** — 读取模板，生成 3 个文件到 `.yy-dev/steering/`
5. **展示摘要 + 建议下一步**

## Phase 1: 检查项目状态（不写任何文件）

- 用 Glob 检查 `.yy-dev/` 是否已存在
- 如果存在且有 steering：警告用户，问是否重新生成
- 用 Glob 扫描项目文件
- 判断：空项目(greenfield) vs 有代码(brownfield)

## Phase 2: 交互式澄清

**Prefer multiple choice questions when possible, but open-ended is fine too.**
**Only one question per message.** 每次只问一个问题，等回答后再问下一个。

问题方向：产品方向 / 技术偏好 / 功能范围 / 设计风格 / 集成需求

**最少 2 个问题，最多 3 个。**

## Phase 3: 生成 Steering（仅在 Phase 2 完成后）

1. 执行项目初始化脚本（创建目录 + user.md + CLAUDE.md）：
```bash
sh '${CLAUDE_PLUGIN_ROOT}/hooks/setup-project'
```

2. 读取模板：
   - `${CLAUDE_PLUGIN_ROOT}/templates/steering/product.md`
   - `${CLAUDE_PLUGIN_ROOT}/templates/steering/tech.md`
   - `${CLAUDE_PLUGIN_ROOT}/templates/steering/structure.md`
   - `${CLAUDE_PLUGIN_ROOT}/templates/rules/steering-principles.md`

3. 生成 3 个文件到 **`.yy-dev/steering/`**（不是 `.yy-dev/`）：
   - `.yy-dev/steering/product.md` — 产品定位、目标用户、核心价值
   - `.yy-dev/steering/tech.md` — 技术栈、架构决策、开发规范
   - `.yy-dev/steering/structure.md` — 项目结构、目录组织、命名约定

4. **所有内容必须是简体中文**

## Phase 4: 展示摘要 + 建议下一步

展示 steering 摘要表格。

提示用户：**开启新 session 后，user.md（称呼偏好）和 CLAUDE.md（工作流指引）会自动创建。**

**只建议以下命令：**
- `/yy:feature "描述"` — 直接开始实现功能
- `/yy:spec-requirements <名称>` — 走正式需求规格流程
- `/yy:fix "描述"` — 修复 bug
