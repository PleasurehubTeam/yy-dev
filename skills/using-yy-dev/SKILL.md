---
name: using-yy-dev
description: Use when starting any conversation in a project with yy-dev — introduces available workflows and guides skill selection
---

# yy-dev: Spec-Driven Development Workflow

yy-dev provides structured development workflows with project memory (steering) and spec-driven processes.

## Available Workflows

### Daily Work
| Command | When to Use |
|---------|------------|
| `/yy:init` | First time setup — create project steering (product, tech, structure) |
| `/yy:feature "desc"` | Implement a feature — auto-sizes and routes to direct TDD or plan generation |
| `/yy:fix "desc"` | Fix a bug — TDD fix with auto code review |
| `/yy:investigate "desc"` | Diagnose an issue — 4-phase systematic debugging |
| `/yy:steering` | Bootstrap or sync project steering |
| `/yy:status [name]` | View spec status and progress |

### Formal Spec Pipeline (large features / new projects)
| Command | When to Use |
|---------|------------|
| `/yy:spec-requirements <name>` | Generate EARS-format requirements |
| `/yy:spec-design <name> [-y]` | Create technical design with discovery research |
| `/yy:spec-tasks <name> [-y]` | Generate implementation tasks |
| `/yy:spec-impl <name> [tasks]` | TDD implementation of tasks |

### Validation
| Command | When to Use |
|---------|------------|
| `/yy:validate-gap <name>` | Analyze gap between requirements and existing code |
| `/yy:validate-design <name>` | Interactive design quality review (GO/NO-GO) |
| `/yy:validate-impl <name>` | Verify implementation matches specs |

## How It Works

1. **Steering** (`.yy-dev/steering/`) = persistent project memory (product, tech, structure)
2. **Specs** (`.yy-dev/specs/`) = decision records and feature documentation
3. **Workflows** delegate to superpowers skills for execution (TDD, code review, brainstorming, plans)

## Skill Selection Guide

- User says "add X" / "implement Y" / "build Z" → invoke `yy:feature`
- User says "fix" / "bug" / "broken" / "error" → invoke `yy:fix`
- User says "investigate" / "why" / "diagnose" / "debug" → invoke `yy:investigate`
- User mentions "requirements" / "design" / "spec" → invoke the specific spec skill
- User says "status" / "progress" → invoke `yy:status`

## Key Principle

yy-dev orchestrates; superpowers executes. When a workflow needs TDD, code review, brainstorming, or plan execution, it delegates to the corresponding superpowers skill.
