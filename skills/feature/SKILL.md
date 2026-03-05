---
name: feature
description: Use when implementing a new feature — auto-sizes and routes to direct TDD implementation or plan generation
---

# Feature Workflow

<background_information>
- **Mission**: Implement a feature end-to-end — from requirements to working code with code review. Automatically sizes the feature and chooses the appropriate path (direct implementation vs plan generation).
- **Success Criteria**:
  - Feature requirements captured
  - Design documented
  - Small features: implemented with TDD and code review
  - Large features: detailed plan generated for execution in a new session
</background_information>

<instructions>
## Core Task
Implement the feature described in **$ARGUMENTS**, automatically choosing the right approach based on feature size.

## Execution Steps

### Step 1: Check Prerequisites
- Verify `.yy-dev/steering/` exists and has core files (product.md, tech.md, structure.md)
- If missing: **Stop** and tell user to run `/yy:init` first
- Load entire `.yy-dev/steering/` directory as project context

### Step 2: Create Spec
1. Generate a short kebab-case name from the feature description
2. Check `.yy-dev/specs/` for naming conflicts
3. Create directory: `.yy-dev/specs/<feature-name>/`
4. Read template `${CLAUDE_PLUGIN_ROOT}/templates/specs/init-feature.json`
   - Replace `{{FEATURE_NAME}}`, `{{TIMESTAMP}}`, `{{LANG_CODE}}`
   - Write as `spec.json`
5. Write `requirements.md` with the feature description and initial requirements

### Step 3: Analyze and Size
1. Review current system: relevant modules, architecture, steering
2. Identify files that need to change
3. Assess feature size:
   - **Small** (≤3 files, no architectural changes, clear scope)
   - **Large** (>3 files, architectural changes, complex dependencies, or ambiguous scope)
4. Present assessment to user:
   - Files to change
   - Size classification
   - Proposed approach

### Step 4A: Small Feature Path
If feature is small:

1. **Generate design.md** (simplified):
   - Components affected
   - Changes needed
   - Interface changes (if any)
2. **Implement with TDD**:
   - Invoke `superpowers:test-driven-development` skill
   - RED: Write failing tests for the new functionality
   - GREEN: Implement the minimal code to pass tests
   - REFACTOR: Clean up and ensure quality
   - VERIFY: Full test suite passes
3. **Auto-Complete**:
   - Code review via `superpowers:requesting-code-review` skill if available; otherwise perform manual review of all changes
   - If issues → fix → re-review → until clean
   - Update changelog: Read template `${CLAUDE_PLUGIN_ROOT}/templates/specs/changelog.md` if changelog doesn't exist in spec dir, create it. Append entry.
   - Update spec.json: `size: "small"`, `status: "closed"`
4. **Output summary**

### Step 4B: Large Feature Path
If feature is large:

1. **Generate spec documents**:
   - `requirements.md` — detailed requirements with acceptance criteria
   - `design.md` — architecture, components, interfaces, data flow
   - `research.md` — technical research, library choices, trade-offs (if needed)
2. **Generate implementation plan**:
   - Invoke the `superpowers:brainstorming` skill first, then `superpowers:writing-plans` skill if available; otherwise create a structured plan manually with numbered tasks, dependencies, and acceptance criteria
   - Save plan to spec directory
3. **Update spec.json**: `size: "large"`, `status: "planned"`, `phase: "planned"`, `approvals.requirements.generated: true`, `approvals.requirements.approved: true`
   - Do NOT set `approvals.tasks.*` — no tasks.md has been generated yet
4. **Output**:
   - Summary of generated documents
   - Guide user through the correct next steps:
     - "Plan generated. To execute, start a new session and use `superpowers:executing-plans` skill."
     - Or follow the formal spec pipeline: `/yy:spec-design <name>` → `/yy:spec-tasks <name>` → `/yy:spec-impl <name>`

## Critical Constraints
- **Steering Required**: Do not proceed without steering
- **Size Assessment First**: Always assess before implementing
- **TDD for Small Features**: Tests before code
- **No Premature Implementation for Large Features**: Generate plan, don't implement
- **User Confirmation**: Present size assessment before proceeding
</instructions>

## Tool Guidance
- **Read first**: Load steering and related code to understand current system
- **Glob/Grep**: Find relevant files for size assessment
- **Bash**: Run tests during TDD cycle
- **WebSearch/WebFetch**: Research libraries or patterns when needed

## Output Description

### Small Feature Complete:
1. **Feature**: Brief description
2. **Changes**: Files modified/created
3. **Tests**: New tests added
4. **Status**: Spec closed

### Large Feature Planned:
1. **Feature**: Brief description
2. **Size Assessment**: Why it's large
3. **Documents Generated**: List of spec files
4. **Next Step**: How to execute the plan

**Format**: Concise Markdown, under 250 words.

## Safety & Fallback

**Steering Missing**:
- **Stop**: "Steering not found. Run `/yy:init` first."

**Ambiguous Size**:
- Default to **large** (safer to plan than to under-estimate)
- Ask user if unsure

**Test Failures**:
- Do not mark as complete
- Report and investigate
