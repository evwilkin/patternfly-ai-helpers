---
description: Generate complete documentation for a new or undocumented component
---

# Documentation Generator

You are generating comprehensive documentation for a PatternFly component from scratch.

## Input
The user will provide:
- A component source file path
- Or a component name to locate

## Your Task

### Phase 1: Analyze Component
1. Read the component source file
2. Extract TypeScript interfaces and type definitions
3. Parse JSDoc comments
4. Identify all props, their types, and default values
5. Analyze component variants and states
6. Extract accessibility features implemented
7. Identify related components and imports

### Phase 2: Fetch PatternFly Context
Use `mcp__pf-mcp__usePatternFlyDocs` to:
- Find similar component documentation for reference
- Get PatternFly documentation templates
- Fetch accessibility guidelines
- Review design patterns for similar components

### Phase 3: Generate Complete Documentation

Create comprehensive documentation following PatternFly standards:

```markdown
# [ComponentName]

[Brief one-sentence description of what this component does]

## Overview

[2-3 paragraph overview including:
- Component purpose and primary use case
- Key features
- When to use vs alternatives]

---

## Installation

```bash
npm install @patternfly/react-core
```

**Import:**
```tsx
import { ComponentName } from '@patternfly/react-core';
```

---

## Usage

### Basic Example

```tsx
import React from 'react';
import { ComponentName } from '@patternfly/react-core';

const BasicExample = () => (
  <ComponentName>
    Basic usage with minimal props
  </ComponentName>
);
```

**Result:** [Brief description of what this renders]

---

## Props

### ComponentName Props

Extends: `React.HTMLProps<HTMLDivElement>` [or appropriate base]

| Prop name | Type | Default | Description |
|-----------|------|---------|-------------|
| variant | `'default' \| 'primary' \| 'secondary'` | `'default'` | [Generated from JSDoc or inferred] |
| isDisabled | `boolean` | `false` | [Description] |
| children | `React.ReactNode` | - | Content to display inside component |
| className | `string` | - | Additional CSS classes |
| [...props] | [...] | [...] | [...] |

#### Detailed Prop Descriptions

**variant**
- Controls the visual style of the component
- Options:
  - `'default'`: Standard appearance
  - `'primary'`: Emphasized/call-to-action appearance
  - `'secondary'`: Subdued appearance
- Use `'primary'` for main actions, `'secondary'` for supporting actions

**isDisabled**
- When `true`, component is not interactive
- Applies disabled styling
- Prevents all user interactions
- Note: Use semantic disabled state, not just visual styling

[Continue for complex props...]

---

## Examples

### [Variant Examples]

#### Default Variant
```tsx
<ComponentName variant="default">
  Default content
</ComponentName>
```

#### Primary Variant
```tsx
<ComponentName variant="primary">
  Primary content
</ComponentName>
```

---

### [State Examples]

#### Disabled State
```tsx
<ComponentName isDisabled>
  Cannot interact with this
</ComponentName>
```

#### Loading State
```tsx
<ComponentName isLoading>
  Loading...
</ComponentName>
```

---

### [Composition Examples]

#### With Icons
```tsx
import { CheckIcon } from '@patternfly/react-icons';

<ComponentName icon={<CheckIcon />}>
  With icon
</ComponentName>
```

#### Complex Composition
```tsx
<ComponentName>
  <ComponentHeader>Header Content</ComponentHeader>
  <ComponentBody>
    Main content here
  </ComponentBody>
  <ComponentFooter>Footer</ComponentFooter>
</ComponentName>
```

---

### [Advanced Examples]

#### Controlled Component
```tsx
const [value, setValue] = React.useState('');

<ComponentName
  value={value}
  onChange={(newValue) => setValue(newValue)}
/>
```

#### With Form Integration
```tsx
<Form>
  <FormGroup label="Label" fieldId="example">
    <ComponentName id="example" />
  </FormGroup>
</Form>
```

---

## Accessibility

### ARIA Attributes

This component implements the following ARIA patterns:

| Attribute | When Applied | Purpose |
|-----------|--------------|---------|
| `aria-label` | When no visible label | Provides accessible name |
| `aria-describedby` | When description present | Links to description |
| `aria-disabled` | When `isDisabled={true}` | Indicates disabled state |
| `role="..."` | [Condition] | [Purpose] |

### Keyboard Navigation

| Key | Action |
|-----|--------|
| Tab | Moves focus to/from component |
| Enter | [Action if applicable] |
| Space | [Action if applicable] |
| Escape | [Action if applicable] |
| Arrow Keys | [Action if applicable] |

### Screen Reader Support

**Announcements:**
- Component identifies as "[role]" to screen readers
- Label is announced as "[label content]"
- State changes announce "[announcement]"

**NVDA/JAWS:**
- [Specific behavior]

**VoiceOver:**
- [Specific behavior]

### Focus Management

- Component receives focus when: [conditions]
- Focus indicator: [description of visual focus state]
- Focus is trapped when: [if applicable, e.g., in modal]
- Focus returns to: [where focus goes on close/dismiss]

### Testing

```tsx
// Example accessibility tests
import { render, screen } from '@testing-library/react';
import { ComponentName } from './ComponentName';

describe('ComponentName Accessibility', () => {
  it('has proper ARIA label', () => {
    render(<ComponentName aria-label="Test label" />);
    expect(screen.getByLabelText('Test label')).toBeInTheDocument();
  });

  it('announces state changes', () => {
    const { rerender } = render(<ComponentName />);
    // Test ARIA live announcements
  });
});
```

---

## Design Guidelines

### When to Use

Use [ComponentName] when:
- [Use case 1]
- [Use case 2]
- [Use case 3]

### When Not to Use

Avoid [ComponentName] when:
- [Anti-pattern 1] - Use [AlternativeComponent] instead
- [Anti-pattern 2] - Use [AlternativeApproach] instead

### Best Practices

✅ **Do:**
- [Best practice 1]
- [Best practice 2]
- [Best practice 3]

❌ **Don't:**
- [Anti-pattern 1]
- [Anti-pattern 2]
- [Anti-pattern 3]

### Visual Specifications

**Spacing:**
- Padding: [value]
- Margin: [value]
- Gap between elements: [value]

**Sizing:**
- Minimum height: [value]
- Minimum width: [value]
- Touch target size: 44x44px (WCAG)

**Typography:**
- Font size: [value]
- Font weight: [value]
- Line height: [value]

**Colors:**
- Default state: [color token]
- Hover state: [color token]
- Active state: [color token]
- Disabled state: [color token]

### Responsive Behavior

**Mobile (< 768px):**
- [Mobile-specific behavior]

**Tablet (768px - 1024px):**
- [Tablet-specific behavior]

**Desktop (> 1024px):**
- [Desktop-specific behavior]

### Dark Theme

- Component adapts automatically to dark theme
- Uses PatternFly color tokens for theme compatibility
- [Any dark-theme-specific considerations]

---

## Variations

### [Variation Name]

**Description:** [What makes this variation different]

**Use Case:** [When to use this variation]

**Example:**
```tsx
<ComponentName [variation-props]>
  Variation content
</ComponentName>
```

---

## Component Composition

[ComponentName] works well with these PatternFly components:

**Common Patterns:**

### With [RelatedComponent1]
```tsx
<RelatedComponent1>
  <ComponentName />
</RelatedComponent1>
```

### With [RelatedComponent2]
```tsx
<ComponentName>
  <RelatedComponent2 />
</ComponentName>
```

---

## Related Components

- **[Component1]**: [When to use instead - more specific use case]
- **[Component2]**: [When to use instead - different context]
- **[Component3]**: [When to use together - complementary]

**Comparison:**

| Feature | [ComponentName] | [AlternativeComponent] |
|---------|----------------|----------------------|
| [Feature1] | [Capability] | [Capability] |
| [Feature2] | [Capability] | [Capability] |
| Best for | [Use case] | [Use case] |

---

## TypeScript

### Component Props Type

```tsx
interface ComponentNameProps extends React.HTMLProps<HTMLDivElement> {
  variant?: 'default' | 'primary' | 'secondary';
  isDisabled?: boolean;
  children?: React.ReactNode;
  // ... other props
}
```

### Usage with TypeScript

```tsx
import React from 'react';
import { ComponentName, ComponentNameProps } from '@patternfly/react-core';

// Type-safe wrapper
const CustomComponent: React.FC<ComponentNameProps> = (props) => (
  <ComponentName {...props} />
);

// With custom types
type CustomVariant = 'custom1' | 'custom2';

interface CustomProps extends Omit<ComponentNameProps, 'variant'> {
  variant?: CustomVariant;
}
```

---

## Styling and Customization

### CSS Variables

```css
/* Available CSS custom properties */
--pf-c-component-name--BackgroundColor
--pf-c-component-name--Color
--pf-c-component-name--Padding
/* ... other variables */
```

### Custom Styling

```tsx
// Using className
<ComponentName className="custom-class">
  Content
</ComponentName>

// Using style prop
<ComponentName style={{ backgroundColor: 'var(--pf-global-primary-color-100)' }}>
  Content
</ComponentName>
```

**Note:** Prefer CSS custom properties over inline styles for theme compatibility

---

## Testing

### Unit Testing

```tsx
import { render, screen, fireEvent } from '@testing-library/react';
import { ComponentName } from './ComponentName';

describe('ComponentName', () => {
  it('renders with default props', () => {
    render(<ComponentName>Test</ComponentName>);
    expect(screen.getByText('Test')).toBeInTheDocument();
  });

  it('applies variant classes', () => {
    render(<ComponentName variant="primary">Test</ComponentName>);
    const element = screen.getByText('Test');
    expect(element).toHaveClass('pf-m-primary');
  });

  it('handles disabled state', () => {
    render(<ComponentName isDisabled>Test</ComponentName>);
    const element = screen.getByText('Test');
    expect(element).toHaveAttribute('aria-disabled', 'true');
  });
});
```

### Integration Testing

```tsx
// Testing with form submission
it('integrates with form', () => {
  const handleSubmit = jest.fn();
  render(
    <form onSubmit={handleSubmit}>
      <ComponentName name="test" />
      <button type="submit">Submit</button>
    </form>
  );

  fireEvent.click(screen.getByText('Submit'));
  expect(handleSubmit).toHaveBeenCalled();
});
```

---

## Performance Considerations

- [Any performance notes, e.g., "Component is memoized"]
- [Re-render behavior]
- [Large list handling if applicable]

---

## Browser Support

Supports all browsers in PatternFly's support matrix:
- Chrome (latest)
- Firefox (latest)
- Safari (latest)
- Edge (latest)

---

## Changelog

**Version [X.X.X]** (YYYY-MM-DD)
- Initial release
- [Feature 1]
- [Feature 2]

---

## Resources

- **GitHub Source:** [link to component source]
- **Design Specs:** [link to design file if available]
- **PatternFly Guidelines:** https://www.patternfly.org/components/[component-name]
- **React Component Docs:** https://www.patternfly.org/components/[component-name]/react
- **Accessibility Guidelines:** https://www.patternfly.org/accessibility/accessibility-fundamentals
```

## Generation Checklist

Ensure the generated documentation includes:

### Required Sections
- [ ] Overview with clear description
- [ ] Installation and import instructions
- [ ] Basic usage example
- [ ] Complete props table
- [ ] Multiple examples covering common use cases
- [ ] Accessibility documentation (ARIA, keyboard, screen reader)
- [ ] Design guidelines (when to use, best practices)
- [ ] Related components section
- [ ] TypeScript types

### Quality Checks
- [ ] All props extracted from TypeScript interfaces
- [ ] JSDoc comments incorporated into descriptions
- [ ] Code examples are syntactically correct
- [ ] Accessibility section is complete
- [ ] Design guidelines are practical
- [ ] Related components accurately identified
- [ ] Examples cover all major variants

### PatternFly Standards
- [ ] Follows PatternFly documentation structure
- [ ] Uses PatternFly terminology
- [ ] References PatternFly design tokens
- [ ] Links to relevant PatternFly resources
- [ ] Includes accessibility requirements
- [ ] Shows responsive behavior

## Critical Requirements

✅ **DO:**
- Extract all information from actual code
- Generate working, tested examples
- Include comprehensive accessibility documentation
- Provide practical design guidelines
- Reference PatternFly patterns and tokens
- Create examples for all variants
- Include TypeScript type definitions

❌ **DON'T:**
- Make up prop descriptions without JSDoc
- Skip accessibility documentation
- Provide untested code examples
- Ignore PatternFly conventions
- Skip design guidelines
- Forget responsive behavior
- Omit TypeScript types

## Output

Generate complete, production-ready documentation following PatternFly standards.
