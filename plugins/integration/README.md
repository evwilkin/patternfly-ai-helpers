# Integration Plugin

Debug component integration issues, resolve styling conflicts, and check compatibility in PatternFly applications.

## Commands

### `/debug-integration`

Diagnose component integration and compatibility issues in your PatternFly application.

**Use this command when:**
- Components don't render correctly when used together
- You encounter unexpected behavior when composing components
- Props aren't being passed correctly between components
- Component context is not working as expected
- Event handlers conflict between nested components
- Layout breaks when combining certain components

**What it analyzes:**
- Component composition patterns and potential conflicts
- Props flow and type compatibility
- Context provider hierarchies
- Event bubbling and handler conflicts
- CSS cascade and specificity issues
- Component lifecycle interactions
- Portal and overlay positioning
- Z-index stacking contexts

**Outputs:**
- Root cause analysis of integration issues
- Step-by-step debugging guidance
- Component hierarchy visualization
- Recommended fixes with code examples
- Integration patterns and best practices

---

### `/resolve-conflicts`

Identify and resolve CSS and dependency conflicts in your PatternFly project.

**Use this command when:**
- Styles are not applying as expected
- Global styles interfere with component styles
- CSS specificity wars occur
- Multiple versions of dependencies cause issues
- Theme variables are not cascading properly
- Custom styles break PatternFly components
- Third-party libraries conflict with PatternFly

**What it analyzes:**
- CSS specificity and cascade conflicts
- Conflicting style declarations
- Theme variable overrides and scope
- Dependency version incompatibilities
- Duplicate package installations
- CSS-in-JS conflicts
- Global vs. scoped style issues
- Shadow DOM style isolation

**Outputs:**
- Conflict identification and classification
- CSS specificity calculations
- Dependency tree analysis
- Resolution strategies with priority order
- Code examples for fixes
- Migration guides for breaking changes

---

### `/check-compatibility`

Verify PatternFly version compatibility with dependencies and runtime environment.

**Use this command when:**
- Planning to upgrade PatternFly versions
- Adding new dependencies to your project
- Encountering React version warnings
- TypeScript types don't match
- Build errors occur after updates
- Runtime errors suggest version mismatches
- Migrating between major versions

**What it checks:**
- PatternFly version vs. React version compatibility
- Peer dependency requirements
- TypeScript version compatibility
- Node.js version requirements
- Build tool compatibility (Webpack, Vite, etc.)
- SSR framework compatibility (Next.js, Remix, etc.)
- Browser support matrix
- Breaking changes between versions

**Outputs:**
- Compatibility matrix for all dependencies
- Version upgrade recommendations
- Breaking change warnings
- Migration checklist
- Code transformation examples
- Codemod suggestions
- Testing recommendations

## Installation

This plugin is part of the PatternFly AI Helpers collection and includes access to the PatternFly documentation MCP server for enhanced context.

## Use Cases

### Common Integration Issues
- Nested forms and form controls
- Modal dialogs with custom content
- Dropdown menus in table cells
- Tabs containing complex layouts
- Wizards with dynamic steps
- Popovers with interactive content

### Common Conflicts
- Global CSS reset vs. PatternFly styles
- Custom theme variables
- CSS-in-JS library conflicts
- Multiple React versions
- Styled-components interference
- Tailwind CSS conflicts

### Compatibility Checks
- Major version upgrades
- React 17 to React 18 migration
- TypeScript strict mode
- Server-side rendering setup
- Build tool migrations
- Browser compatibility verification

## Tips

- Run `/debug-integration` first to identify if issues are integration-related
- Use `/resolve-conflicts` when styles don't match design specifications
- Use `/check-compatibility` before upgrading dependencies
- Combine commands for comprehensive troubleshooting
- Provide specific error messages and component combinations for faster diagnosis
