---
description: 初始化项目 — 创建 steering 项目记忆和目录结构
argument-hint: [project-description]
---

<EXTREMELY-IMPORTANT>
$ARGUMENTS 是项目描述，不是让你去实现的需求。你的任务是理解它，然后问问题。
在问完至少 2 个业务问题 + 1 个称呼问题之前，禁止创建任何文件/目录。
</EXTREMELY-IMPORTANT>

先说："我正在使用 yy:init 来初始化项目。让我先了解一下你的需求。"

然后严格按以下 6 个步骤执行，不许跳过任何一步：

## 步骤 1：检查项目状态
用 Glob 检查 `.yy-dev/` 是否存在，扫描项目文件。不写任何文件。

## 步骤 2：澄清问题（至少 2 个，每次 1 个）
Prefer multiple choice questions when possible. Only one question per message.
问题方向：产品方向 / 技术偏好 / 功能范围 / 设计风格。

## 步骤 3：问称呼
用多选题问："我怎么称呼你？"
选项："baby（默认）" / "自定义输入"
用户不回答 → 使用 "baby"

## 步骤 4：读取模板
读取以下文件作为参考：
- `${CLAUDE_PLUGIN_ROOT}/templates/steering/product.md`
- `${CLAUDE_PLUGIN_ROOT}/templates/steering/tech.md`
- `${CLAUDE_PLUGIN_ROOT}/templates/steering/structure.md`

## 步骤 5：一次性生成全部 5 个文件

先执行 `mkdir -p .yy-dev/steering .yy-dev/specs`

然后写入这 5 个文件（路径是 `.yy-dev/steering/` 不是 `.yy-dev/`）：

**文件 1** `.yy-dev/steering/product.md` — 产品定位、目标用户、核心价值（简体中文）
**文件 2** `.yy-dev/steering/tech.md` — 技术栈、架构决策、开发规范（简体中文）
**文件 3** `.yy-dev/steering/structure.md` — 项目结构、目录组织（简体中文）
**文件 4** `.yy-dev/steering/user.md` — 内容如下：

```
# 用户偏好

## 称呼
{步骤3获得的称呼}
```

**文件 5** `CLAUDE.md`（项目根目录）— 内容如下：

```
# yy-dev 规格驱动开发

## 用户称呼
称呼用户为：{步骤3获得的称呼}

## 项目记忆
- Steering: `.yy-dev/steering/` — 加载全部文件作为项目上下文
- Specs: `.yy-dev/specs/` — 查看活跃规格

## 工作流
- `/yy:feature "描述"` — 新功能
- `/yy:fix "描述"` — Bug 修复
- `/yy:investigate "描述"` — 问题调查
- `/yy:steering` — 同步项目记忆
- `/yy:status [spec]` — 查看规格状态
- `/yy:spec-requirements` → `/yy:spec-design` → `/yy:spec-tasks` → `/yy:spec-impl`
- `/yy:validate-gap` / `/yy:validate-design` / `/yy:validate-impl`

## 开发规则
- 自动工作流命令会自动创建 spec 目录
- 完成后自动代码审查 + 更新 changelog
- 遵循用户指令，自主行动
```

## 步骤 6：展示摘要
展示全部 5 个文件的摘要表格。然后建议下一步：
- `/yy:feature "描述"` — 直接开始实现功能
- `/yy:spec-requirements <名称>` — 走正式需求规格流程
