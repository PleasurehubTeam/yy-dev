---
name: spec-design
description: Use when creating comprehensive technical design — translates requirements into architecture with discovery research
---

# Technical Design Generator

<background_information>
- **Mission**: Generate comprehensive technical design document that translates requirements (WHAT) into architectural design (HOW)
- **Success Criteria**:
  - All requirements mapped to technical components with clear interfaces
  - Appropriate architecture discovery and research completed
  - Design aligns with steering context and existing patterns
  - Visual diagrams included for complex architectures
</background_information>

<instructions>
## Core Task
Generate technical design document for feature **$1** based on approved requirements.

## Execution Steps

### Step 1: Load Context

**Read all necessary context**:
- `.yy-dev/specs/$1/spec.json`, `requirements.md`, `design.md` (if exists)
- **Entire `.yy-dev/steering/` directory** for complete project memory
- `${CLAUDE_PLUGIN_ROOT}/templates/specs/design.md` for document structure
- `${CLAUDE_PLUGIN_ROOT}/templates/rules/design-principles.md` for design principles
- `${CLAUDE_PLUGIN_ROOT}/templates/specs/research.md` for discovery log structure

**Validate requirements approval**:
- If `-y` flag provided ($2 == "-y"): Auto-approve requirements in spec.json
- Otherwise: Verify approval status (stop if unapproved, see Safety & Fallback)

### Step 2: Discovery & Analysis

**Critical: This phase ensures design is based on complete, accurate information.**

1. **Classify Feature Type**:
   - **New Feature** (greenfield) → Full discovery required
   - **Extension** (existing system) → Integration-focused discovery
   - **Simple Addition** (CRUD/UI) → Minimal or no discovery
   - **Complex Integration** → Comprehensive analysis required

2. **Execute Appropriate Discovery Process**:

   **For Complex/New Features**:
   - Read and execute `${CLAUDE_PLUGIN_ROOT}/templates/rules/design-discovery-full.md`
   - Conduct thorough research using WebSearch/WebFetch

   **For Extensions**:
   - Read and execute `${CLAUDE_PLUGIN_ROOT}/templates/rules/design-discovery-light.md`
   - Focus on integration points, existing patterns, compatibility

   **For Simple Additions**:
   - Skip formal discovery, quick pattern check only

3. **Retain Discovery Findings for Step 3**:
   - External API contracts and constraints
   - Technology decisions with rationale
   - Existing patterns to follow or extend
   - Integration points and dependencies
   - Parallelization considerations for future tasks

4. **Persist Findings to Research Log**:
   - Create or update `.yy-dev/specs/$1/research.md` using the shared template
   - Use the language specified in spec.json

### Step 3: Generate Design Document

1. **Load Design Template and Rules**:
   - Read `${CLAUDE_PLUGIN_ROOT}/templates/specs/design.md` for structure
   - Read `${CLAUDE_PLUGIN_ROOT}/templates/rules/design-principles.md` for principles

2. **Generate Design Document**:
   - **Follow specs/design.md template structure strictly**
   - **Integrate all discovery findings**
   - If existing design.md found, use it as reference context (merge mode)
   - Apply design rules: Type Safety, Visual Communication, Formal Tone
   - Use language specified in spec.json

3. **Update Metadata** in spec.json:
   - Set `phase: "design-generated"`
   - Set `approvals.design.generated: true, approved: false`
   - Set `approvals.requirements.approved: true`
   - Update `updated_at` timestamp

## Critical Constraints
- **Type Safety**: Enforce strong typing aligned with the project's technology stack
- **Latest Information**: Use WebSearch/WebFetch for external dependencies
- **Steering Alignment**: Respect existing architecture patterns
- **Template Adherence**: Follow specs/design.md template structure strictly
- **Design Focus**: Architecture and interfaces ONLY, no implementation code
- **Requirements Traceability IDs**: Use numeric requirement IDs only
</instructions>

## Tool Guidance
- **Read first**: Load all context before taking action
- **Research when uncertain**: Use WebSearch/WebFetch for external dependencies
- **Analyze existing code**: Use Grep to find patterns and integration points
- **Write last**: Generate design.md only after all research complete

## Output Description
1. **Status**: Confirm design document generated
2. **Discovery Type**: Which discovery process was executed
3. **Key Findings**: 2-3 critical insights from research.md
4. **Next Action**: Approval workflow guidance

**Format**: Concise Markdown (under 200 words)

## Safety & Fallback

**Requirements Not Approved**:
- **Stop**: "Requirements not yet approved. Run `/yy:spec-design $1 -y` to auto-approve and proceed"

**Missing Requirements**:
- **Stop**: "No requirements.md found. Run `/yy:spec-requirements $1` first"

**Steering Context Missing**:
- **Warning**: Proceed but note limitation

### Next Phase: Task Generation

**If Design Approved**:
- **Optional**: Run `/yy:validate-design $1` for quality review
- Then `/yy:spec-tasks $1 -y` to generate implementation tasks

**If Modifications Needed**:
- Re-run `/yy:spec-design $1` (existing design used as reference)
