---
description: Generate comprehensive test suites for PatternFly components with full coverage
---

# Comprehensive Test Suite Generator

You are generating complete, production-ready test suites for PatternFly React components.

## Input
The user will provide:
- A component file path to generate tests for
- A component name to locate and test
- Specific testing requirements (accessibility, interactions, etc.)
- Existing test file to extend

## Your Task

### Phase 1: Component Analysis

1. **Read and Analyze Component**
   - Read the component source file
   - Extract TypeScript interfaces and prop types
   - Identify all props, defaults, and required props
   - Map all component variants and states
   - List all interactive elements
   - Note conditional rendering logic
   - Identify child components and composition patterns

2. **Extract Component Metadata**
   - Component name and export type
   - PropTypes/TypeScript definitions
   - Default prop values
   - Variant options (primary, secondary, etc.)
   - State variations (disabled, loading, error, etc.)
   - Event handlers (onClick, onChange, etc.)
   - Accessibility features (ARIA attributes, roles)

3. **Identify Test Requirements**
   - Unit tests for each prop
   - Variant testing
   - State testing
   - User interaction tests
   - Accessibility tests
   - Integration tests for composition
   - Edge cases and error states
   - Visual regression (snapshots)

4. **Map Dependencies**
   - Required imports
   - Context providers needed
   - Mock requirements (APIs, modules)
   - Test utilities needed

### Phase 2: Fetch PatternFly Testing Patterns

Use `mcp__pf-mcp__usePatternFlyDocs` to:
- Get PatternFly testing guidelines
- Review component-specific testing examples
- Fetch accessibility requirements for component type
- Find similar component test patterns
- Get best practices for the component category

### Phase 3: Generate Comprehensive Test Suite

Create a complete test file with these sections:

#### Test File Structure

```tsx
/**
 * Comprehensive test suite for [ComponentName]
 *
 * Coverage:
 * - ✅ Unit tests for all props
 * - ✅ Variant rendering
 * - ✅ State management
 * - ✅ User interactions
 * - ✅ Accessibility (ARIA, keyboard, screen reader)
 * - ✅ Component composition
 * - ✅ Edge cases and error handling
 * - ✅ Visual regression (snapshots)
 */

import React from 'react';
import { render, screen, within, waitFor } from '@testing-library/react';
import userEvent from '@testing-library/user-event';
import { [ComponentName] } from '@patternfly/react-core';

describe('[ComponentName]', () => {
  // Tests organized by category
});
```

#### 1. Basic Rendering Tests

```tsx
describe('rendering', () => {
  it('renders without crashing', () => {
    const { container } = render(<ComponentName>Content</ComponentName>);
    expect(container.firstChild).toBeInTheDocument();
  });

  it('renders children correctly', () => {
    render(<ComponentName>Test Content</ComponentName>);
    expect(screen.getByText('Test Content')).toBeInTheDocument();
  });

  it('applies custom className', () => {
    const { container } = render(
      <ComponentName className="custom-class">Content</ComponentName>
    );
    expect(container.firstChild).toHaveClass('custom-class');
  });

  it('forwards ref correctly', () => {
    const ref = React.createRef<HTMLDivElement>();
    render(<ComponentName ref={ref}>Content</ComponentName>);
    expect(ref.current).toBeInstanceOf(HTMLDivElement);
  });

  it('spreads additional props to DOM element', () => {
    render(<ComponentName data-testid="custom-id">Content</ComponentName>);
    expect(screen.getByTestId('custom-id')).toBeInTheDocument();
  });

  it('renders with default props', () => {
    const { container } = render(<ComponentName>Content</ComponentName>);
    expect(container.firstChild).toMatchSnapshot();
  });
});
```

#### 2. Props Testing

```tsx
describe('props', () => {
  describe('variant prop', () => {
    const variants = ['default', 'primary', 'secondary', 'tertiary'];

    variants.forEach(variant => {
      it(`renders ${variant} variant correctly`, () => {
        render(<ComponentName variant={variant}>Content</ComponentName>);
        const element = screen.getByText('Content');
        expect(element).toHaveClass(`pf-m-${variant}`);
      });
    });

    it('uses default variant when not specified', () => {
      render(<ComponentName>Content</ComponentName>);
      const element = screen.getByText('Content');
      expect(element).toHaveClass('pf-m-default');
    });
  });

  describe('isDisabled prop', () => {
    it('renders enabled state by default', () => {
      render(<ComponentName>Content</ComponentName>);
      const element = screen.getByText('Content');
      expect(element).not.toHaveAttribute('disabled');
      expect(element).not.toHaveAttribute('aria-disabled');
    });

    it('applies disabled attribute when isDisabled is true', () => {
      render(<ComponentName isDisabled>Content</ComponentName>);
      const element = screen.getByText('Content');
      expect(element).toHaveAttribute('aria-disabled', 'true');
    });

    it('prevents interaction when disabled', async () => {
      const user = userEvent.setup();
      const onClick = jest.fn();

      render(<ComponentName isDisabled onClick={onClick}>Click</ComponentName>);
      const element = screen.getByText('Click');

      await user.click(element);
      expect(onClick).not.toHaveBeenCalled();
    });
  });

  describe('size prop', () => {
    const sizes = ['sm', 'md', 'lg', 'xl'];

    sizes.forEach(size => {
      it(`renders ${size} size correctly`, () => {
        render(<ComponentName size={size}>Content</ComponentName>);
        const element = screen.getByText('Content');
        expect(element).toHaveClass(`pf-m-${size}`);
      });
    });
  });

  describe('icon prop', () => {
    const TestIcon = () => <span data-testid="test-icon">Icon</span>;

    it('renders without icon by default', () => {
      render(<ComponentName>Content</ComponentName>);
      expect(screen.queryByTestId('test-icon')).not.toBeInTheDocument();
    });

    it('renders icon when provided', () => {
      render(<ComponentName icon={<TestIcon />}>Content</ComponentName>);
      expect(screen.getByTestId('test-icon')).toBeInTheDocument();
    });

    it('positions icon correctly', () => {
      render(<ComponentName icon={<TestIcon />}>Content</ComponentName>);
      const icon = screen.getByTestId('test-icon');
      const content = screen.getByText('Content');
      // Icon should come before content in DOM
      expect(icon.compareDocumentPosition(content)).toBe(
        Node.DOCUMENT_POSITION_FOLLOWING
      );
    });
  });
});
```

#### 3. Variant Testing

```tsx
describe('variants', () => {
  it('renders all variants with correct styling', () => {
    const variants = ['primary', 'secondary', 'tertiary', 'danger', 'warning'];

    variants.forEach(variant => {
      const { container } = render(
        <ComponentName variant={variant}>Test</ComponentName>
      );

      const element = container.firstChild;
      expect(element).toHaveClass(`pf-m-${variant}`);
      expect(element).toMatchSnapshot(`${variant}-variant`);
    });
  });

  it('combines variant with other modifiers', () => {
    render(
      <ComponentName variant="primary" isDisabled>
        Content
      </ComponentName>
    );

    const element = screen.getByText('Content');
    expect(element).toHaveClass('pf-m-primary');
    expect(element).toHaveAttribute('aria-disabled', 'true');
  });
});
```

#### 4. State Testing

```tsx
describe('states', () => {
  describe('disabled state', () => {
    it('applies disabled styling', () => {
      render(<ComponentName isDisabled>Disabled</ComponentName>);
      const element = screen.getByText('Disabled');
      expect(element).toHaveClass('pf-m-disabled');
      expect(element).toMatchSnapshot('disabled-state');
    });

    it('is not focusable when disabled', () => {
      render(<ComponentName isDisabled>Content</ComponentName>);
      const element = screen.getByText('Content');
      expect(element).toHaveAttribute('tabindex', '-1');
    });
  });

  describe('loading state', () => {
    it('shows loading indicator when isLoading is true', () => {
      render(<ComponentName isLoading>Content</ComponentName>);
      expect(screen.getByRole('progressbar')).toBeInTheDocument();
    });

    it('hides content during loading', () => {
      render(<ComponentName isLoading>Content</ComponentName>);
      const content = screen.queryByText('Content');
      expect(content).toHaveAttribute('aria-hidden', 'true');
    });

    it('announces loading to screen readers', () => {
      render(<ComponentName isLoading>Content</ComponentName>);
      const loader = screen.getByRole('progressbar');
      expect(loader).toHaveAttribute('aria-label', 'Loading');
    });
  });

  describe('error state', () => {
    it('displays error message when hasError is true', () => {
      render(
        <ComponentName hasError errorMessage="Error occurred">
          Content
        </ComponentName>
      );
      expect(screen.getByText('Error occurred')).toBeInTheDocument();
    });

    it('applies error styling', () => {
      render(<ComponentName hasError>Content</ComponentName>);
      const element = screen.getByText('Content');
      expect(element).toHaveClass('pf-m-error');
    });
  });

  describe('selected state', () => {
    it('applies selected styling when isSelected is true', () => {
      render(<ComponentName isSelected>Selected</ComponentName>);
      const element = screen.getByText('Selected');
      expect(element).toHaveClass('pf-m-selected');
      expect(element).toHaveAttribute('aria-selected', 'true');
    });
  });
});
```

#### 5. User Interaction Tests

```tsx
describe('user interactions', () => {
  describe('click interactions', () => {
    it('calls onClick handler when clicked', async () => {
      const user = userEvent.setup();
      const onClick = jest.fn();

      render(<ComponentName onClick={onClick}>Click me</ComponentName>);
      const element = screen.getByText('Click me');

      await user.click(element);
      expect(onClick).toHaveBeenCalledTimes(1);
    });

    it('passes event object to onClick handler', async () => {
      const user = userEvent.setup();
      const onClick = jest.fn();

      render(<ComponentName onClick={onClick}>Click me</ComponentName>);
      await user.click(screen.getByText('Click me'));

      expect(onClick).toHaveBeenCalledWith(
        expect.objectContaining({
          type: 'click',
        })
      );
    });

    it('does not call onClick when disabled', async () => {
      const user = userEvent.setup();
      const onClick = jest.fn();

      render(
        <ComponentName onClick={onClick} isDisabled>
          Click me
        </ComponentName>
      );

      await user.click(screen.getByText('Click me'));
      expect(onClick).not.toHaveBeenCalled();
    });
  });

  describe('keyboard interactions', () => {
    it('responds to Enter key press', async () => {
      const user = userEvent.setup();
      const onAction = jest.fn();

      render(<ComponentName onAction={onAction}>Press Enter</ComponentName>);
      const element = screen.getByText('Press Enter');

      element.focus();
      await user.keyboard('{Enter}');

      expect(onAction).toHaveBeenCalledTimes(1);
    });

    it('responds to Space key press', async () => {
      const user = userEvent.setup();
      const onAction = jest.fn();

      render(<ComponentName onAction={onAction}>Press Space</ComponentName>);
      const element = screen.getByText('Press Space');

      element.focus();
      await user.keyboard(' ');

      expect(onAction).toHaveBeenCalledTimes(1);
    });

    it('closes on Escape key press', async () => {
      const user = userEvent.setup();
      const onClose = jest.fn();

      render(<ComponentName onClose={onClose} isOpen>Content</ComponentName>);
      const element = screen.getByText('Content');

      element.focus();
      await user.keyboard('{Escape}');

      expect(onClose).toHaveBeenCalledTimes(1);
    });

    it('navigates with arrow keys', async () => {
      const user = userEvent.setup();

      render(
        <ComponentName>
          <ComponentItem>Item 1</ComponentItem>
          <ComponentItem>Item 2</ComponentItem>
          <ComponentItem>Item 3</ComponentItem>
        </ComponentName>
      );

      const firstItem = screen.getByText('Item 1');
      firstItem.focus();

      await user.keyboard('{ArrowDown}');
      expect(screen.getByText('Item 2')).toHaveFocus();

      await user.keyboard('{ArrowDown}');
      expect(screen.getByText('Item 3')).toHaveFocus();

      await user.keyboard('{ArrowUp}');
      expect(screen.getByText('Item 2')).toHaveFocus();
    });
  });

  describe('focus management', () => {
    it('receives focus when tabbed to', async () => {
      const user = userEvent.setup();

      render(
        <>
          <button>Before</button>
          <ComponentName>Component</ComponentName>
          <button>After</button>
        </>
      );

      const beforeButton = screen.getByText('Before');
      beforeButton.focus();

      await user.tab();
      expect(screen.getByText('Component')).toHaveFocus();

      await user.tab();
      expect(screen.getByText('After')).toHaveFocus();
    });

    it('shows focus indicator when focused', async () => {
      const user = userEvent.setup();

      render(<ComponentName>Content</ComponentName>);
      const element = screen.getByText('Content');

      await user.tab();
      element.focus();

      expect(element).toHaveClass('pf-m-focus');
    });

    it('traps focus when modal is open', async () => {
      const user = userEvent.setup();

      render(
        <ComponentName isOpen>
          <button>First</button>
          <button>Second</button>
        </ComponentName>
      );

      const first = screen.getByText('First');
      const second = screen.getByText('Second');

      first.focus();
      expect(first).toHaveFocus();

      await user.tab();
      expect(second).toHaveFocus();

      await user.tab();
      expect(first).toHaveFocus(); // Focus wraps
    });
  });

  describe('form interactions', () => {
    it('updates value on user input', async () => {
      const user = userEvent.setup();
      const onChange = jest.fn();

      render(<ComponentName onChange={onChange} />);
      const input = screen.getByRole('textbox');

      await user.type(input, 'test');

      expect(onChange).toHaveBeenCalled();
      expect(input).toHaveValue('test');
    });

    it('submits form on Enter', async () => {
      const user = userEvent.setup();
      const onSubmit = jest.fn(e => e.preventDefault());

      render(
        <form onSubmit={onSubmit}>
          <ComponentName name="field" />
          <button type="submit">Submit</button>
        </form>
      );

      const input = screen.getByRole('textbox');
      await user.type(input, 'test{Enter}');

      expect(onSubmit).toHaveBeenCalledTimes(1);
    });
  });

  describe('hover interactions', () => {
    it('applies hover state on mouse over', async () => {
      const user = userEvent.setup();

      render(<ComponentName>Hover me</ComponentName>);
      const element = screen.getByText('Hover me');

      await user.hover(element);
      expect(element).toHaveClass('pf-m-hover');

      await user.unhover(element);
      expect(element).not.toHaveClass('pf-m-hover');
    });

    it('shows tooltip on hover', async () => {
      const user = userEvent.setup();

      render(<ComponentName tooltip="Helpful text">Content</ComponentName>);
      const element = screen.getByText('Content');

      await user.hover(element);
      const tooltip = await screen.findByRole('tooltip');

      expect(tooltip).toHaveTextContent('Helpful text');
    });
  });
});
```

#### 6. Accessibility Tests

```tsx
describe('accessibility', () => {
  describe('ARIA attributes', () => {
    it('has proper role', () => {
      render(<ComponentName>Content</ComponentName>);
      const element = screen.getByRole('button'); // or appropriate role
      expect(element).toBeInTheDocument();
    });

    it('has accessible name', () => {
      render(<ComponentName aria-label="Accessible name">Content</ComponentName>);
      const element = screen.getByRole('button', { name: 'Accessible name' });
      expect(element).toBeInTheDocument();
    });

    it('uses aria-labelledby when label is provided', () => {
      render(
        <>
          <h2 id="label-id">Label</h2>
          <ComponentName aria-labelledby="label-id">Content</ComponentName>
        </>
      );

      const element = screen.getByLabelText('Label');
      expect(element).toHaveAttribute('aria-labelledby', 'label-id');
    });

    it('has aria-describedby for additional context', () => {
      render(
        <>
          <ComponentName aria-describedby="desc-id">Content</ComponentName>
          <div id="desc-id">Description text</div>
        </>
      );

      const element = screen.getByText('Content');
      expect(element).toHaveAttribute('aria-describedby', 'desc-id');
    });

    it('updates aria-expanded on toggle', async () => {
      const user = userEvent.setup();

      render(<ComponentName>Toggle</ComponentName>);
      const toggle = screen.getByRole('button', { name: 'Toggle' });

      expect(toggle).toHaveAttribute('aria-expanded', 'false');

      await user.click(toggle);
      expect(toggle).toHaveAttribute('aria-expanded', 'true');

      await user.click(toggle);
      expect(toggle).toHaveAttribute('aria-expanded', 'false');
    });

    it('sets aria-disabled instead of disabled attribute', () => {
      render(<ComponentName isDisabled>Disabled</ComponentName>);
      const element = screen.getByText('Disabled');

      expect(element).toHaveAttribute('aria-disabled', 'true');
      expect(element).not.toHaveAttribute('disabled');
    });

    it('has aria-live region for dynamic updates', async () => {
      const { rerender } = render(<ComponentName status="idle" />);

      const liveRegion = screen.getByRole('status');
      expect(liveRegion).toHaveAttribute('aria-live', 'polite');

      rerender(<ComponentName status="success" />);
      expect(liveRegion).toHaveTextContent('Success');
    });

    it('uses aria-current for current item', () => {
      render(
        <ComponentName>
          <ComponentItem isCurrent>Current</ComponentItem>
          <ComponentItem>Other</ComponentItem>
        </ComponentName>
      );

      const currentItem = screen.getByText('Current');
      expect(currentItem).toHaveAttribute('aria-current', 'true');
    });
  });

  describe('keyboard navigation', () => {
    it('is keyboard accessible', async () => {
      const user = userEvent.setup();
      const onAction = jest.fn();

      render(<ComponentName onAction={onAction}>Content</ComponentName>);
      const element = screen.getByText('Content');

      await user.tab();
      expect(element).toHaveFocus();

      await user.keyboard('{Enter}');
      expect(onAction).toHaveBeenCalled();
    });

    it('follows proper tab order', async () => {
      const user = userEvent.setup();

      render(
        <ComponentName>
          <button>First</button>
          <button>Second</button>
          <button>Third</button>
        </ComponentName>
      );

      await user.tab();
      expect(screen.getByText('First')).toHaveFocus();

      await user.tab();
      expect(screen.getByText('Second')).toHaveFocus();

      await user.tab();
      expect(screen.getByText('Third')).toHaveFocus();
    });

    it('skips disabled elements in tab order', async () => {
      const user = userEvent.setup();

      render(
        <ComponentName>
          <button>First</button>
          <button disabled>Disabled</button>
          <button>Third</button>
        </ComponentName>
      );

      await user.tab();
      expect(screen.getByText('First')).toHaveFocus();

      await user.tab();
      expect(screen.getByText('Third')).toHaveFocus();
    });

    it('supports roving tabindex for composite widgets', async () => {
      const user = userEvent.setup();

      render(
        <ComponentName>
          <ComponentItem>Item 1</ComponentItem>
          <ComponentItem>Item 2</ComponentItem>
          <ComponentItem>Item 3</ComponentItem>
        </ComponentName>
      );

      // First item is tabbable
      const item1 = screen.getByText('Item 1');
      expect(item1).toHaveAttribute('tabindex', '0');

      // Other items not tabbable
      expect(screen.getByText('Item 2')).toHaveAttribute('tabindex', '-1');
      expect(screen.getByText('Item 3')).toHaveAttribute('tabindex', '-1');

      // Navigate with arrows
      item1.focus();
      await user.keyboard('{ArrowDown}');

      // Now item 2 is tabbable
      expect(screen.getByText('Item 2')).toHaveAttribute('tabindex', '0');
      expect(item1).toHaveAttribute('tabindex', '-1');
    });
  });

  describe('screen reader support', () => {
    it('provides meaningful labels for screen readers', () => {
      render(
        <ComponentName aria-label="Close dialog">
          <span aria-hidden="true">×</span>
        </ComponentName>
      );

      const button = screen.getByRole('button', { name: 'Close dialog' });
      expect(button).toBeInTheDocument();
    });

    it('announces status changes to screen readers', async () => {
      const { rerender } = render(<ComponentName status="loading" />);

      const status = screen.getByRole('status');
      expect(status).toHaveAttribute('aria-live', 'polite');
      expect(status).toHaveTextContent('Loading');

      rerender(<ComponentName status="success" />);
      expect(status).toHaveTextContent('Success');
    });

    it('hides decorative elements from screen readers', () => {
      render(
        <ComponentName>
          <span aria-hidden="true" className="decorative-icon">→</span>
          <span>Visible content</span>
        </ComponentName>
      );

      const decorative = document.querySelector('.decorative-icon');
      expect(decorative).toHaveAttribute('aria-hidden', 'true');
    });

    it('provides context for icon-only buttons', () => {
      const IconComponent = () => <span>🔍</span>;

      render(
        <ComponentName aria-label="Search">
          <IconComponent />
        </ComponentName>
      );

      const button = screen.getByRole('button', { name: 'Search' });
      expect(button).toBeInTheDocument();
    });
  });

  describe('focus indicators', () => {
    it('shows visible focus indicator', async () => {
      const user = userEvent.setup();

      render(<ComponentName>Content</ComponentName>);
      const element = screen.getByText('Content');

      await user.tab();
      element.focus();

      // Verify focus visible class or style
      expect(element).toHaveClass('pf-m-focus');
    });

    it('maintains focus visibility on interaction', async () => {
      const user = userEvent.setup();

      render(<ComponentName>Click me</ComponentName>);
      const element = screen.getByText('Click me');

      element.focus();
      await user.click(element);

      expect(document.activeElement).toBe(element);
    });
  });

  describe('semantic HTML', () => {
    it('uses button element for clickable actions', () => {
      render(<ComponentName onClick={() => {}}>Action</ComponentName>);
      const button = screen.getByRole('button');
      expect(button.tagName).toBe('BUTTON');
    });

    it('uses proper heading hierarchy', () => {
      render(
        <ComponentName>
          <h2>Section Title</h2>
          <h3>Subsection</h3>
        </ComponentName>
      );

      expect(screen.getByRole('heading', { level: 2, name: 'Section Title' }))
        .toBeInTheDocument();
      expect(screen.getByRole('heading', { level: 3, name: 'Subsection' }))
        .toBeInTheDocument();
    });

    it('uses list elements for lists', () => {
      render(
        <ComponentName>
          <ul>
            <li>Item 1</li>
            <li>Item 2</li>
          </ul>
        </ComponentName>
      );

      const list = screen.getByRole('list');
      const items = screen.getAllByRole('listitem');

      expect(list).toBeInTheDocument();
      expect(items).toHaveLength(2);
    });
  });
});
```

#### 7. Component Composition Tests

```tsx
describe('component composition', () => {
  it('renders with child components', () => {
    render(
      <ComponentName>
        <ComponentHeader>Header</ComponentHeader>
        <ComponentBody>Body content</ComponentBody>
        <ComponentFooter>Footer</ComponentFooter>
      </ComponentName>
    );

    expect(screen.getByText('Header')).toBeInTheDocument();
    expect(screen.getByText('Body content')).toBeInTheDocument();
    expect(screen.getByText('Footer')).toBeInTheDocument();
  });

  it('maintains correct DOM structure with composition', () => {
    const { container } = render(
      <ComponentName>
        <ComponentHeader>Header</ComponentHeader>
        <ComponentBody>Body</ComponentBody>
      </ComponentName>
    );

    const header = screen.getByText('Header');
    const body = screen.getByText('Body');

    // Header should come before body
    expect(header.compareDocumentPosition(body)).toBe(
      Node.DOCUMENT_POSITION_FOLLOWING
    );

    expect(container.firstChild).toMatchSnapshot('composition-structure');
  });

  it('passes context to child components', () => {
    render(
      <ComponentName variant="primary">
        <ComponentChild>Child</ComponentChild>
      </ComponentName>
    );

    const child = screen.getByText('Child');
    // Child should inherit variant from parent context
    expect(child).toHaveClass('pf-m-primary');
  });

  it('handles deeply nested composition', () => {
    render(
      <ComponentName>
        <ComponentSection>
          <ComponentHeader>Nested Header</ComponentHeader>
          <ComponentBody>
            <ComponentItem>Item 1</ComponentItem>
            <ComponentItem>Item 2</ComponentItem>
          </ComponentBody>
        </ComponentSection>
      </ComponentName>
    );

    expect(screen.getByText('Nested Header')).toBeInTheDocument();
    expect(screen.getByText('Item 1')).toBeInTheDocument();
    expect(screen.getByText('Item 2')).toBeInTheDocument();
  });
});
```

#### 8. Edge Cases and Error Handling

```tsx
describe('edge cases and error handling', () => {
  it('handles empty children gracefully', () => {
    const { container } = render(<ComponentName />);
    expect(container.firstChild).toBeInTheDocument();
  });

  it('handles null children', () => {
    const { container } = render(<ComponentName>{null}</ComponentName>);
    expect(container.firstChild).toBeInTheDocument();
  });

  it('handles undefined props', () => {
    const { container } = render(
      <ComponentName variant={undefined}>Content</ComponentName>
    );
    expect(container.firstChild).toBeInTheDocument();
  });

  it('validates required props', () => {
    // Suppress console.error for this test
    const spy = jest.spyOn(console, 'error').mockImplementation(() => {});

    render(<ComponentName />); // Missing required prop

    expect(spy).toHaveBeenCalledWith(
      expect.stringContaining('required prop')
    );

    spy.mockRestore();
  });

  it('handles very long text content', () => {
    const longText = 'a'.repeat(10000);
    render(<ComponentName>{longText}</ComponentName>);

    const element = screen.getByText(longText);
    expect(element).toBeInTheDocument();
  });

  it('handles special characters in content', () => {
    const specialContent = '<script>alert("xss")</script>';
    render(<ComponentName>{specialContent}</ComponentName>);

    expect(screen.getByText(specialContent)).toBeInTheDocument();
    // Ensure it's escaped, not executed
  });

  it('handles rapid state changes', async () => {
    const user = userEvent.setup();
    const { rerender } = render(<ComponentName isOpen={false} />);

    // Rapidly toggle state
    for (let i = 0; i < 10; i++) {
      rerender(<ComponentName isOpen={i % 2 === 0} />);
    }

    // Should not crash
    expect(screen.getByText('Content')).toBeInTheDocument();
  });

  it('cleans up on unmount', () => {
    const { unmount } = render(<ComponentName />);

    unmount();

    // Verify event listeners removed, timers cleared, etc.
    expect(document.body.querySelector('.pf-c-component')).not.toBeInTheDocument();
  });
});
```

#### 9. Async Operations Tests

```tsx
describe('async operations', () => {
  beforeEach(() => {
    jest.clearAllMocks();
  });

  it('loads data asynchronously', async () => {
    const mockFetch = jest.fn(() =>
      Promise.resolve({ data: 'Loaded data' })
    );

    render(<ComponentName onLoad={mockFetch} />);

    expect(screen.getByText('Loading...')).toBeInTheDocument();

    const data = await screen.findByText('Loaded data');
    expect(data).toBeInTheDocument();
    expect(mockFetch).toHaveBeenCalledTimes(1);
  });

  it('handles loading errors', async () => {
    const mockFetch = jest.fn(() =>
      Promise.reject(new Error('Failed to load'))
    );

    render(<ComponentName onLoad={mockFetch} />);

    const error = await screen.findByText(/failed to load/i);
    expect(error).toBeInTheDocument();
  });

  it('shows loading state during async operation', async () => {
    let resolvePromise;
    const promise = new Promise(resolve => {
      resolvePromise = resolve;
    });

    render(<ComponentName loadData={() => promise} />);

    expect(screen.getByRole('progressbar')).toBeInTheDocument();

    resolvePromise({ data: 'Complete' });
    await screen.findByText('Complete');

    expect(screen.queryByRole('progressbar')).not.toBeInTheDocument();
  });

  it('cancels pending requests on unmount', async () => {
    const abortSpy = jest.fn();
    const mockFetch = jest.fn(() => ({
      promise: new Promise(() => {}), // Never resolves
      abort: abortSpy,
    }));

    const { unmount } = render(<ComponentName onLoad={mockFetch} />);

    unmount();

    expect(abortSpy).toHaveBeenCalled();
  });

  it('handles concurrent requests correctly', async () => {
    const mockFetch = jest
      .fn()
      .mockResolvedValueOnce({ data: 'First' })
      .mockResolvedValueOnce({ data: 'Second' });

    const { rerender } = render(<ComponentName query="first" />);

    rerender(<ComponentName query="second" />);

    // Should only show the latest result
    const result = await screen.findByText('Second');
    expect(result).toBeInTheDocument();
    expect(screen.queryByText('First')).not.toBeInTheDocument();
  });
});
```

#### 10. Visual Regression (Snapshot) Tests

```tsx
describe('visual regression', () => {
  it('matches snapshot for default state', () => {
    const { container } = render(<ComponentName>Default</ComponentName>);
    expect(container.firstChild).toMatchSnapshot();
  });

  describe('variant snapshots', () => {
    const variants = ['primary', 'secondary', 'tertiary', 'danger'];

    variants.forEach(variant => {
      it(`matches snapshot for ${variant} variant`, () => {
        const { container } = render(
          <ComponentName variant={variant}>Content</ComponentName>
        );
        expect(container.firstChild).toMatchSnapshot(`variant-${variant}`);
      });
    });
  });

  describe('state snapshots', () => {
    it('matches snapshot for disabled state', () => {
      const { container } = render(
        <ComponentName isDisabled>Disabled</ComponentName>
      );
      expect(container.firstChild).toMatchSnapshot('state-disabled');
    });

    it('matches snapshot for loading state', () => {
      const { container } = render(
        <ComponentName isLoading>Loading</ComponentName>
      );
      expect(container.firstChild).toMatchSnapshot('state-loading');
    });

    it('matches snapshot for error state', () => {
      const { container } = render(
        <ComponentName hasError errorMessage="Error">Content</ComponentName>
      );
      expect(container.firstChild).toMatchSnapshot('state-error');
    });
  });

  describe('size snapshots', () => {
    ['sm', 'md', 'lg', 'xl'].forEach(size => {
      it(`matches snapshot for ${size} size`, () => {
        const { container } = render(
          <ComponentName size={size}>Content</ComponentName>
        );
        expect(container.firstChild).toMatchSnapshot(`size-${size}`);
      });
    });
  });

  it('matches snapshot with all props', () => {
    const { container } = render(
      <ComponentName
        variant="primary"
        size="lg"
        icon={<span>Icon</span>}
        className="custom"
        aria-label="Full props"
      >
        Full props content
      </ComponentName>
    );
    expect(container.firstChild).toMatchSnapshot('all-props');
  });
});
```

### Phase 4: Generate Test Utilities and Helpers

```tsx
// test-helpers.tsx
export const defaultProps = {
  variant: 'default',
  size: 'md',
  isDisabled: false,
};

export function renderComponent(props = {}) {
  return render(<ComponentName {...defaultProps} {...props} />);
}

export function getAllVariants() {
  return ['default', 'primary', 'secondary', 'tertiary'];
}

export function getAllSizes() {
  return ['sm', 'md', 'lg', 'xl'];
}

export async function userClickElement(name: string) {
  const user = userEvent.setup();
  const element = screen.getByRole('button', { name });
  await user.click(element);
  return element;
}

export function expectElementToHaveClasses(element: HTMLElement, classes: string[]) {
  classes.forEach(className => {
    expect(element).toHaveClass(className);
  });
}
```

### Phase 5: Generate Test Documentation

```markdown
# ComponentName Test Suite

## Coverage Summary

- **Unit Tests:** ✅ All props tested
- **Variant Tests:** ✅ All variants covered
- **State Tests:** ✅ All states covered
- **Interaction Tests:** ✅ Click, keyboard, focus
- **Accessibility Tests:** ✅ ARIA, keyboard nav, screen reader
- **Composition Tests:** ✅ Child components
- **Edge Cases:** ✅ Error handling, async
- **Snapshots:** ✅ Visual regression

## Running Tests

```bash
# Run all tests
npm test ComponentName.test.tsx

# Run with coverage
npm test -- --coverage ComponentName.test.tsx

# Run in watch mode
npm test -- --watch ComponentName.test.tsx

# Update snapshots
npm test -- -u ComponentName.test.tsx
```

## Test Organization

Tests are organized into logical groups:

1. **rendering** - Basic rendering and props
2. **props** - Individual prop testing
3. **variants** - All variant options
4. **states** - Component states
5. **user interactions** - Click, keyboard, focus
6. **accessibility** - ARIA, keyboard nav, screen readers
7. **composition** - Child component integration
8. **edge cases** - Error handling, special cases
9. **async operations** - Async data loading
10. **visual regression** - Snapshot tests

## Adding New Tests

When adding functionality:

1. Add unit test for the new prop/feature
2. Add interaction test if interactive
3. Add accessibility test for a11y features
4. Add snapshot for visual changes
5. Update this documentation

## Common Test Patterns

### Testing Props
```tsx
it('renders with prop', () => {
  render(<ComponentName propName="value" />);
  expect(screen.getByText('value')).toBeInTheDocument();
});
```

### Testing Interactions
```tsx
it('handles interaction', async () => {
  const user = userEvent.setup();
  const handler = jest.fn();

  render(<ComponentName onAction={handler} />);
  await user.click(screen.getByRole('button'));

  expect(handler).toHaveBeenCalled();
});
```

### Testing Accessibility
```tsx
it('is accessible', () => {
  render(<ComponentName aria-label="Label" />);
  const element = screen.getByRole('button', { name: 'Label' });
  expect(element).toBeInTheDocument();
});
```

## Debugging Failed Tests

1. Use `screen.debug()` to see rendered output
2. Use `screen.logTestingPlaygroundURL()` for query help
3. Check component recent changes
4. Verify props are passed correctly
5. Check for async issues

See [Test Failure Analysis Guide](./TEST_FAILURES.md) for more details.
```

## Critical Requirements

✅ **DO:**
- Generate complete test coverage for all props and variants
- Use semantic queries (getByRole, getByLabelText)
- Test accessibility thoroughly (ARIA, keyboard, screen reader)
- Include user interaction tests with userEvent
- Test all component states (disabled, loading, error)
- Create focused, meaningful snapshots
- Test component composition patterns
- Handle edge cases and error states
- Provide async operation tests
- Include test utilities and helpers
- Generate runnable, working code
- Follow PatternFly testing patterns
- Organize tests logically
- Add descriptive test names

❌ **DON'T:**
- Use implementation details in queries
- Skip accessibility testing
- Use fireEvent instead of userEvent
- Create massive snapshot tests
- Forget to test error states
- Skip keyboard navigation tests
- Ignore async operations
- Test internal state directly
- Use shallow rendering
- Skip edge case testing
- Generate tests without running them
- Mix concerns in single tests
- Use non-semantic queries

## Output Format

Generate:
1. **Complete test file** with all test categories
2. **Test utilities** for common operations
3. **Test documentation** explaining organization
4. **Coverage report** showing what's tested
5. **Running instructions** for different scenarios
6. **Debugging guide** for common issues

Always provide production-ready, fully tested code that achieves comprehensive coverage.
