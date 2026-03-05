# yy-dev

Spec-driven development workflow plugin for Claude Code.

Structured feature, bugfix, and investigation workflows with steering-based project memory.

## Install

```bash
# Add marketplace and install
/plugin marketplace add PleasurehubTeam/yy-dev
/plugin install yy-dev@yy-dev
```

## Quick Start

```bash
/yy:init "my project description"   # Initialize project steering
/yy:feature "add user auth"         # Implement a feature
/yy:fix "login fails on mobile"     # Fix a bug
/yy:investigate "slow API response"  # Diagnose an issue
```

## Commands

### Daily Work
- `/yy:init` — Project initialization (create steering)
- `/yy:feature` — Feature workflow (auto-sizes: small → TDD, large → plan)
- `/yy:fix` — Bugfix workflow (TDD + code review)
- `/yy:investigate` — Issue investigation (4-phase debugging)
- `/yy:steering` — Bootstrap or sync project steering
- `/yy:status` — View spec status and progress

### Formal Spec Pipeline
- `/yy:spec-requirements` — Generate EARS-format requirements
- `/yy:spec-design` — Technical design with discovery
- `/yy:spec-tasks` — Implementation task generation
- `/yy:spec-impl` — TDD implementation

### Validation
- `/yy:validate-gap` — Requirements vs codebase gap analysis
- `/yy:validate-design` — Design quality review (GO/NO-GO)
- `/yy:validate-impl` — Implementation vs spec verification

## Project Structure

After initialization, your project gets:

```
.yy-dev/
├── steering/          # Project memory (product, tech, structure)
├── specs/             # Decision records and feature docs
│   └── <feature>/     # Per-feature spec directory
│       ├── spec.json
│       ├── requirements.md
│       ├── design.md
│       ├── tasks.md
│       └── changelog.md  # Per-spec decision log
└── config/            # Optional: override plugin templates
```

## Dependencies

- [superpowers](https://github.com/anthropics/superpowers) plugin (for TDD, code review, brainstorming)

## License

MIT
