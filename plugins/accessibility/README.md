# Accessibility Plugin

Comprehensive accessibility auditing and implementation support for PatternFly components in both code and design contexts.

## Available Commands

### `/audit-accessibility-code`

Scans React components for accessibility compliance issues.

**Usage:**
```
/audit-accessibility-code [file-path or directory]
```

**Example:**
```
/audit-accessibility-code src/components/Dashboard.tsx
```

**What it does:**
1. Analyzes component code for ARIA attribute compliance
2. Validates keyboard navigation patterns
3. Checks screen reader compatibility
4. Identifies hardcoded aria-labels that should be dynamic
5. Verifies semantic HTML usage
6. Generates accessibility testing checklist

**Output:**
- Critical accessibility violations with severity ratings
- Recommended fixes with code examples
- Testing checklist for manual verification
- Links to WCAG and PatternFly accessibility guidelines

---

### `/audit-accessibility-design`

Reviews Figma designs for accessibility compliance.

**Usage:**
```
/audit-accessibility-design https://www.figma.com/design/[fileKey]/[fileName]?node-id=[nodeId]
```

**Example:**
```
/audit-accessibility-design https://www.figma.com/design/rxlWfeof9blmF1rZBCItoN/Dashboard?node-id=31-3576
```

**What it does:**
1. Checks color contrast ratios (WCAG AA/AAA)
2. Validates focus indicators visibility
3. Analyzes text sizing and readability
4. Identifies missing accessibility annotations
5. Reviews component state variations for accessibility
6. Validates icon-only controls have labels

**Output:**
- Color contrast analysis with specific ratios
- Missing accessibility features in designs
- Recommendations for design improvements
- Compliance checklist for handoff to development

---

### `/implement-accessibility`

Interactive helper to implement accessibility features in code.

**Usage:**
```
/implement-accessibility [component-file]
```

**Example:**
```
/implement-accessibility src/components/CustomTable.tsx
```

**What it does:**
1. Reviews current component implementation
2. Suggests appropriate ARIA attributes
3. Implements keyboard navigation handlers
4. Adds screen reader announcements
5. Generates accessibility testing checklist
6. Provides testing instructions

**Output:**
- Updated component code with accessibility features
- Inline comments explaining ARIA usage
- Testing checklist
- Example Jest/RTL tests for accessibility

---

## How to Use

1. Navigate to the directory or file you want to audit
2. Run the appropriate command
3. Review the generated report
4. Apply recommended fixes
5. Re-run to verify improvements

## Related Documentation

- [PatternFly Accessibility Guidelines](https://www.patternfly.org/accessibility/accessibility-fundamentals)
- [WCAG 2.1 Guidelines](https://www.w3.org/WAI/WCAG21/quickref/)
- [ARIA Authoring Practices](https://www.w3.org/WAI/ARIA/apg/)
