---
name: validate-design
description: Use when reviewing technical design quality — interactive GO/NO-GO assessment with focused critical issues
---

# Technical Design Validation

<background_information>
- **Mission**: Conduct interactive quality review of technical design to ensure readiness for implementation
- **Success Criteria**:
  - Critical issues identified (maximum 3 most important concerns)
  - Balanced assessment with strengths recognized
  - Clear GO/NO-GO decision with rationale
  - Actionable feedback for improvements if needed
</background_information>

<instructions>
## Core Task
Interactive design quality review for feature **$1** based on approved requirements and design document.

## Execution Steps

1. **Load Context**:
   - Read `.yy-dev/specs/$1/spec.json` for language and metadata
   - Read `.yy-dev/specs/$1/requirements.md` for requirements
   - Read `.yy-dev/specs/$1/design.md` for design document
   - **Load ALL steering context**: Read entire `.yy-dev/steering/` directory

2. **Read Review Guidelines**:
   - Read `${CLAUDE_PLUGIN_ROOT}/templates/rules/design-review.md` for review criteria and process

3. **Execute Design Review**:
   - Follow design-review.md process: Analysis → Critical Issues → Strengths → GO/NO-GO
   - Limit to 3 most important concerns
   - Engage interactively with user
   - Use language specified in spec.json (default: Simplified Chinese `zh`)
   - **All review output MUST be written in the specified language**

4. **Provide Decision and Next Steps**:
   - Clear GO/NO-GO decision with rationale
   - Guide user on proceeding based on decision

## Important Constraints
- **Quality assurance, not perfection seeking**: Accept acceptable risk
- **Critical focus only**: Maximum 3 issues, only those significantly impacting success
- **Interactive approach**: Engage in dialogue, not one-way evaluation
- **Balanced assessment**: Recognize both strengths and weaknesses
- **Actionable feedback**: All suggestions must be implementable
</instructions>

## Tool Guidance
- **Read first**: Load all context before review
- **Grep if needed**: Search codebase for pattern validation

## Output Description
1. **Review Summary**: Brief overview (2-3 sentences)
2. **Critical Issues**: Maximum 3, following design-review.md format
3. **Design Strengths**: 1-2 positive aspects
4. **Final Assessment**: GO/NO-GO with rationale and next steps

## Safety & Fallback
- **Missing Design**: Stop — "Run `/yy:spec-design $1` first"
- **Empty Steering**: Warn about missing context

### Next Phase
**GO**: Run `/yy:spec-tasks $1 -y` for task generation
**NO-GO**: Address issues, re-run `/yy:spec-design $1`, then re-validate
