---
name: init
description: Use when initializing a new project with yy-dev — creates .yy-dev/ directory and steering files
---

# Project Initialization

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

## Execution Steps

### Step 1: Check Prerequisites
- Check if `.yy-dev/` already exists
- If exists with steering: Warn user and ask if they want to regenerate
- If exists without steering: Continue with steering generation

### Step 2: Create Directory Structure
```
.yy-dev/
├── steering/
├── specs/
└── config/
```

### Step 3: Generate Steering

**With Input** ($ARGUMENTS provided):
1. Analyze the project description
2. Ask ONE clarifying question at a time (interactive, not a batch questionnaire)
3. Scan codebase for existing patterns:
   - `Glob` for source files and config
   - `Read` README, package.json, pyproject.toml, etc.
   - `Grep` for framework patterns
4. Read steering templates from `${CLAUDE_PLUGIN_ROOT}/templates/steering/`
5. Read steering principles from `${CLAUDE_PLUGIN_ROOT}/templates/rules/steering-principles.md`
6. Generate three steering files:
   - `product.md`: Purpose, capabilities, value proposition
   - `tech.md`: Stack, standards, conventions
   - `structure.md`: Organization, naming, imports
7. Present summary for user review

**Without Input** (brownfield):
1. Scan codebase comprehensively:
   - README, configs, source files
   - Framework detection, build tools
   - Directory patterns, naming conventions
2. Infer steering from code analysis
3. Present inferred steering for user confirmation
4. Allow corrections before writing files

### Step 4: Offer Next Steps
- Ask: "Would you like to start with a feature (`/yy:feature`) or set up formal requirements (`/yy:spec-requirements`)?"

## Critical Constraints
- **Interactive**: One question at a time, not batch questionnaires
- **Pattern-focused**: Document patterns, not exhaustive lists (follow steering principles)
- **Security**: Never include secrets, keys, or credentials in steering
- **Preserve existing**: If regenerating, preserve user customizations
</instructions>

## Tool Guidance
- **Glob**: Find source files, configs, package files
- **Read**: Examine README, package.json, steering templates
- **Grep**: Search for framework patterns, import conventions
- **Write**: Create steering files

## Output Description
```
✅ Project Initialized

## Steering Created:
- product.md: [Brief description]
- tech.md: [Key stack summary]
- structure.md: [Organization pattern]

## Next Steps:
- /yy:feature "description" — implement a feature
- /yy:fix "description" — fix a bug
- /yy:spec-requirements <name> — formal spec pipeline
```
