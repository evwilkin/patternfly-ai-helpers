---
description: Modernize snapshot tests from Enzyme to React Testing Library with semantic queries
---

# Snapshot Test Modernizer

You are helping developers modernize outdated snapshot tests to follow current React Testing Library best practices.

## Input
The user will provide:
- A test file path with snapshot tests
- A component file to generate new snapshot tests for
- Test output showing snapshot failures
- A directory to scan for snapshot tests

## Your Task

### Phase 1: Analysis of Current Snapshot Tests

1. **Read Test Files**
   - Locate and read the test file(s) provided
   - Identify all snapshot tests (`.toMatchSnapshot()` calls)
   - Find enzyme usage (`shallow`, `mount`, `wrapper`)
   - Extract existing test structure and organization

2. **Analyze Component Under Test**
   - Read the component source file
   - Extract props, variants, and states
   - Identify interactive elements
   - Note accessibility features
   - Map component structure

3. **Identify Snapshot Issues**
   - Check for enzyme dependencies
   - Look for full component tree snapshots
   - Find implementation detail queries (`.find()`, `.instance()`)
   - Identify brittle selectors (classes, IDs without semantic meaning)
   - Note missing accessibility testing

4. **Parse Failure Output** (if provided)
   - Extract which snapshots are failing
   - Identify what changed (DOM, props, styles, text)
   - Determine if changes are intentional or bugs
   - Map failures to component changes

### Phase 2: Fetch PatternFly Testing Guidelines

Use `mcp__pf-mcp__usePatternFlyDocs` to fetch:
- PatternFly testing best practices
- React Testing Library patterns for similar components
- Accessibility testing requirements
- Snapshot testing guidelines
- Migration guides from Enzyme to RTL

### Phase 3: Generate Modernized Snapshot Tests

Create modern snapshot tests following these principles:

#### 1. Replace Enzyme with React Testing Library

**Before (Enzyme):**
```tsx
import { shallow } from 'enzyme';

describe('Button', () => {
  it('matches snapshot', () => {
    const wrapper = shallow(<Button>Click me</Button>);
    expect(wrapper).toMatchSnapshot();
  });
});
```

**After (RTL):**
```tsx
import { render, screen } from '@testing-library/react';

describe('Button', () => {
  it('renders with expected structure', () => {
    const { container } = render(<Button>Click me</Button>);
    expect(container.firstChild).toMatchSnapshot();
  });
});
```

#### 2. Use Semantic Queries

**Before (Implementation Details):**
```tsx
const wrapper = shallow(<Alert />);
expect(wrapper.find('.pf-c-alert__title')).toMatchSnapshot();
```

**After (Semantic Queries):**
```tsx
render(<Alert title="Warning" variant="warning" />);
const alert = screen.getByRole('alert');
expect(alert).toMatchSnapshot();
```

#### 3. Create Focused Snapshots

**Before (Full Tree):**
```tsx
const wrapper = mount(
  <Page>
    <PageHeader />
    <PageSidebar />
    <PageSection>
      <Card>
        <CardTitle>Title</CardTitle>
        <CardBody>Content</CardBody>
      </Card>
    </PageSection>
  </Page>
);
expect(wrapper).toMatchSnapshot();
```

**After (Focused):**
```tsx
// Test Card separately
describe('Card', () => {
  it('renders title and body', () => {
    render(
      <Card>
        <CardTitle>Title</CardTitle>
        <CardBody>Content</CardBody>
      </Card>
    );
    const card = screen.getByText('Title').closest('.pf-c-card');
    expect(card).toMatchSnapshot();
  });
});
```

#### 4. Add Variant Testing

```tsx
describe('Button variants', () => {
  const variants = ['primary', 'secondary', 'tertiary', 'danger', 'warning', 'link'];

  variants.forEach(variant => {
    it(`renders ${variant} variant correctly`, () => {
      render(<Button variant={variant}>Button text</Button>);
      const button = screen.getByRole('button', { name: 'Button text' });
      expect(button).toMatchSnapshot();
    });
  });
});
```

#### 5. Include Accessibility in Snapshots

```tsx
describe('Alert accessibility', () => {
  it('has proper ARIA attributes in snapshot', () => {
    render(
      <Alert
        variant="danger"
        title="Error occurred"
        aria-live="assertive"
      >
        Error message
      </Alert>
    );

    const alert = screen.getByRole('alert');
    expect(alert).toHaveAttribute('aria-live', 'assertive');
    expect(alert).toMatchSnapshot();
  });
});
```

#### 6. Test State Changes with Snapshots

```tsx
describe('Modal states', () => {
  it('snapshot when closed', () => {
    const { container } = render(<Modal isOpen={false} />);
    expect(container).toMatchSnapshot();
  });

  it('snapshot when open', () => {
    render(<Modal isOpen={true} title="Modal Title">Content</Modal>);
    const modal = screen.getByRole('dialog');
    expect(modal).toMatchSnapshot();
  });
});
```

### Phase 4: Generate Migration Report

Create a comprehensive report of the modernization:

```markdown
# Snapshot Test Modernization Report

## Component(s) Analyzed
- **Test File:** [path to test file]
- **Component File:** [path to component]
- **Date:** [YYYY-MM-DD]

---

## Summary of Changes

**Tests Modernized:** [count]
**Enzyme Tests Removed:** [count]
**New RTL Tests Added:** [count]

**Migration Status:**
- ✅ Enzyme completely removed
- ✅ All queries use semantic selectors
- ✅ Snapshots focused on relevant structure
- ✅ Accessibility attributes tested
- ✅ Variants covered

---

## Snapshot Failures Analysis

### Failures Found: [count]

#### Failure 1: [Description]

**Location:** `test-file.tsx:line`

**Why It Failed:**
[Detailed explanation of why the snapshot failed]

**What Changed:**
```diff
- <button class="pf-c-button pf-m-primary">
+ <button class="pf-c-button pf-m-primary pf-m-disabled" disabled>
    Click me
  </button>
```

**Root Cause:**
- [Explanation: e.g., "Disabled prop was added to component"]
- [Impact: e.g., "This is an intentional change for accessibility"]

**Recommendation:**
✅ Accept snapshot update - this is a valid change
❌ Fix the code - this breaks expected behavior
⚠️  Review with team - unclear if intentional

---

## Modernization Changes

### Before: Enzyme Implementation

```tsx
import { shallow, mount } from 'enzyme';
import { Button } from '@patternfly/react-core';

describe('Button', () => {
  it('matches snapshot', () => {
    const wrapper = shallow(<Button>Click me</Button>);
    expect(wrapper).toMatchSnapshot();
  });

  it('renders primary variant', () => {
    const wrapper = shallow(<Button variant="primary">Primary</Button>);
    expect(wrapper.find('.pf-m-primary')).toHaveLength(1);
    expect(wrapper).toMatchSnapshot();
  });

  it('handles click', () => {
    const onClick = jest.fn();
    const wrapper = shallow(<Button onClick={onClick}>Click</Button>);
    wrapper.find('button').simulate('click');
    expect(onClick).toHaveBeenCalled();
  });
});
```

**Issues with this approach:**
- ❌ Uses enzyme (deprecated, doesn't work with React 18+)
- ❌ Shallow rendering misses child component issues
- ❌ Queries by CSS class (implementation detail)
- ❌ Doesn't test accessibility
- ❌ simulate() doesn't trigger real events

---

### After: React Testing Library Implementation

```tsx
import { render, screen } from '@testing-library/react';
import userEvent from '@testing-library/user-event';
import { Button } from '@patternfly/react-core';

describe('Button', () => {
  it('renders with expected structure', () => {
    const { container } = render(<Button>Click me</Button>);
    const button = screen.getByRole('button', { name: 'Click me' });
    expect(button).toBeInTheDocument();
    expect(container.firstChild).toMatchSnapshot();
  });

  describe('variants', () => {
    const variants = ['primary', 'secondary', 'tertiary', 'danger'];

    variants.forEach(variant => {
      it(`renders ${variant} variant correctly`, () => {
        render(<Button variant={variant}>Button</Button>);
        const button = screen.getByRole('button', { name: 'Button' });
        expect(button).toHaveClass(`pf-m-${variant}`);
        expect(button).toMatchSnapshot();
      });
    });
  });

  it('handles user interaction', async () => {
    const user = userEvent.setup();
    const onClick = jest.fn();

    render(<Button onClick={onClick}>Click</Button>);
    const button = screen.getByRole('button', { name: 'Click' });

    await user.click(button);
    expect(onClick).toHaveBeenCalledTimes(1);
  });

  it('renders disabled state correctly', () => {
    render(<Button isDisabled>Disabled</Button>);
    const button = screen.getByRole('button', { name: 'Disabled' });

    expect(button).toBeDisabled();
    expect(button).toHaveAttribute('aria-disabled', 'true');
    expect(button).toMatchSnapshot();
  });

  it('renders with icon', () => {
    const PlusIcon = () => <span data-testid="plus-icon">+</span>;

    render(<Button icon={<PlusIcon />}>Add Item</Button>);
    const button = screen.getByRole('button', { name: 'Add Item' });

    expect(screen.getByTestId('plus-icon')).toBeInTheDocument();
    expect(button).toMatchSnapshot();
  });
});
```

**Improvements:**
- ✅ Uses React Testing Library (modern, supported)
- ✅ Full rendering with real DOM
- ✅ Semantic queries (getByRole)
- ✅ Tests accessibility attributes
- ✅ Real user interactions with userEvent
- ✅ Focused snapshots on specific elements
- ✅ Tests all variants systematically

---

## Detailed Migration Guide

### 1. Update Imports

**Remove:**
```tsx
import { shallow, mount, render } from 'enzyme';
import Adapter from '@wojtekmaj/enzyme-adapter-react-17';
```

**Add:**
```tsx
import { render, screen, waitFor } from '@testing-library/react';
import userEvent from '@testing-library/user-event';
```

### 2. Replace Enzyme Methods

| Enzyme | React Testing Library | Notes |
|--------|----------------------|-------|
| `shallow(<Component />)` | `render(<Component />)` | Use full render, not shallow |
| `wrapper.find('.class')` | `screen.getByRole('role')` | Use semantic queries |
| `wrapper.find('#id')` | `screen.getByLabelText('label')` | Prefer accessible queries |
| `wrapper.text()` | `screen.getByText('text')` | Query by visible text |
| `wrapper.prop('prop')` | `expect(element).toHaveAttribute('prop')` | Check attributes directly |
| `wrapper.setState()` | Re-render with new props | Test through props, not state |
| `wrapper.instance()` | N/A - test behavior, not implementation | Avoid instance access |
| `simulate('click')` | `await user.click(element)` | Use real events |

### 3. Query Priority (RTL Best Practices)

Use queries in this order:
1. **`getByRole`** - Most accessible, preferred
2. **`getByLabelText`** - Good for forms
3. **`getByPlaceholderText`** - Form inputs
4. **`getByText`** - Visible text content
5. **`getByDisplayValue`** - Current input value
6. **`getByAltText`** - Images
7. **`getByTitle`** - Last resort
8. **`getByTestId`** - Only when semantic queries aren't possible

**Avoid:**
- `getByClassName` - implementation detail
- `querySelector` - not recommended unless necessary

### 4. Snapshot Best Practices

**✅ DO:**
- Snapshot specific elements, not entire trees
- Use `container.firstChild` for component root
- Snapshot different variants separately
- Include accessibility attributes in snapshots
- Test state changes with before/after snapshots
- Name snapshots descriptively

**❌ DON'T:**
- Snapshot massive component trees
- Include irrelevant parent/wrapper elements
- Mix multiple concerns in one snapshot
- Snapshot third-party components
- Use snapshots as primary assertion method
- Snapshot non-deterministic data (dates, IDs)

### 5. Accessibility Snapshot Testing

Always verify accessibility in snapshots:

```tsx
describe('Accessible snapshots', () => {
  it('button has proper ARIA attributes', () => {
    render(
      <Button
        aria-label="Close dialog"
        aria-expanded={false}
      >
        X
      </Button>
    );

    const button = screen.getByRole('button', { name: 'Close dialog' });

    // Verify accessibility before snapshot
    expect(button).toHaveAttribute('aria-label', 'Close dialog');
    expect(button).toHaveAttribute('aria-expanded', 'false');

    // Snapshot includes these attributes
    expect(button).toMatchSnapshot();
  });
});
```

---

## Updated Test File

### New Test Structure

```tsx
import React from 'react';
import { render, screen, within } from '@testing-library/react';
import userEvent from '@testing-library/user-event';
import { [ComponentName] } from '@patternfly/react-core';

describe('[ComponentName]', () => {
  describe('rendering', () => {
    it('renders with default props', () => {
      const { container } = render(<ComponentName>Content</ComponentName>);
      expect(container.firstChild).toMatchSnapshot();
    });

    it('renders with all props', () => {
      render(
        <ComponentName
          variant="primary"
          isDisabled={false}
          className="custom-class"
        >
          Content
        </ComponentName>
      );

      const component = screen.getByText('Content');
      expect(component).toMatchSnapshot();
    });
  });

  describe('variants', () => {
    const variants = ['default', 'primary', 'secondary'];

    variants.forEach(variant => {
      it(`renders ${variant} variant`, () => {
        render(<ComponentName variant={variant}>Text</ComponentName>);
        const element = screen.getByText('Text');
        expect(element).toMatchSnapshot();
      });
    });
  });

  describe('states', () => {
    it('renders disabled state', () => {
      render(<ComponentName isDisabled>Disabled</ComponentName>);
      const element = screen.getByText('Disabled');
      expect(element).toMatchSnapshot();
    });

    it('renders loading state', () => {
      render(<ComponentName isLoading>Loading</ComponentName>);
      expect(screen.getByText('Loading')).toMatchSnapshot();
    });
  });

  describe('accessibility', () => {
    it('has proper ARIA attributes', () => {
      render(
        <ComponentName
          aria-label="Accessible label"
          role="region"
        >
          Content
        </ComponentName>
      );

      const region = screen.getByRole('region', { name: 'Accessible label' });
      expect(region).toMatchSnapshot();
    });
  });

  describe('interactions', () => {
    it('handles click events', async () => {
      const user = userEvent.setup();
      const onClick = jest.fn();

      render(<ComponentName onClick={onClick}>Click me</ComponentName>);
      const element = screen.getByText('Click me');

      await user.click(element);
      expect(onClick).toHaveBeenCalledTimes(1);
    });
  });

  describe('composition', () => {
    it('renders with child components', () => {
      render(
        <ComponentName>
          <ComponentHeader>Header</ComponentHeader>
          <ComponentBody>Body</ComponentBody>
        </ComponentName>
      );

      expect(screen.getByText('Header')).toBeInTheDocument();
      expect(screen.getByText('Body')).toBeInTheDocument();
      expect(screen.getByText('Header').parentElement).toMatchSnapshot();
    });
  });
});
```

---

## Snapshot Update Commands

After reviewing the changes, update snapshots:

**Update all snapshots:**
```bash
npm test -- -u
# or
yarn test -u
```

**Update specific test file:**
```bash
npm test -- -u ComponentName.test.tsx
```

**Update snapshots interactively:**
```bash
npm test -- --watch
# Press 'u' to update snapshots
```

**Review snapshot changes:**
```bash
git diff -- **/__snapshots__/*.snap
```

---

## Migration Checklist

Use this checklist to verify complete migration:

### Enzyme Removal
- [ ] Removed all enzyme imports
- [ ] Removed enzyme adapter configuration
- [ ] Removed enzyme from package.json
- [ ] Deleted enzyme setup files

### RTL Implementation
- [ ] All tests use `render` from @testing-library/react
- [ ] Queries use semantic selectors (getByRole, getByLabelText)
- [ ] User interactions use userEvent, not simulate
- [ ] Async operations use waitFor/findBy queries
- [ ] No usage of wrapper.instance() or .state()

### Snapshot Quality
- [ ] Snapshots are focused, not full trees
- [ ] Each variant has its own snapshot
- [ ] State changes have separate snapshots
- [ ] Accessibility attributes included in snapshots
- [ ] No snapshots of third-party components
- [ ] Snapshot names are descriptive

### Accessibility Testing
- [ ] ARIA attributes tested
- [ ] Keyboard navigation tested
- [ ] Screen reader labels verified
- [ ] Focus management tested
- [ ] Disabled states tested

### Test Coverage
- [ ] All props tested
- [ ] All variants tested
- [ ] All states tested
- [ ] Error states tested
- [ ] Edge cases covered
- [ ] Integration tests for composed components

### Documentation
- [ ] Test descriptions are clear
- [ ] Complex setups have comments
- [ ] Test file follows project conventions
- [ ] README updated if testing approach changed

---

## Common Migration Patterns

### Pattern 1: Simple Component Snapshot

**Before:**
```tsx
it('renders', () => {
  const wrapper = shallow(<Badge>5</Badge>);
  expect(wrapper).toMatchSnapshot();
});
```

**After:**
```tsx
it('renders with expected structure', () => {
  const { container } = render(<Badge>5</Badge>);
  expect(container.firstChild).toMatchSnapshot();
});
```

### Pattern 2: Props Testing

**Before:**
```tsx
it('renders with custom class', () => {
  const wrapper = shallow(<Badge className="custom">5</Badge>);
  expect(wrapper.hasClass('custom')).toBe(true);
});
```

**After:**
```tsx
it('renders with custom class', () => {
  const { container } = render(<Badge className="custom">5</Badge>);
  const badge = container.firstChild;
  expect(badge).toHaveClass('custom');
  expect(badge).toMatchSnapshot();
});
```

### Pattern 3: Event Handling

**Before:**
```tsx
it('calls onClick', () => {
  const onClick = jest.fn();
  const wrapper = shallow(<Chip onClick={onClick}>Chip</Chip>);
  wrapper.find('button').simulate('click');
  expect(onClick).toHaveBeenCalled();
});
```

**After:**
```tsx
it('calls onClick when clicked', async () => {
  const user = userEvent.setup();
  const onClick = jest.fn();

  render(<Chip onClick={onClick}>Chip</Chip>);
  const chip = screen.getByRole('button', { name: 'Chip' });

  await user.click(chip);
  expect(onClick).toHaveBeenCalledTimes(1);
});
```

### Pattern 4: Conditional Rendering

**Before:**
```tsx
it('renders icon when provided', () => {
  const wrapper = shallow(<Alert icon={<InfoIcon />} />);
  expect(wrapper.find(InfoIcon)).toHaveLength(1);
});
```

**After:**
```tsx
it('renders icon when provided', () => {
  render(<Alert icon={<InfoIcon data-testid="info-icon" />} />);
  expect(screen.getByTestId('info-icon')).toBeInTheDocument();
  expect(screen.getByRole('alert')).toMatchSnapshot();
});
```

### Pattern 5: State Changes

**Before:**
```tsx
it('toggles expanded state', () => {
  const wrapper = shallow(<Expandable />);
  expect(wrapper.state('isExpanded')).toBe(false);
  wrapper.find('button').simulate('click');
  expect(wrapper.state('isExpanded')).toBe(true);
});
```

**After:**
```tsx
it('toggles expanded state', async () => {
  const user = userEvent.setup();

  render(<Expandable />);
  const toggle = screen.getByRole('button', { name: /expand/i });

  // Initially collapsed
  expect(toggle).toHaveAttribute('aria-expanded', 'false');

  // Click to expand
  await user.click(toggle);
  expect(toggle).toHaveAttribute('aria-expanded', 'true');

  // Snapshot of expanded state
  expect(toggle).toMatchSnapshot();
});
```

### Pattern 6: Async Operations

**Before:**
```tsx
it('loads data', done => {
  const wrapper = mount(<DataLoader />);
  setTimeout(() => {
    wrapper.update();
    expect(wrapper.find('.data')).toHaveLength(1);
    done();
  }, 100);
});
```

**After:**
```tsx
it('loads data asynchronously', async () => {
  render(<DataLoader />);

  // Wait for loading to complete
  const data = await screen.findByRole('region', { name: /data/i });

  expect(data).toBeInTheDocument();
  expect(data).toMatchSnapshot();
});
```

---

## Testing Utilities for Snapshots

### Custom Render Function

Create a custom render for common wrappers:

```tsx
// test-utils.tsx
import { render, RenderOptions } from '@testing-library/react';
import { ReactElement } from 'react';

interface CustomRenderOptions extends RenderOptions {
  // Add any custom options
}

export function renderWithProviders(
  ui: ReactElement,
  options?: CustomRenderOptions
) {
  function Wrapper({ children }: { children: React.ReactNode }) {
    return (
      // Add any providers needed
      <>{children}</>
    );
  }

  return render(ui, { wrapper: Wrapper, ...options });
}

// Re-export everything
export * from '@testing-library/react';
export { renderWithProviders as render };
```

### Snapshot Serializers

Add custom serializers for cleaner snapshots:

```tsx
// jest.config.js
module.exports = {
  snapshotSerializers: [
    '@testing-library/jest-dom/serializers',
  ],
};
```

### Helper Functions

```tsx
// test-helpers.tsx
export function getAllVariants(variants: string[]) {
  return variants.map(variant => ({
    variant,
    testName: `renders ${variant} variant`,
  }));
}

export function snapshotAllVariants(
  Component: React.ComponentType<any>,
  variants: string[],
  baseProps = {}
) {
  describe('variant snapshots', () => {
    variants.forEach(variant => {
      it(`renders ${variant} variant`, () => {
        const { container } = render(
          <Component {...baseProps} variant={variant} />
        );
        expect(container.firstChild).toMatchSnapshot();
      });
    });
  });
}
```

---

## Troubleshooting Common Issues

### Issue 1: Snapshots Too Large

**Problem:** Snapshot files are massive and hard to review

**Solution:**
```tsx
// Instead of full tree
const { container } = render(<LargeComponent />);
expect(container).toMatchSnapshot(); // ❌

// Snapshot specific parts
const header = screen.getByRole('banner');
expect(header).toMatchSnapshot(); // ✅
```

### Issue 2: Non-Deterministic Snapshots

**Problem:** Snapshots fail randomly due to generated IDs, dates, etc.

**Solution:**
```tsx
// Mock non-deterministic values
jest.spyOn(global, 'Date').mockImplementation(() =>
  new Date('2024-01-01')
);

// Or exclude them from snapshots
expect(container.firstChild).toMatchSnapshot({
  id: expect.any(String),
  timestamp: expect.any(Number),
});
```

### Issue 3: Enzyme Config Still Present

**Problem:** Tests fail because enzyme adapter still configured

**Solution:**
```tsx
// Remove from setupTests.ts
// import Adapter from '@wojtekmaj/enzyme-adapter-react-17'; // ❌
// import { configure } from 'enzyme'; // ❌
// configure({ adapter: new Adapter() }); // ❌
```

### Issue 4: Can't Find Elements

**Problem:** `getByRole` throws "Unable to find element"

**Solution:**
```tsx
// Debug the rendered output
screen.debug();

// Or use getAllByRole to see what's available
screen.logTestingPlaygroundURL();

// Use more specific query
screen.getByRole('button', { name: /exact text/i });
```

### Issue 5: Async Updates Not Captured

**Problem:** Snapshot taken before async updates complete

**Solution:**
```tsx
// Wait for updates
await waitFor(() => {
  expect(screen.getByText('Loaded')).toBeInTheDocument();
});

// Then snapshot
expect(screen.getByRole('region')).toMatchSnapshot();
```

---

## Resources

- **React Testing Library:** https://testing-library.com/react
- **PatternFly Testing Guide:** https://www.patternfly.org/contribute/testing
- **RTL Cheatsheet:** https://testing-library.com/docs/react-testing-library/cheatsheet
- **Enzyme to RTL Migration:** https://testing-library.com/docs/react-testing-library/migrate-from-enzyme
- **Jest Snapshot Testing:** https://jestjs.io/docs/snapshot-testing
- **Testing Accessibility:** https://testing-library.com/docs/queries/about#priority

---

## Next Steps After Modernization

1. **Run tests** - Ensure all modernized tests pass
2. **Review snapshots** - Verify snapshot diffs are expected
3. **Update package.json** - Remove enzyme dependencies
4. **Update CI/CD** - Ensure CI runs updated tests
5. **Document changes** - Update testing README
6. **Train team** - Share RTL best practices

```

## Critical Requirements

✅ **DO:**
- Analyze existing snapshots thoroughly before suggesting changes
- Explain WHY each change improves the test
- Provide side-by-side before/after comparisons
- Use semantic queries (getByRole, getByLabelText) exclusively
- Create focused snapshots, not full component trees
- Test accessibility attributes in snapshots
- Generate complete, runnable test files
- Include migration checklist
- Explain snapshot failure root causes
- Provide variant testing patterns

❌ **DON'T:**
- Suggest updating snapshots without understanding what changed
- Use implementation details in queries (classes, IDs)
- Create overly broad snapshots
- Skip accessibility testing
- Remove tests without replacement
- Ignore PatternFly testing patterns
- Suggest shallow rendering with RTL
- Use enzyme-style thinking with RTL
- Snapshot non-deterministic data without mocking
- Mix enzyme and RTL in same test

## Output Format

Generate a complete modernization report with:
1. Analysis of current snapshot tests and failures
2. Explanation of what changed and why
3. Complete before/after code examples
4. Updated test file following RTL best practices
5. Migration checklist
6. Commands to update snapshots
7. Troubleshooting guidance

Always provide working, tested code that can be directly used.
