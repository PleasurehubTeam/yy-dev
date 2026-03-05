---
name: spec-tasks
description: Use when generating implementation tasks from approved requirements and design
---

# Implementation Tasks Generator

<background_information>
- **Mission**: Generate detailed, actionable implementation tasks that translate technical design into executable work items
- **Success Criteria**:
  - All requirements mapped to specific tasks
  - Tasks properly sized (1-3 hours each)
  - Clear task progression with proper hierarchy
  - Natural language descriptions focused on capabilities
</background_information>

<instructions>
## Core Task
Generate implementation tasks for feature **$1** based on approved requirements and design.

## Execution Steps

### Step 1: Load Context

**Read all necessary context**:
- `.yy-dev/specs/$1/spec.json`, `requirements.md`, `design.md`
- `.yy-dev/specs/$1/tasks.md` (if exists, for merge mode)
- **Entire `.yy-dev/steering/` directory** for complete project memory

**Validate approvals**:
- If `-y` flag provided ($2 == "-y"): Auto-approve requirements and design in spec.json
- Otherwise: Verify both approved (stop if not, see Safety & Fallback)
- Determine sequential mode based on presence of `--sequential`

### Step 2: Generate Implementation Tasks

**Load generation rules and template**:
- Read `${CLAUDE_PLUGIN_ROOT}/templates/rules/tasks-generation.md` for principles
- If `sequential` is **false**: Read `${CLAUDE_PLUGIN_ROOT}/templates/rules/tasks-parallel-analysis.md` for parallel judgement criteria
- Read `${CLAUDE_PLUGIN_ROOT}/templates/specs/tasks.md` for format (supports `(P)` markers)

**Generate task list following all rules**:
- Use language specified in spec.json
- Map all requirements to tasks
- When documenting requirement coverage, list numeric requirement IDs only (comma-separated)
- Ensure all design components included
- Verify task progression is logical and incremental
- Apply `(P)` markers to tasks that satisfy parallel criteria (omit in sequential mode)
- If existing tasks.md found, merge with new content

### Step 3: Finalize

**Write and update**:
- Create/update `.yy-dev/specs/$1/tasks.md`
- Update spec.json metadata:
  - Set `phase: "tasks-generated"`
  - Set `approvals.tasks.generated: true, approved: false`
  - Set `approvals.requirements.approved: true`
  - Set `approvals.design.approved: true`
  - Update `updated_at` timestamp

## Critical Constraints
- **Follow rules strictly**: All principles in tasks-generation.md are mandatory
- **Natural Language**: Describe what to do, not code structure details
- **Complete Coverage**: ALL requirements must map to tasks
- **Maximum 2 Levels**: Major tasks and sub-tasks only (no deeper nesting)
- **Sequential Numbering**: Major tasks increment (1, 2, 3...), never repeat
- **Task Integration**: Every task must connect to the system (no orphaned work)
</instructions>

## Tool Guidance
- **Read first**: Load all context, rules, and templates before generation
- **Write last**: Generate tasks.md only after complete analysis

## Output Description
1. **Status**: Confirm tasks generated
2. **Task Summary**: Total major tasks, sub-tasks, requirements covered
3. **Quality Validation**: Requirements mapped, dependencies verified, testing included
4. **Next Action**: Review tasks and proceed when ready

**Format**: Concise (under 200 words)

## Safety & Fallback

**Requirements or Design Not Approved**:
- **Stop**: "Run `/yy:spec-tasks $1 -y` to auto-approve both and proceed"

**Missing Requirements or Design**:
- **Stop**: "Complete requirements and design phases first"

### Next Phase: Implementation

**Before Starting Implementation**:
- Clear conversation history and free up context before running `/yy:spec-impl`

**If Tasks Approved**:
- Execute specific task: `/yy:spec-impl $1 1.1`
- Execute multiple tasks: `/yy:spec-impl $1 1.1,1.2`

**If Modifications Needed**:
- Re-run `/yy:spec-tasks $1` (existing tasks used as reference)
