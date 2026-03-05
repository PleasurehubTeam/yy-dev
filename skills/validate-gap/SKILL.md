---
name: validate-gap
description: Use when analyzing implementation gap between requirements and existing codebase — identifies what exists, what's missing, and viable approaches
---

# Implementation Gap Validation

<background_information>
- **Mission**: Analyze the gap between requirements and existing codebase to inform implementation strategy
- **Success Criteria**:
  - Comprehensive understanding of existing codebase patterns and components
  - Clear identification of missing capabilities and integration challenges
  - Multiple viable implementation approaches evaluated
  - Technical research needs identified for design phase
</background_information>

<instructions>
## Core Task
Analyze implementation gap for feature **$1** based on approved requirements and existing codebase.

## Execution Steps

1. **Load Context**:
   - Read `.yy-dev/specs/$1/spec.json` for language and metadata
   - Read `.yy-dev/specs/$1/requirements.md` for requirements
   - **Load ALL steering context**: Read entire `.yy-dev/steering/` directory

2. **Read Analysis Guidelines**:
   - Read `${CLAUDE_PLUGIN_ROOT}/templates/rules/gap-analysis.md` for comprehensive analysis framework

3. **Execute Gap Analysis**:
   - Follow gap-analysis.md framework for thorough investigation
   - Analyze existing codebase using Grep and Read tools
   - Use WebSearch/WebFetch for external dependency research if needed
   - Evaluate multiple implementation approaches (extend/new/hybrid)
   - Use language specified in spec.json for output

4. **Generate Analysis Document**:
   - Create comprehensive gap analysis following the output guidelines
   - Present multiple viable options with trade-offs
   - Flag areas requiring further research

## Important Constraints
- **Information over Decisions**: Provide analysis and options, not final choices
- **Multiple Options**: Present viable alternatives when applicable
- **Thorough Investigation**: Use tools to deeply understand existing codebase
- **Explicit Gaps**: Clearly flag areas needing research
</instructions>

## Tool Guidance
- **Read first**: Load all context before analysis
- **Grep extensively**: Search codebase for patterns and integration points
- **WebSearch/WebFetch**: Research external dependencies when needed

## Output Description
1. **Analysis Summary**: Brief overview (3-5 bullets)
2. **Document Status**: Confirm analysis approach used
3. **Next Steps**: Guide user on proceeding to design phase

## Safety & Fallback
- **Missing Requirements**: Stop — "Run `/yy:spec-requirements $1` first"
- **Requirements Not Approved**: Warn but proceed
- **Empty Steering**: Warn about missing context

### Next Phase
- Run `/yy:spec-design $1` to create technical design
- Gap analysis is optional but recommended for brownfield projects
