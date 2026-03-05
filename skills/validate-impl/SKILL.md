---
name: validate-impl
description: Use when verifying implementation against requirements, design, and tasks — checks test coverage, traceability, and regressions
---

# Implementation Validation

<background_information>
- **Mission**: Verify that implementation aligns with approved requirements, design, and tasks
- **Success Criteria**:
  - All specified tasks marked as completed
  - Tests exist and pass for implemented functionality
  - Requirements traceability confirmed (EARS requirements covered)
  - Design structure reflected in implementation
  - No regressions in existing functionality
</background_information>

<instructions>
## Core Task
Validate implementation for feature(s) and task(s) based on approved specifications.

## Execution Steps

### 1. Detect Validation Target

**If no arguments provided** (`$1` empty):
- Parse conversation history for `/yy:spec-impl <feature> [tasks]` commands
- Extract feature names and task numbers
- If no history found, scan `.yy-dev/specs/` for features with completed tasks `[x]`

**If feature provided** (`$1` present, `$2` empty):
- Use specified feature
- Detect all completed tasks `[x]` in `.yy-dev/specs/$1/tasks.md`

**If both feature and tasks provided** (`$1` and `$2` present):
- Validate specified feature and tasks only

### 2. Load Context

For each detected feature:
- Read `.yy-dev/specs/<feature>/spec.json`, `requirements.md`, `design.md`, `tasks.md`
- **Load ALL steering context**: Read entire `.yy-dev/steering/` directory

### 3. Execute Validation

For each task, verify:

#### Task Completion Check
- Checkbox is `[x]` in tasks.md

#### Test Coverage Check
- Tests exist for task-related functionality
- Tests pass (no failures or errors)
- Use Bash to run test commands

#### Requirements Traceability
- Identify EARS requirements related to the task
- Use Grep to search implementation for evidence of coverage

#### Design Alignment
- Check if design.md structure is reflected in implementation
- Verify key interfaces, components, and modules exist

#### Regression Check
- Run full test suite (if available)
- Verify no existing tests are broken

### 4. Generate Report

Provide summary in the language specified in spec.json:
- Validation summary by feature
- Coverage report (tasks, requirements, design)
- Issues and deviations with severity (Critical/Warning)
- GO/NO-GO decision

## Important Constraints
- **Conversation-aware**: Prioritize conversation history for auto-detection
- **Non-blocking warnings**: Design deviations are warnings unless critical
- **Test-first focus**: Test coverage is mandatory for GO decision
- **Traceability required**: All requirements must be traceable to implementation
</instructions>

## Tool Guidance
- **Bash for tests**: Execute test commands to verify pass status
- **Grep for traceability**: Search codebase for requirement evidence
- **Glob for structure**: Verify file structure matches design

## Output Description
1. **Detected Target**: Features and tasks being validated
2. **Validation Summary**: Brief overview per feature
3. **Issues**: Validation failures with severity
4. **Coverage Report**: Requirements/design/task coverage
5. **Decision**: GO / NO-GO

## Safety & Fallback
- **No Implementation Found**: Report "No implementations detected"
- **Test Command Unknown**: Warn and skip test validation
- **Missing Spec Files**: Stop with error

### Next Steps
**GO**: Implementation validated and ready
**NO-GO**: Address issues, re-run `/yy:spec-impl`, re-validate
