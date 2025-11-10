# PatternFly AI Helpers Marketplace

A comprehensive collection of Claude Code plugins for designers and developers using and building the PatternFly design system.

## Table of Contents

- [Overview](#overview)
- [Available Plugins](#available-plugins)
- [Plugin Organization](#plugin-organization)
- [For Maintainers vs Consumers](#for-maintainers-vs-consumers)
- [Getting Started](#getting-started)
- [Common Workflows](#common-workflows)
- [MCP Server Configuration](#mcp-server-configuration)
- [Plugin Development](#plugin-development)
- [Resources](#resources)
- [Contributing](#contributing)
- [Support](#support)
- [License](#license)

## Overview

The PatternFly AI Helpers marketplace provides specialized plugins organized by functionality to help with:
- **Design review and validation** - Audit Figma designs against PatternFly guidelines
- **Accessibility compliance** - Ensure code and designs meet WCAG standards
- **Documentation management** - Keep docs synchronized with code changes
- **Testing and quality** - Modernize tests and generate comprehensive test suites
- **Component development** - Suggest, compare, and build with PatternFly components
- **Migration and upgrades** - Safely upgrade between PatternFly versions
- **Integration debugging** - Resolve conflicts and compatibility issues
- **Forms and tables** - Build complex, accessible forms and data tables

## Available Plugins

### 🎨 Design Plugins

#### [Figma](./plugins/figma/)
Review Figma designs against PatternFly guidelines.

**Commands:**
- `/design-review` - Comprehensive PatternFly design review with actionable feedback

**Use Cases:**
- Design handoff validation
- Component configuration verification
- PatternFly compliance checking

---

### ♿ Accessibility Plugins

#### [Accessibility](./plugins/accessibility/)
Audit and implement accessibility best practices for both code and design.

**Commands:**
- `/audit-accessibility-code` - Scan React components for accessibility compliance
- `/audit-accessibility-design` - Review Figma designs for accessibility compliance
- `/implement-accessibility` - Interactive helper to implement accessibility features

**Use Cases:**
- WCAG 2.1 compliance audits
- ARIA attribute validation
- Keyboard navigation implementation
- Screen reader compatibility
- Color contrast analysis

---

### 📚 Documentation Plugins

#### [Documentation](./plugins/documentation/)
Sync component documentation with code changes and maintain accuracy.

**Commands:**
- `/sync-docs` - Detect prop changes and generate updated documentation
- `/validate-docs` - Validate documentation matches current code
- `/generate-docs` - Generate complete documentation for new components

**Use Cases:**
- Keeping docs synchronized during development
- Pre-release documentation validation
- Generating docs for new components
- Identifying breaking changes

---

### 🧪 Testing Plugins

#### [Testing](./plugins/testing/)
Modernize snapshot tests, analyze failures, and generate test suites.

**Commands:**
- `/modernize-snapshots` - Update snapshot tests to modern React Testing Library patterns
- `/analyze-test-failures` - Explain test failures with specific fixes
- `/generate-tests` - Generate comprehensive test suite for components

**Use Cases:**
- Migrating from Enzyme to React Testing Library
- Understanding and fixing test failures
- Generating tests for new components
- Improving test coverage

---

### 🐛 Issue Management Plugins

#### [Issues](./plugins/issues/)
Generate well-documented "Good First Issue" GitHub issues for contributors.

**Commands:**
- `/generate-good-first-issue` - Create detailed, beginner-friendly issues
- `/analyze-issue-opportunity` - Evaluate if something is suitable for new contributors

**Use Cases:**
- Onboarding new contributors
- Creating beginner-friendly issues
- Documenting improvement opportunities
- Building contributor pipeline

---

### 🔄 Migration Plugins

#### [Migration](./plugins/migration/)
Analyze breaking changes and assist with PatternFly version upgrades.

**Commands:**
- `/analyze-breaking-changes` - Identify potential API disruptions
- `/generate-migration-guide` - Create version upgrade documentation
- `/upgrade-assistant` - Interactive helper for upgrading PatternFly versions

**Use Cases:**
- Planning major version upgrades
- Understanding breaking changes impact
- Generating migration documentation
- Automating upgrade processes

---

### 🧩 Component Plugins

#### [Components](./plugins/components/)
Suggest appropriate components, compare alternatives, and prototype usage.

**Commands:**
- `/suggest-component` - Recommend appropriate PatternFly components for use cases
- `/compare-components` - Compare similar components and explain trade-offs
- `/component-playground` - Generate interactive examples to try components

**Use Cases:**
- Choosing the right component for a use case
- Understanding component differences
- Prototyping component implementations
- Learning component capabilities

---

### 🔗 Integration Plugins

#### [Integration](./plugins/integration/)
Debug component integration issues and resolve conflicts.

**Commands:**
- `/debug-integration` - Diagnose component compatibility issues
- `/resolve-conflicts` - Identify and resolve CSS/dependency conflicts
- `/check-compatibility` - Verify PatternFly version compatibility

**Use Cases:**
- Troubleshooting component integration
- Resolving CSS conflicts with other frameworks
- Checking dependency compatibility
- Debugging SSR/hydration issues

---

### 📝 Forms Plugins

#### [Forms](./plugins/forms/)
Build accessible forms and integrate with form libraries.

**Commands:**
- `/build-form` - Generate accessible forms with PatternFly components
- `/add-validation` - Implement form validation with error handling
- `/integrate-form-library` - Integrate with React Hook Form, Formik, etc.

**Use Cases:**
- Building complex forms quickly
- Implementing validation patterns
- Integrating with form management libraries
- Ensuring form accessibility

---

### 📊 Tables Plugins

#### [Tables](./plugins/tables/)
Configure data tables, add features, and optimize performance.

**Commands:**
- `/configure-table` - Analyze data and recommend optimal table configuration
- `/add-table-features` - Add sorting, filtering, pagination, selection, actions
- `/optimize-table-performance` - Optimize large tables with virtualization

**Use Cases:**
- Building data tables from scratch
- Adding sorting, filtering, pagination
- Optimizing large dataset performance
- Implementing accessible tables

---

## Plugin Organization

Plugins are organized by **functionality** rather than user type:

```
plugins/
├── figma/              # Design review
├── accessibility/      # Accessibility auditing and implementation
├── documentation/      # Documentation sync and generation
├── testing/           # Test modernization and generation
├── issues/            # Good first issue generation
├── migration/         # Version upgrades and breaking changes
├── components/        # Component selection and comparison
├── integration/       # Integration debugging
├── forms/             # Form building and validation
└── tables/            # Table configuration and optimization
```

## For Maintainers vs Consumers

### Plugins for PatternFly Maintainers
Focused on **building and maintaining** PatternFly itself:

- **Documentation** - Keep component docs synchronized
- **Testing** - Modernize test suites
- **Issues** - Generate good first issues for contributors
- **Migration** - Analyze breaking changes for releases
- **Accessibility** (Code) - Audit component implementations

### Plugins for PatternFly Consumers
Focused on **using** PatternFly in applications:

- **Components** - Choose and use the right components
- **Forms** - Build forms with PatternFly
- **Tables** - Implement data tables
- **Integration** - Debug integration issues
- **Migration** - Upgrade PatternFly versions
- **Accessibility** (Implementation) - Make apps accessible

### Cross-Cutting Plugins
Useful for **both maintainers and consumers**:

- **Figma** - Review designs (both internal and consumer designs)
- **Accessibility** - Comprehensive accessibility support
- **Testing** - Applicable to any React app using PatternFly

## Getting Started

### 1. Browse Plugins
Explore the plugins above and identify which ones match your needs.

### 2. Install Claude Code
Ensure you have Claude Code installed and configured.

### 3. Activate a Plugin
Navigate to a plugin directory to activate it:
```bash
cd plugins/accessibility
```

### 4. Use Commands
Type `/` in Claude Code to see available commands from the active plugin:
```
/audit-accessibility-code src/components/Button.tsx
```

### 5. Switch Plugins
Navigate to a different plugin directory to switch contexts:
```bash
cd plugins/forms
/build-form
```

## Common Workflows

### Design to Development
1. **Figma** - `/design-review` to validate design
2. **Accessibility** - `/audit-accessibility-design` for accessibility review
3. **Components** - `/suggest-component` to confirm component choices
4. **Forms** or **Tables** - Build implementation
5. **Testing** - `/generate-tests` for test coverage
6. **Documentation** - `/generate-docs` for documentation

### Component Development
1. **Components** - `/component-playground` to prototype
2. **Accessibility** - `/implement-accessibility` while building
3. **Testing** - `/generate-tests` for comprehensive tests
4. **Documentation** - `/sync-docs` to update documentation

### Upgrading PatternFly
1. **Migration** - `/analyze-breaking-changes` to understand impact
2. **Migration** - `/generate-migration-guide` for upgrade plan
3. **Migration** - `/upgrade-assistant` for interactive upgrade
4. **Integration** - `/check-compatibility` to verify compatibility
5. **Testing** - `/analyze-test-failures` if tests break

### Quality Assurance
1. **Accessibility** - `/audit-accessibility-code` for WCAG compliance
2. **Testing** - `/modernize-snapshots` to update tests
3. **Documentation** - `/validate-docs` to ensure accuracy
4. **Integration** - `/debug-integration` for any issues

## MCP Server Configuration

Most plugins use the PatternFly MCP server to fetch documentation and guidelines:

```json
{
  "mcpServers": {
    "patternfly-docs": {
      "command": "npx",
      "args": [
        "-y",
        "@patternfly/patternfly-mcp"
      ],
      "description": "PatternFly React development rules and documentation"
    }
  }
}
```

The **Figma** plugin additionally requires the Figma Desktop MCP server:

```json
{
  "mcpServers": {
    "figma-desktop": {
      "type": "http",
      "url": "http://127.0.0.1:3845/mcp"
    }
  }
}
```

## Plugin Development

Each plugin follows a consistent structure:

```
plugin-name/
├── .claude-plugin/
│   └── plugin.json          # Plugin metadata
├── .mcp.json                # MCP server configuration
├── README.md                # Plugin documentation
└── commands/
    ├── command-1.md         # Command implementation
    ├── command-2.md
    └── command-3.md
```

### Command File Structure

Each command file includes:
- **Frontmatter** with description
- **Multi-phase workflow** (Analysis, Implementation, Output)
- **Detailed templates** for structured outputs
- **Critical Requirements** (DO/DON'T sections)
- **PatternFly integration** via MCP
- **Code examples** and patterns

## Resources

- **PatternFly Website**: https://www.patternfly.org
- **PatternFly React**: https://github.com/patternfly/patternfly-react
- **PatternFly Design**: https://github.com/patternfly/patternfly-design
- **PatternFly Documentation**: https://www.patternfly.org/get-started/develop
- **PatternFly Accessibility**: https://www.patternfly.org/accessibility/accessibility-fundamentals
- **Claude Code Documentation**: https://docs.claude.com/claude-code

## Contributing

To add a new plugin:
1. Create plugin directory following the structure above
2. Add plugin.json with metadata
3. Configure MCP servers in .mcp.json
4. Create comprehensive README.md
5. Implement commands with detailed prompts
6. Add plugin to this marketplace README
7. Test commands thoroughly

## Support

For issues or questions:
- **PatternFly AI Helpers**: [GitHub Issues](https://github.com/patternfly/patternfly-ai-helpers/issues)
- **PatternFly General**: [PatternFly Slack](https://patternfly.slack.com)
- **Claude Code**: https://docs.claude.com/claude-code

## License

See individual plugin directories for licensing information.
