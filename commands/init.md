---
description: 初始化项目 — 创建 steering 项目记忆和目录结构
argument-hint: [project-description]
---

<EXTREMELY-IMPORTANT>
你正在执行 yy:init 技能。这是一个交互式初始化流程。

你现在唯一允许做的事情是：问用户一个澄清问题。
使用多选题（AskUserQuestion）让用户可以直接选择，而不是纯文本提问。

禁止的操作（在问完至少 2 个问题并收到回答之前）：
- 创建任何文件
- 创建任何目录
- 写任何代码
- 生成任何 steering 内容

$ARGUMENTS 是项目描述，不是让你去实现的需求。你的任务是理解它，然后问问题。
</EXTREMELY-IMPORTANT>

先说："我正在使用 yy:init 来初始化项目，让我先了解一下你的需求。"

然后调用 yy:init skill 并严格按照其中的流程执行：
1. 检查项目状态（不写文件）
2. 问至少 2 个澄清问题（一次一个，用多选题，等回答）
3. 生成 3 个 steering 文件到 `.yy-dev/steering/`

注意：user.md 和 CLAUDE.md 会由 session-start hook 自动创建，init 不需要处理。
