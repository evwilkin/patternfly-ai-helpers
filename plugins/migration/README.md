# Migration Plugin

Analyze breaking changes, generate migration guides, and assist with PatternFly version upgrades.

## Commands

### `/analyze-breaking-changes`
Identify potential API disruptions from code changes across PatternFly components and packages.

**Purpose:**
- Detect breaking changes in component APIs, props, CSS variables, and imports
- Analyze impact on consumers and downstream dependencies
- Generate detailed breaking change reports with severity classifications
- Identify affected code patterns and provide remediation guidance

**Use cases:**
- Pre-release breaking change analysis for major/minor versions
- Code review validation for API changes
- Impact assessment before merging potentially breaking PRs
- Automated detection during CI/CD pipelines

### `/generate-migration-guide`
Create comprehensive migration documentation for version upgrades with before/after examples.

**Purpose:**
- Generate structured migration guides for version upgrades
- Provide step-by-step upgrade instructions with code examples
- Document all breaking changes with migration paths
- Create version compatibility matrices
- Include rollback strategies and troubleshooting tips

**Use cases:**
- Creating release migration documentation
- Documenting major version upgrade paths
- Providing consumer upgrade assistance
- Generating internal upgrade checklists

### `/upgrade-assistant`
Interactive helper for upgrading PatternFly versions with automated migration support.

**Purpose:**
- Guide users through version upgrade process interactively
- Suggest and generate automated migration scripts (codemods)
- Validate upgrade compatibility and dependencies
- Provide real-time upgrade progress and validation
- Generate custom migration scripts for specific codebases

**Use cases:**
- Assisting consumers with complex version upgrades
- Automating repetitive migration tasks
- Validating successful upgrades
- Generating project-specific codemods

## Installation

This plugin is part of the PatternFly AI Helpers repository. No additional installation required.

## Requirements

- Access to PatternFly codebase and documentation
- Git access for analyzing code changes
- Node.js for running codemods and migration scripts

## Best Practices

1. **Run breaking change analysis early** - Analyze changes during development, not just before release
2. **Document deprecation paths** - Always provide clear migration paths for deprecated APIs
3. **Test migration guides** - Validate all code examples in migration documentation
4. **Version codemods** - Tag and version migration scripts for specific version upgrades
5. **Maintain compatibility matrices** - Keep version compatibility documentation up to date

## Support

For issues or questions, please refer to the PatternFly documentation or open an issue in the PatternFly repository.
