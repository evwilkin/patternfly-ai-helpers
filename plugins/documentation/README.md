# Documentation Plugin

Ensure PatternFly component documentation stays synchronized with code changes and maintains accuracy.

## Available Commands

### `/sync-docs`

Detects prop changes and generates updated documentation.

**Usage:**
```
/sync-docs [component-file]
```

**Example:**
```
/sync-docs src/components/Alert/Alert.tsx
```

**What it does:**
1. Analyzes component TypeScript interfaces/props
2. Compares with existing documentation
3. Detects prop additions, removals, and type changes
4. Validates code examples still work
5. Generates updated documentation markdown
6. Checks design guideline alignment

**Output:**
- Updated component documentation
- Migration notes for breaking changes
- List of code examples that need updates
- Accessibility documentation checklist

---

### `/validate-docs`

Validates that documentation matches current code.

**Usage:**
```
/validate-docs [component-name or directory]
```

**Example:**
```
/validate-docs Alert
```

**What it does:**
1. Reads component source code
2. Fetches published documentation
3. Compares prop definitions
4. Validates code examples compile
5. Checks for missing accessibility docs
6. Verifies design guidelines match implementation

**Output:**
- Validation report with discrepancies
- List of outdated examples
- Missing documentation sections
- Recommendations for updates

---

### `/generate-docs`

Generates complete documentation for a component.

**Usage:**
```
/generate-docs [component-file]
```

**Example:**
```
/generate-docs src/components/NewComponent/NewComponent.tsx
```

**What it does:**
1. Analyzes component code and props
2. Extracts JSDoc comments
3. Generates usage examples
4. Creates accessibility documentation
5. Builds props table
6. Suggests design guidelines

**Output:**
- Complete markdown documentation
- React component examples
- Props API reference
- Accessibility implementation notes
- Testing recommendations

---

## How to Use

1. Make changes to a component
2. Run `/sync-docs [component]` to update docs
3. Review generated documentation
4. Run `/validate-docs` before publishing
5. Commit documentation alongside code changes

## Documentation Structure

Generated documentation follows this structure:
- **Overview**: Component purpose and use cases
- **Usage**: Basic example
- **Props**: Complete props table with types and defaults
- **Examples**: Common patterns and variations
- **Accessibility**: ARIA requirements and keyboard support
- **Design Guidelines**: Visual and UX guidance
- **Related Components**: Links to similar components

## Related Documentation

- [PatternFly Documentation Guidelines](https://www.patternfly.org/contribute/documentation)
- [Component Documentation Template](https://github.com/patternfly/patternfly-react/blob/main/.github/COMPONENT_TEMPLATE.md)
