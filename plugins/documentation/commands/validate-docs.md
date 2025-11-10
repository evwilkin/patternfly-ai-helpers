---
description: Validate component documentation accuracy against code
---

# Documentation Validator

You are validating that PatternFly component documentation accurately reflects the current code implementation.

## Input
The user will provide:
- A component name
- Or a directory of components to validate
- Or "all" for complete documentation validation

## Your Task

### Phase 1: Load Component and Documentation
1. Locate component source file(s)
2. Extract prop definitions, types, and defaults
3. Parse JSDoc comments
4. Fetch published documentation using `mcp__pf-mcp__usePatternFlyDocs`

### Phase 2: Validation Checks

Run these validation checks:

#### 1. Props Table Accuracy
- ✅ All props in code are documented
- ❌ Documented props that don't exist in code
- ❌ Type mismatches between code and docs
- ❌ Incorrect default values
- ⚠️ Missing prop descriptions

#### 2. Code Examples Validity
- ✅ Examples use valid prop combinations
- ❌ Examples import non-existent components
- ❌ Examples use removed or deprecated props
- ❌ TypeScript compilation errors in examples
- ⚠️ Examples don't follow best practices

#### 3. Accessibility Documentation
- ✅ All ARIA attributes documented
- ❌ Missing keyboard navigation documentation
- ❌ Accessibility implementation doesn't match docs
- ⚠️ Missing screen reader behavior description

#### 4. Design Guidelines Alignment
- ✅ Documented use cases match component capabilities
- ❌ Guidelines show features not implemented
- ❌ Visual specs don't match actual component
- ⚠️ Missing responsive behavior documentation

#### 5. Version Accuracy
- ✅ Correct version numbers
- ❌ Deprecated features not marked
- ❌ Beta/experimental features not flagged
- ⚠️ Missing migration guides for breaking changes

### Phase 3: Test Code Examples

For each code example in documentation:
1. Extract the example code
2. Check for syntax errors
3. Verify imports are correct
4. Validate prop types match component definition
5. Flag any runtime issues

### Phase 4: Generate Validation Report

```markdown
# Documentation Validation Report

**Component:** [ComponentName]
**Validation Date:** [YYYY-MM-DD]
**Component Version:** [version]
**Documentation Last Updated:** [date if available]

---

## Validation Summary

**Overall Status:** [✅ PASS / ⚠️ WARNINGS / ❌ FAILED]

| Category | Status | Issues Found |
|----------|--------|--------------|
| Props Table | [✅/⚠️/❌] | [count] |
| Code Examples | [✅/⚠️/❌] | [count] |
| Accessibility Docs | [✅/⚠️/❌] | [count] |
| Design Guidelines | [✅/⚠️/❌] | [count] |
| Version Info | [✅/⚠️/❌] | [count] |

---

## ❌ Critical Issues

### Props Table Errors

#### 1. Undocumented Props
**Issue:** Props exist in code but not in documentation

| Prop Name | Type | Added In Version |
|-----------|------|------------------|
| missingProp | `boolean` | v5.2.0 |

**Impact:** Users unaware of available props
**Action Required:** Add to props table with description

---

#### 2. Documented Props Not in Code
**Issue:** Documentation references props that don't exist

| Prop Name | Last Seen Version | Migration Path |
|-----------|-------------------|----------------|
| oldProp | v4.8.0 | Use `newProp` instead |

**Impact:** Users may try to use non-existent props
**Action Required:** Remove from docs or add deprecation note

---

#### 3. Type Mismatches
**Issue:** Prop types in docs don't match code

| Prop Name | Documented Type | Actual Type | Breaking? |
|-----------|----------------|-------------|-----------|
| variant | `'primary' \| 'secondary'` | `'primary' \| 'secondary' \| 'tertiary'` | No |

**Impact:** Users may miss available options or use invalid values
**Action Required:** Update prop type in documentation

---

### Code Example Errors

#### Example 1: "Basic Usage"
**Location:** docs/components/[component].md:42-56

**Issues Found:**
```tsx
// ❌ Error: Property 'removedProp' does not exist
<Component removedProp="value" />

// ❌ Error: Type 'invalid' is not assignable to type 'primary' | 'secondary'
<Component variant="invalid" />
```

**How to Fix:**
```tsx
// ✅ Corrected version
<Component variant="primary" />
```

---

## ⚠️ Warnings

### Missing Documentation Sections

#### Accessibility
- [ ] **Keyboard navigation:** No table of keyboard shortcuts
- [ ] **Screen reader:** Missing screen reader announcement behavior
- [ ] **Focus management:** Focus behavior not documented

**Recommendation:** Add complete accessibility section using template

---

#### Design Guidelines
- [ ] **Responsive behavior:** Mobile/tablet behavior not specified
- [ ] **Dark theme:** Dark theme considerations missing
- [ ] **RTL support:** Right-to-left language support not documented

**Recommendation:** Collaborate with design team to add guidelines

---

### Examples Missing

**Common use cases without examples:**
- Disabled state
- Error state
- Loading state
- With icons
- Responsive sizing

**Recommendation:** Add examples for these common patterns

---

## ✅ Validation Passed

The following documentation is accurate:

### Props Documented Correctly
- `variant` - Type, default, and description match code
- `isDisabled` - Correctly documented including behavior
- `children` - ReactNode type and usage documented

### Working Code Examples
- ✅ **Basic Usage** - Compiles and runs correctly
- ✅ **With Custom Styling** - Valid prop usage
- ✅ **Controlled Component** - Proper state management shown

### Complete Documentation
- ✅ **Accessibility Section** - Complete ARIA and keyboard docs
- ✅ **Related Components** - Accurate links and comparisons

---

## Detailed Example Validation

### Example: "Basic Usage"
**Status:** ✅ PASS

```tsx
// Validated: Compiles successfully
import { Component } from '@patternfly/react-core';

const Example = () => (
  <Component variant="primary">
    Click me
  </Component>
);
```

**Validation Checks:**
- ✅ Import path correct
- ✅ All props valid
- ✅ Types correct
- ✅ Follows best practices

---

### Example: "Advanced Pattern"
**Status:** ❌ FAIL

```tsx
// ❌ TypeScript Error: Property 'oldProp' does not exist
<Component oldProp={true} />
```

**Required Fix:**
```tsx
// ✅ Updated version
<Component newProp={true} />
```

---

## Recommendations

### Immediate Actions (Required)
1. **Remove** documentation for `oldProp` (no longer exists)
2. **Add** documentation for `newFeatureProp` (added in v5.1.0)
3. **Fix** type mismatch for `variant` prop
4. **Update** "Advanced Pattern" example to use current API

### Short-term Improvements (Recommended)
1. Add missing accessibility documentation
2. Create examples for common use cases
3. Add responsive behavior guidelines
4. Document dark theme considerations

### Long-term Enhancements (Nice to Have)
1. Add interactive examples
2. Create migration guides for each major version
3. Add troubleshooting section
4. Include performance considerations

---

## Action Items

**For Technical Writers:**
- [ ] Update props table with missing props
- [ ] Remove or deprecate documentation for removed props
- [ ] Fix code examples with TypeScript errors
- [ ] Add missing accessibility section

**For Developers:**
- [ ] Review and confirm prop changes
- [ ] Validate example fixes
- [ ] Add JSDoc comments for new props

**For Designers:**
- [ ] Provide responsive behavior guidelines
- [ ] Review and update visual specifications
- [ ] Confirm dark theme documentation

---

## Files Requiring Updates

1. `docs/components/[component].md` - Main documentation
2. `docs/components/[component]-examples.md` - Code examples
3. `CHANGELOG.md` - Document breaking changes if any

---

## Validation Methodology

This report was generated by:
1. Parsing TypeScript definitions from source code
2. Comparing with published documentation
3. Compiling all code examples with TypeScript
4. Cross-referencing with PatternFly guidelines
5. Checking accessibility implementation

**Code Version:** [git commit hash]
**Documentation Version:** [last updated date]
```

## Critical Requirements

✅ **DO:**
- Extract actual types from TypeScript source
- Actually attempt to compile code examples
- Provide specific line numbers for issues
- Distinguish between critical errors and warnings
- Offer concrete fix recommendations
- Check accessibility implementation vs documentation
- Validate version information accuracy

❌ **DON'T:**
- Assume examples work without validation
- Skip type checking
- Flag warnings as critical errors
- Provide vague "needs update" feedback
- Ignore accessibility documentation gaps
- Overlook deprecated features

## Output

Generate a comprehensive validation report with specific, actionable findings and recommendations.
