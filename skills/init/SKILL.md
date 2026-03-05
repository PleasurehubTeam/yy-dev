---
name: init
description: Use when initializing a new project with yy-dev — creates .yy-dev/ directory and steering files
---

# 项目初始化

<background_information>
**Mission**: Initialize a project for spec-driven development by creating `.yy-dev/` directory structure and generating steering files.

**Success Criteria**:
- `.yy-dev/` directory created with proper structure
- Steering files (product.md, tech.md, structure.md) generated from project analysis
- User can immediately start using `/yy:feature`, `/yy:fix`, etc.
</background_information>

<instructions>
## Core Task
Initialize yy-dev for the current project based on **$ARGUMENTS** (project description).

**All generated steering content MUST be in Simplified Chinese (简体中文).**

## Execution Steps

### Step 1: Check Prerequisites
- Check if `.yy-dev/` already exists
- If exists with steering: Warn user and ask if they want to regenerate
- If exists without steering: Continue with steering generation

### Step 2: Create Directory Structure
```
.yy-dev/
├── steering/
└── specs/
```

### Step 3: Interactive Clarification (MANDATORY)

**DO NOT skip this step. DO NOT generate steering directly from the description alone.**

Before generating any steering files, you MUST ask clarifying questions ONE AT A TIME:

1. **First question**: Based on the user's description, ask about the most important unclear aspect (e.g., target users, core differentiator, tech preferences)
2. **Wait for answer**, then ask the next question if needed
3. **Maximum 3 questions** — stop if you have enough context

Example flow:
- User: "搞一个 web 版本的计算器，要有创意的"
- Q1: "你希望这个计算器的「创意」体现在哪方面？比如：视觉设计（3D/动画）、交互方式（手势/语音）、功能（科学计算/单位换算/图形化），还是其他？"
- User answers...
- Q2: "技术栈有偏好吗？纯 HTML/CSS/JS，还是用 React/Vue 等框架？"
- User answers...
- Proceed to Step 4

### Step 4: Scan Codebase (if not empty)
- `Glob` for source files and config
- `Read` README, package.json, pyproject.toml, etc.
- `Grep` for framework patterns
- Skip this step for empty/greenfield projects

### Step 5: Generate Steering

1. Read steering templates from `${CLAUDE_PLUGIN_ROOT}/templates/steering/`
2. Read steering principles from `${CLAUDE_PLUGIN_ROOT}/templates/rules/steering-principles.md`
3. Generate three steering files **entirely in Simplified Chinese**:
   - `product.md`: 产品定位、目标用户、核心价值
   - `tech.md`: 技术栈、开发规范、约束条件
   - `structure.md`: 项目结构、目录组织、命名约定
4. Present summary for user review

### Step 6: Offer Next Steps

Present ONLY these valid commands:
- `/yy:feature "描述"` — 直接开始实现功能
- `/yy:spec-requirements <名称>` — 走正式需求规格流程

**DO NOT suggest commands that don't exist** (e.g., `/yy:brainstorming` does NOT exist).

## Critical Constraints
- **Interactive**: Ask clarifying questions BEFORE generating, one at a time, max 3 questions
- **Language**: All steering content in Simplified Chinese (简体中文)
- **Pattern-focused**: Document patterns, not exhaustive lists (follow steering principles)
- **Security**: Never include secrets, keys, or credentials in steering
- **Preserve existing**: If regenerating, preserve user customizations
- **Valid commands only**: Only suggest `/yy:*` commands that actually exist
</instructions>

## Tool Guidance
- **Glob**: Find source files, configs, package files
- **Read**: Examine README, package.json, steering templates
- **Grep**: Search for framework patterns, import conventions
- **Write**: Create steering files

## Output Description
```
✅ 项目已初始化

## Steering 已创建：
- product.md: [简述]
- tech.md: [技术栈概要]
- structure.md: [项目结构]

## 下一步：
- /yy:feature "描述" — 实现一个功能
- /yy:fix "描述" — 修复一个 bug
- /yy:spec-requirements <名称> — 正式需求规格流程
```
