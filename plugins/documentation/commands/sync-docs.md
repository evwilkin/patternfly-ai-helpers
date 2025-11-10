---
description: Sync component documentation with code changes
---

# Component Documentation Sync

You are helping PatternFly maintainers keep documentation synchronized with component code changes.

## Input
The user will provide:
- A component file path
- Or a component name

## Your Task

### Phase 1: Analyze Component Code
1. Read the component source file
2. Extract TypeScript interface/type definitions for props
3. Parse JSDoc comments
4. Identify component variants and examples in the code
5. Note accessibility features implemented
6. Check for breaking changes in git history (if requested)

### Phase 2: Fetch Current Documentation
Use `mcp__pf-mcp__usePatternFlyDocs` to fetch:
- Current component documentation
- Published props table
- Existing code examples

### Phase 3: Compare and Detect Changes

Identify discrepancies:

#### Props Changes
- ✅ New props added (need documentation)
- ✅ Props removed (breaking change)
- ✅ Type changes (potentially breaking)
- ✅ Default value changes
- ✅ Prop renamed (breaking change)
- ⚠️ JSDoc descriptions missing or outdated

#### Examples
- ❌ Examples using removed props
- ❌ Examples with incorrect prop types
- ❌ Missing examples for common use cases
- ⚠️ Examples not following current best practices

#### Accessibility Documentation
- ❌ Missing ARIA documentation
- ❌ Keyboard navigation not documented
- ❌ Screen reader behavior not described
- ⚠️ Accessibility examples missing

#### Design Guidelines
- ⚠️ Visual guidelines don't match implementation
- ⚠️ Use cases not documented
- ⚠️ Component composition examples missing

### Phase 4: Generate Updated Documentation

Create comprehensive documentation following this structure:

```markdown
# [Component Name]

## Overview
[Brief description of component purpose and use cases]

---

## Usage

### Basic Example
```tsx
import { ComponentName } from '@patternfly/react-core';

const Example = () => (
  <ComponentName
    // Essential props
  />
);
```

---

## Props

### ComponentName Props

| Prop name | Type | Default | Description |
|-----------|------|---------|-------------|
| propName | `string` | - | [Description from JSDoc] |
| optionalProp | `boolean` | `false` | [Description] |

**Additional Details:**
- **propName**: [Extended explanation if needed, usage notes]

---

## Examples

### [Example Category 1]
```tsx
// Code example with explanation
```

### [Example Category 2]
```tsx
// Code example with explanation
```

---

## Accessibility

### ARIA Attributes
- **aria-label**: [When and how to use]
- **aria-describedby**: [When and how to use]

### Keyboard Navigation
- **Tab**: [Behavior]
- **Enter/Space**: [Behavior]
- **Escape**: [Behavior]
- **Arrow Keys**: [Behavior if applicable]

### Screen Reader Support
[How the component announces to screen readers]

### Focus Management
[How focus is handled]

---

## Design Guidelines

### When to Use
- [Use case 1]
- [Use case 2]

### When Not to Use
- [Anti-pattern 1]
- [Anti-pattern 2]

### Visual Specifications
- [Spacing requirements]
- [Color usage]
- [Responsive behavior]

---

## Variations

### [Variation Name]
[Description and example]

---

## Related Components
- **[RelatedComponent]**: [When to use this instead]

---

## Migration Notes
[If there are breaking changes]

### Migrating from v[X] to v[Y]
**Changed:**
- `oldProp` renamed to `newProp`
- `removedProp` removed, use `newApproach` instead

**Before:**
```tsx
<Component oldProp="value" />
```

**After:**
```tsx
<Component newProp="value" />
```

---

## Resources
- [PatternFly Design Guidelines](https://www.patternfly.org/components/[component])
- [React Component API](https://www.patternfly.org/components/[component]/react)
```

## Change Summary Report

Also generate a change summary report:

```markdown
# Documentation Sync Report: [Component Name]

**Date:** [YYYY-MM-DD]
**Component File:** [path]

---

## Changes Detected

### Props Changes

#### 🆕 New Props
| Prop | Type | Description |
|------|------|-------------|
| newProp | `string` | [description] |

**Documentation Action:** Added to props table with full description

---

#### 🔴 Removed Props (BREAKING)
| Prop | Type | Migration Path |
|------|------|----------------|
| oldProp | `boolean` | Use `newProp` instead |

**Documentation Action:** Added migration notes, updated examples

---

#### ⚠️ Modified Props
| Prop | Old Type | New Type | Breaking? |
|------|----------|----------|-----------|
| changedProp | `string` | `string \| number` | No (additive) |

**Documentation Action:** Updated type in props table

---

### Code Examples

#### ❌ Examples Needing Updates
1. **Basic Usage Example** - Uses removed `oldProp`
   - **Fixed:** Updated to use `newProp`

2. **Advanced Example** - Missing new `featureProp`
   - **Added:** New example showing `featureProp` usage

---

### Accessibility Documentation

#### Missing Accessibility Docs
- [ ] ARIA labels documentation added
- [ ] Keyboard navigation table added
- [ ] Screen reader behavior documented

**Documentation Action:** Added complete accessibility section

---

### Design Guidelines

#### Updates Needed
- [ ] New variant patterns documented
- [ ] Updated visual specifications
- [ ] Added responsive behavior notes

---

## Files Updated

- `docs/components/[component].md` - Main documentation
- `docs/components/[component]-examples.md` - Code examples
- `CHANGELOG.md` - Added entry for breaking changes

---

## Review Checklist

Before publishing:
- [ ] All new props documented with types and descriptions
- [ ] Breaking changes noted with migration path
- [ ] Code examples compile and run
- [ ] Accessibility documentation complete
- [ ] Design guidelines align with implementation
- [ ] Related components linked
- [ ] Changelog updated if breaking changes

---

## Next Steps

1. Review generated documentation for accuracy
2. Test all code examples
3. Get design team review on guideline changes
4. Update any related documentation
5. Publish with next release
```

## Critical Requirements

✅ **DO:**
- Extract actual prop types from TypeScript definitions
- Preserve and enhance JSDoc comments
- Generate working, tested code examples
- Document breaking changes clearly
- Provide migration paths for removed/changed props
- Include complete accessibility documentation
- Reference design guidelines
- Update changelogs appropriately

❌ **DON'T:**
- Make assumptions about prop behavior without reading code
- Skip migration notes for breaking changes
- Provide untested code examples
- Ignore accessibility documentation
- Forget to check git history for recent changes
- Leave outdated examples in documentation

## Interactive Workflow

1. Show the detected changes first
2. Ask user to confirm breaking changes before documenting
3. Offer to generate examples for new props
4. Request design team input if guidelines are unclear

## Output

Generate complete, updated documentation and a detailed change summary report.
