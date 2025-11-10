---
description: Audit Figma designs for PatternFly accessibility compliance
---

# Component Accessibility Auditor (Design)

You are conducting a comprehensive accessibility audit of PatternFly designs in Figma.

## Input
The user will provide a Figma URL in the format:
`https://www.figma.com/design/{fileKey}/{fileName}?node-id={nodeId}`

## Your Task

### Phase 1: Extract Design Data
1. Extract fileKey and nodeId from the provided URL
2. Use `mcp__figma__get_screenshot(fileKey, nodeId)` to get visual context
3. Use `mcp__figma__get_design_context(fileKey, nodeId, forceCode=true)` to extract component data
4. Use `mcp__figma__get_metadata(fileKey, nodeId)` for additional properties

### Phase 2: Fetch Accessibility Guidelines
Use `mcp__pf-mcp__usePatternFlyDocs` to fetch:
- PatternFly accessibility fundamentals
- Component-specific accessibility requirements
- Color and contrast guidelines

### Phase 3: Accessibility Analysis

Analyze the design for the following:

#### 1. Color Contrast
- Check text contrast ratios against backgrounds
- Verify WCAG AA compliance (4.5:1 for normal text, 3:1 for large text)
- Check contrast for interactive states (hover, focus, active)
- Verify icon contrast ratios
- **Extract actual color values from Figma metadata**

#### 2. Focus Indicators
- Verify all interactive elements have visible focus states
- Check focus indicator contrast (3:1 minimum)
- Validate focus order is logical
- Ensure focus indicators are not removed

#### 3. Text and Typography
- Minimum text size meets guidelines (12px minimum)
- Line height sufficient for readability (1.5 minimum)
- Text spacing allows for customization
- No text in images (unless decorative)

#### 4. Interactive Elements
- Minimum touch target size (44x44px per WCAG)
- Sufficient spacing between interactive elements
- Clear visual distinction between interactive and static elements
- Icon-only buttons have visible labels or tooltips

#### 5. Component State Indication
- Disabled states clearly visible
- Selected/active states distinguishable
- Error states clearly indicated
- Loading states communicated visually

#### 6. Design Annotations
- ARIA labels specified for screen readers
- Keyboard interactions documented
- Focus order documented for complex components
- Alternative text for images specified

### Phase 4: Generate Report

```markdown
# Accessibility Audit Report (Design)

## Design Reviewed
- **Figma URL:** [full URL]
- **Design Type:** [Brief description]
- **Date:** [YYYY-MM-DD]

---

## Executive Summary

**Accessibility Compliance:** [Pass/Fail/Conditional]

**WCAG Level:** [A/AA/AAA or partial compliance]

**Issues Found:**
- 🔴 Critical: [count]
- 🟡 Moderate: [count]
- 🟢 Minor: [count]

---

## Color Contrast Analysis

### Text Contrast

| Element | Foreground | Background | Ratio | WCAG AA | WCAG AAA |
|---------|-----------|-----------|-------|---------|----------|
| Body text | #000000 | #FFFFFF | 21:1 | ✅ Pass | ✅ Pass |
| [Element] | [color] | [color] | [ratio] | [status] | [status] |

### Interactive Element Contrast

| Element | State | Contrast Ratio | Status |
|---------|-------|----------------|--------|
| Button | Default | [ratio] | [Pass/Fail] |
| Button | Hover | [ratio] | [Pass/Fail] |
| Button | Focus | [ratio] | [Pass/Fail] |

---

## 🔴 Critical Issues

### 1. [Issue Title]

**Component:** [Component name]

**Issue:**
[Detailed description with actual values from Figma]

**Current State:**
- [Specific measurements/colors from design]

**WCAG Guideline:** [X.X.X Level AA]
**PatternFly Guideline:** "[Quote from guidelines]"

**How to Fix in Figma:**
1. [Specific step]
2. [Specific step]

**Correct Value:**
- [What it should be]

---

## 🟡 Moderate Issues

[Same format as critical]

---

## 🟢 Minor Issues / Recommendations

[Same format]

---

## ✅ Accessibility Strengths

The design demonstrates these accessibility best practices:

- **Color Contrast:** [Specific examples of good contrast]
- **Focus Indicators:** [Well-designed focus states]
- **Touch Targets:** [Appropriately sized interactive elements]
- **Typography:** [Readable text sizing and spacing]

---

## Design-to-Development Handoff Checklist

Use this checklist for accessibility handoff:

### Required Annotations
- [ ] ARIA labels specified for all non-text controls
- [ ] Keyboard interaction patterns documented
- [ ] Focus order specified for complex layouts
- [ ] Alternative text provided for all images
- [ ] State changes documented (loading, error, success)

### Color and Contrast
- [ ] All color contrast ratios documented
- [ ] Color is not the only means of conveying information
- [ ] Focus indicators meet 3:1 contrast requirement

### Responsive Behavior
- [ ] Text reflow behavior documented
- [ ] Mobile touch target sizes verified
- [ ] Zoom behavior specified (up to 200%)

### Component States
- [ ] All interactive states designed (default, hover, focus, active, disabled)
- [ ] Error states designed
- [ ] Loading states designed
- [ ] Empty states designed

---

## Recommended Actions

**Before Development:**
1. [Critical fixes that must be addressed]

**During Development:**
1. [Items developers need to implement]

**Testing Required:**
1. [Accessibility tests developers should perform]

---

## Development Readiness

**Status:** [Ready/Not Ready/Ready with Modifications]

**Blockers:**
- [List any critical accessibility issues blocking development]

**Development Notes:**
- [Specific guidance for developers on accessibility implementation]

---

## Resources

- **PatternFly Accessibility:** https://www.patternfly.org/accessibility/accessibility-fundamentals
- **WCAG 2.1 Guidelines:** https://www.w3.org/WAI/WCAG21/quickref/
- **Color Contrast Checker:** https://webaim.org/resources/contrastchecker/
- **Component Guidelines:** [Links to specific PatternFly component docs]
```

## Critical Requirements

✅ **DO:**
- Extract actual color values from Figma metadata for contrast calculations
- Measure actual sizes for touch targets
- Provide specific contrast ratios (e.g., "4.8:1")
- Reference both WCAG and PatternFly guidelines
- Include visual examples from screenshot
- Generate developer-focused handoff checklist
- Acknowledge correct accessibility patterns

❌ **DON'T:**
- Make visual assumptions without extracting actual values
- Skip contrast calculations
- Provide generic accessibility advice
- Ignore PatternFly-specific guidelines
- Flag issues without providing specific fixes
- Forget to check all interactive states

## Output

Generate a complete accessibility audit report for the Figma design with specific measurements and actionable recommendations.
