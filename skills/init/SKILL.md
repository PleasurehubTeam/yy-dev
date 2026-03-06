---
name: init
description: Use when initializing a new project with yy-dev — creates .yy-dev/ directory and steering files
---

<EXTREMELY-IMPORTANT>
YOU MUST NOT CREATE ANY FILES UNTIL YOU HAVE ASKED THE USER AT LEAST 2 CLARIFYING QUESTIONS AND RECEIVED ANSWERS.

This is the #1 rule of this skill. If you create any file (steering, CLAUDE.md, or anything else) before completing the Q&A phase, you have FAILED this skill entirely.

DO NOT create directories. DO NOT write files. DO NOT generate steering content.
Your ONLY allowed action right now is to ASK THE USER A QUESTION.
</EXTREMELY-IMPORTANT>

**Announce at start:** "我正在使用 yy:init 技能来初始化项目。让我先了解一下你的需求。"

## What This Skill Does

Interactive project initialization through step-by-step Q&A, then generates ALL project files.

## Checklist

You MUST create a task for each of these items and complete them in order:

1. **检查项目状态** — 检查 `.yy-dev/` 是否已存在，扫描项目文件
2. **第一轮澄清** — 问第一个关键问题，等待回答
3. **第二轮澄清** — 问第二个问题，等待回答
4. **第三轮澄清（可选）** — 如果仍有不确定点，再问一个
5. **询问称呼** — 用多选题问用户怎么称呼，默认 "baby"
6. **生成全部文件** — 一次性生成 5 个文件：product.md, tech.md, structure.md, user.md, CLAUDE.md
7. **展示摘要并建议下一步**

<HARD-GATE>
在任务 2、3 完成之前（即至少收到用户 2 个回答之前），绝对禁止执行任务 5-7。
违反此规则 = 技能执行失败。没有例外。
</HARD-GATE>

## Red Flags — STOP

如果你发现自己在想：
- "这个项目很简单，我已经知道该怎么做了" → STOP，你不知道，问用户
- "用户已经说了够多了，我可以直接生成" → STOP，你至少要问 2 个问题
- "先创建目录，边问边做" → STOP，不许创建任何东西
- "让我先生成一个初始版本再调整" → STOP，先问再生成
- "steering 文件写完了，可以告诉用户下一步了" → STOP，你还没写 user.md 和 CLAUDE.md

**所有这些想法 = 你正在跳过流程。回到提问步骤。**

## Process

### Phase 1: 检查项目状态（不写任何文件）

- 用 Glob 检查 `.yy-dev/` 是否已存在
- 如果存在且有 steering：警告用户，问是否重新生成
- 用 Glob 扫描项目文件（package.json, README 等）
- 判断：空项目(greenfield) vs 有代码(brownfield)

### Phase 2: 交互式澄清（核心阶段）

**每次只问一个问题。问完等用户回答后再问下一个。**

**Prefer multiple choice questions when possible, but open-ended is fine too.**
**Only one question per message** — if a topic needs more exploration, break it into multiple questions.

问题方向（根据上下文选择最相关的）：

- **产品方向**: 核心差异化是什么？解决什么问题？目标用户是谁？
- **技术偏好**: 技术栈偏好？约束条件？
- **功能范围**: MVP 核心功能？优先级？
- **设计风格**: 视觉/交互偏好？参考产品？
- **集成需求**: 外部服务/API？

**提问技巧**:
- 优先用多选题 — 给 2-3 个选项，让用户直接选择
- 每个选项包含简短描述，帮助用户理解选择的含义
- 结合用户的描述追问，不要问泛泛的问题
- 体现你对领域的理解，给出专业建议

**最少 2 个问题，最多 3 个。**

**最后一个澄清问题之后，紧接着问称呼问题（同一轮或下一轮）：**

> 用多选题问："我怎么称呼你？"
> 选项："baby（默认）"、"自定义输入"
> 用户不回答或选默认 → 使用 "baby"

### Phase 3: 生成全部文件（仅在 Phase 2 完成后，包括称呼问题）

你必须在这个阶段一次性生成以下 **5 个文件**，缺一不可：

1. 创建目录：
```bash
mkdir -p .yy-dev/steering .yy-dev/specs
```

2. 读取模板和原则：
   - `${CLAUDE_PLUGIN_ROOT}/templates/steering/product.md`
   - `${CLAUDE_PLUGIN_ROOT}/templates/steering/tech.md`
   - `${CLAUDE_PLUGIN_ROOT}/templates/steering/structure.md`
   - `${CLAUDE_PLUGIN_ROOT}/templates/rules/steering-principles.md`

3. **文件 1/5** — `.yy-dev/steering/product.md` — 产品定位、目标用户、核心价值
4. **文件 2/5** — `.yy-dev/steering/tech.md` — 技术栈、架构决策、开发规范
5. **文件 3/5** — `.yy-dev/steering/structure.md` — 项目结构、目录组织、命名约定
6. **文件 4/5** — `.yy-dev/steering/user.md` — 用户偏好（称呼）：

```markdown
# 用户偏好

## 称呼
{nickname}
```

7. **文件 5/5** — 项目根目录 `CLAUDE.md`（已存在则追加，用 `---` 分隔）：

```markdown
# yy-dev 规格驱动开发

## 用户称呼
称呼用户为：{nickname}

## 项目记忆
- Steering: `.yy-dev/steering/` — 加载全部文件作为项目上下文
- Specs: `.yy-dev/specs/` — 查看活跃规格

## 工作流

### 自动工作流（端到端）
- `/yy:feature "描述"` — 新功能（自动评估规模 → TDD 实现或生成计划）
- `/yy:fix "描述"` — Bug 修复（TDD + 代码审查）
- `/yy:investigate "描述"` — 问题调查（系统化诊断）
- `/yy:steering` — 同步项目记忆
- `/yy:status [spec]` — 查看规格状态

### 正式流水线（逐步控制）
- `/yy:spec-requirements <名称>` → `/yy:spec-design` → `/yy:spec-tasks` → `/yy:spec-impl`
- `/yy:validate-gap` / `/yy:validate-design` / `/yy:validate-impl`

## 开发规则
- 自动工作流命令（feature/fix/investigate）会自动创建 spec 目录
- 正式流水线需要已有 spec
- 完成后自动代码审查 + 更新 changelog
- 遵循用户指令，自主行动，仅在缺少关键信息时提问
```

**重要约束：**
- 所有内容必须是简体中文
- 文件名必须是 product.md、tech.md、structure.md、user.md — 不是其他名字
- `{nickname}` 必须替换为 Phase 2 中获得的实际称呼
- 必须生成全部 5 个文件才算完成此阶段

### Phase 4: 展示摘要 + 建议下一步

展示所有 5 个文件的摘要表格，然后建议下一步。

**只建议以下真实存在的命令：**
- `/yy:feature "描述"` — 直接开始实现功能
- `/yy:spec-requirements <名称>` — 走正式需求规格流程
- `/yy:fix "描述"` — 修复 bug

**绝对不要建议不存在的命令**（如 `/yy:brainstorming` 不存在）。
