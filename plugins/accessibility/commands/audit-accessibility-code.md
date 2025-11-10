---
description: Audit React components for PatternFly accessibility compliance
---

# Component Accessibility Auditor (Code)

You are conducting a comprehensive accessibility audit of PatternFly React component code.

## Input
The user will provide either:
- A specific file path to a component
- A directory to scan multiple components
- No path (scan current directory)

## Your Task

### Phase 1: Code Analysis
1. Read the component file(s) provided
2. Identify all interactive elements (buttons, links, inputs, custom controls)
3. Extract ARIA attributes, roles, and properties
4. Analyze keyboard event handlers
5. Check for semantic HTML usage
6. Identify form controls and their labels

### Phase 2: Fetch PatternFly Guidelines
Use `mcp__pf-mcp__usePatternFlyDocs` to fetch accessibility documentation for relevant components:
- General accessibility guidelines
- Component-specific accessibility requirements
- ARIA pattern documentation

### Phase 3: Accessibility Audit

Check for the following issues:

#### 1. ARIA Compliance
- ✅ Proper ARIA roles on custom controls
- ✅ Required ARIA attributes present
- ✅ ARIA states updated dynamically
- ❌ Redundant ARIA (e.g., `role="button"` on `<button>`)
- ❌ Invalid ARIA attribute combinations
- ❌ Hardcoded aria-label values that should be dynamic

#### 2. Keyboard Navigation
- ✅ All interactive elements keyboard accessible
- ✅ Proper focus management
- ✅ Logical tab order
- ✅ Keyboard shortcuts documented
- ❌ Missing onKeyDown/onKeyUp handlers for custom controls
- ❌ Trapped focus without escape mechanism
- ❌ Incorrect tabIndex usage

#### 3. Screen Reader Support
- ✅ Meaningful labels and descriptions
- ✅ Live regions for dynamic content
- ✅ Proper heading hierarchy
- ❌ Missing alt text on images
- ❌ Unlabeled form controls
- ❌ Missing aria-live for status updates

#### 4. Semantic HTML
- ✅ Use of semantic elements (`<button>`, `<nav>`, `<main>`, etc.)
- ✅ Proper heading structure (h1-h6)
- ✅ Lists using `<ul>`, `<ol>`, `<li>`
- ❌ Div soup (interactive divs instead of buttons)
- ❌ Missing landmark regions

#### 5. Form Accessibility
- ✅ Labels associated with inputs
- ✅ Error messages announced
- ✅ Required fields indicated
- ❌ Missing field descriptions
- ❌ No error prevention/validation

### Phase 4: Generate Report

Create a structured accessibility audit report:

```markdown
# Accessibility Audit Report

## Component(s) Audited
- **File:** [path]
- **Date:** [YYYY-MM-DD]
- **Audit Scope:** Code Implementation

---

## Executive Summary

**Overall Accessibility Score:** [%] (based on issues found)

**Severity Breakdown:**
- 🔴 Critical: [count] issues
- 🟡 Moderate: [count] issues
- 🟢 Minor: [count] issues

---

## Detailed Findings

### 🔴 Critical Issues

#### 1. [Issue Title]
**Location:** `file.tsx:line`

**Current Code:**
```tsx
[problematic code]
```

**Issue:**
[Explanation of why this is a problem]

**WCAG Guideline:** [X.X.X Level A/AA/AAA]

**How to Fix:**
```tsx
[corrected code]
```

**Why This Fix Works:**
[Explanation]

---

### 🟡 Moderate Issues

[Same format as critical]

---

### 🟢 Minor Issues / Recommendations

[Same format]

---

## ✅ Accessibility Strengths

The following patterns are correctly implemented:
- [List of correct implementations]

---

## Testing Checklist

Use this checklist to verify accessibility:

### Automated Testing
- [ ] Run axe-core or similar linter
- [ ] Verify no ARIA violations in console
- [ ] Check keyboard navigation in browser

### Manual Testing
- [ ] Navigate entire component using only keyboard
- [ ] Test with screen reader (NVDA/JAWS/VoiceOver)
- [ ] Verify focus visibility at all times
- [ ] Check color contrast meets WCAG AA
- [ ] Test with browser zoom at 200%

### Code Review
- [ ] All interactive elements keyboard accessible
- [ ] ARIA attributes match PatternFly patterns
- [ ] Dynamic content announces to screen readers
- [ ] Form validation errors are accessible

---

## Recommended Actions

**Priority 1 (Immediate):**
1. [Critical fixes]

**Priority 2 (This Sprint):**
1. [Moderate fixes]

**Priority 3 (Backlog):**
1. [Minor improvements]

---

## Resources

- **PatternFly Accessibility:** https://www.patternfly.org/accessibility/accessibility-fundamentals
- **WCAG 2.1 Quick Reference:** https://www.w3.org/WAI/WCAG21/quickref/
- **ARIA Authoring Practices:** https://www.w3.org/WAI/ARIA/apg/
- **Component-Specific Docs:** [Links to relevant PatternFly component docs]
```

## Critical Requirements

✅ **DO:**
- Provide specific line numbers for issues
- Include working code examples for fixes
- Reference WCAG guidelines by number
- Distinguish between critical and minor issues
- Acknowledge correct accessibility patterns
- Generate actionable testing checklist
- Focus on PatternFly-specific patterns

❌ **DON'T:**
- Flag issues without providing solutions
- Make assumptions about dynamic behavior without seeing state management
- Recommend non-PatternFly patterns
- Skip acknowledging correct implementations
- Provide generic accessibility advice without context

## Output

Generate a complete accessibility audit report with specific, actionable recommendations.
