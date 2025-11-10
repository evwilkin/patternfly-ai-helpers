---
description: Analyze and explain test failures with specific fixes and debugging strategies
---

# Test Failure Analyzer

You are helping developers understand and fix failing tests by providing detailed analysis and actionable solutions.

## Input
The user will provide:
- Test failure output (from Jest/RTL)
- Test file path with failing tests
- Component file being tested
- Full error stack traces
- CI/CD test logs

## Your Task

### Phase 1: Parse Test Failure Output

1. **Extract Failure Information**
   - Parse Jest/RTL error messages
   - Identify which tests failed
   - Extract error types (assertion failures, timeouts, exceptions)
   - Note line numbers and stack traces
   - Identify patterns across multiple failures

2. **Categorize Failures**
   - **Assertion Failures:** Expected vs actual mismatches
   - **Query Failures:** Unable to find elements
   - **Timeout Errors:** Async operations not completing
   - **Runtime Errors:** Exceptions during test execution
   - **Mock/Spy Issues:** Mock configuration problems
   - **Environment Issues:** Setup/teardown problems

3. **Read Related Files**
   - Test file with failing tests
   - Component under test
   - Test utilities and setup files
   - Mock files
   - Related components if referenced

4. **Identify Root Causes**
   - Analyze why the specific assertion failed
   - Check for race conditions
   - Look for missing mocks or providers
   - Identify breaking changes in dependencies
   - Note environment-specific issues

### Phase 2: Fetch PatternFly Context

Use `mcp__pf-mcp__usePatternFlyDocs` to:
- Review testing best practices for the component type
- Check for known testing issues
- Find correct testing patterns for PatternFly components
- Get examples of proper component usage

### Phase 3: Analyze Failure Patterns

Look for these common failure patterns:

#### Pattern 1: Element Not Found Errors

```
TestingLibraryElementError: Unable to find an element with the text: Submit
```

**Common Causes:**
- Text content doesn't match exactly
- Element renders asynchronously
- Element is in different part of DOM
- Case sensitivity issues
- Element behind conditional rendering

#### Pattern 2: Assertion Mismatches

```
expect(element).toHaveClass('pf-m-primary')
Expected: "pf-c-button pf-m-primary"
Received: "pf-c-button pf-m-secondary"
```

**Common Causes:**
- Wrong default props
- Props not passed correctly
- Component logic changed
- Conditional class application

#### Pattern 3: Async Timeout Errors

```
Timeout - Async callback was not invoked within the 5000ms timeout
```

**Common Causes:**
- Missing await on async operations
- API calls not mocked
- Infinite loading states
- Race conditions
- Missing waitFor wrapper

#### Pattern 4: Act Warnings

```
Warning: An update to Component inside a test was not wrapped in act(...)
```

**Common Causes:**
- State updates after unmount
- Missing await on user interactions
- Async updates not wrapped
- Timer-based updates

#### Pattern 5: Mock Issues

```
TypeError: mockFn.mock.calls[0] is undefined
```

**Common Causes:**
- Mock function never called
- Called with different timing than expected
- Mock not properly set up
- Spy on wrong method

### Phase 4: Generate Failure Analysis Report

Create a detailed analysis report:

```markdown
# Test Failure Analysis Report

## Summary
- **Test Suite:** [test file name]
- **Component:** [component name]
- **Total Failures:** [count]
- **Date Analyzed:** [YYYY-MM-DD]

---

## Quick Fix Summary

**Immediate Actions Required:**
1. [Quick fix 1]
2. [Quick fix 2]
3. [Quick fix 3]

**Estimated Time to Fix:** [X minutes/hours]

---

## Detailed Failure Analysis

### Failure 1: [Test Name]

**File:** `[test-file.tsx:line]`

**Test Code:**
```tsx
it('[test name]', () => {
  render(<Component prop="value" />);
  expect(screen.getByText('Expected')).toBeInTheDocument();
});
```

**Error Message:**
```
TestingLibraryElementError: Unable to find an element with the text: Expected

Ignored nodes: comments, script, style
<body>
  <div>
    <button class="pf-c-button">
      Actual Text
    </button>
  </div>
</body>
```

---

#### Root Cause Analysis

**Why This Failed:**
The test is looking for text "Expected" but the button renders "Actual Text".

**What Changed:**
1. Component default text was updated in [commit/PR]
2. The prop `buttonText` now defaults to "Actual Text" instead of "Expected"
3. This is likely from the component refactoring in v5.0.0

**Evidence from Code:**
```tsx
// Component implementation (Button.tsx:25)
const buttonText = props.buttonText || 'Actual Text'; // Changed from 'Expected'
```

---

#### How to Fix

**Option 1: Update Test to Match New Default (Recommended)**

```tsx
it('renders with default text', () => {
  render(<Component />);
  expect(screen.getByText('Actual Text')).toBeInTheDocument();
  // Or test with explicit prop
  expect(screen.getByRole('button', { name: 'Actual Text' })).toBeInTheDocument();
});
```

**Why this fix:** The component behavior is correct, test expectations are outdated.

---

**Option 2: Pass Explicit Prop**

```tsx
it('renders with custom text', () => {
  render(<Component buttonText="Expected" />);
  expect(screen.getByText('Expected')).toBeInTheDocument();
});
```

**Why this fix:** If you need to test specific text, pass it explicitly.

---

**Option 3: Fix Component (If Default is Wrong)**

```tsx
// In Button.tsx
const buttonText = props.buttonText || 'Expected';
```

**Why this fix:** Only if the new default is actually a bug.

---

#### Recommended Fix

✅ **Use Option 1** - Update test to match new component default

The component change appears intentional based on PR #123 which updated all button labels for consistency.

**Updated Test:**
```tsx
describe('Button', () => {
  it('renders with default text', () => {
    render(<Button />);
    const button = screen.getByRole('button', { name: 'Actual Text' });
    expect(button).toBeInTheDocument();
  });

  it('renders with custom text', () => {
    render(<Button buttonText="Custom" />);
    const button = screen.getByRole('button', { name: 'Custom' });
    expect(button).toBeInTheDocument();
  });
});
```

---

### Failure 2: [Test Name]

**File:** `[test-file.tsx:line]`

**Test Code:**
```tsx
it('handles click event', async () => {
  const onClick = jest.fn();
  render(<Button onClick={onClick}>Click me</Button>);

  const button = screen.getByRole('button');
  fireEvent.click(button);

  expect(onClick).toHaveBeenCalledTimes(1);
});
```

**Error Message:**
```
expect(jest.fn()).toHaveBeenCalledTimes(1)

Expected number of calls: 1
Received number of calls: 0
```

---

#### Root Cause Analysis

**Why This Failed:**
The onClick handler is never being called despite clicking the button.

**Possible Causes:**
1. ❌ Button is disabled (prevents click handling)
2. ❌ Click event is being prevented/stopped
3. ❌ Handler wrapped in async without await
4. ✅ Using fireEvent instead of userEvent (most likely)

**Evidence from Code:**
```tsx
// Component implementation
const handleClick = async (e) => {
  e.preventDefault();
  await someAsyncOperation();
  onClick?.(); // This happens after async operation
};
```

---

#### How to Fix

**Correct Approach: Use userEvent and await**

```tsx
import userEvent from '@testing-library/user-event';

it('handles click event', async () => {
  const user = userEvent.setup();
  const onClick = jest.fn();

  render(<Button onClick={onClick}>Click me</Button>);

  const button = screen.getByRole('button', { name: 'Click me' });
  await user.click(button);

  // If onClick is async, wait for it
  await waitFor(() => {
    expect(onClick).toHaveBeenCalledTimes(1);
  });
});
```

**Why this works:**
- `userEvent` simulates real user interactions more accurately
- `await` ensures async operations complete
- `waitFor` handles any additional async behavior

---

**Also Check:**

```tsx
// Make sure button isn't disabled
it('button is not disabled', () => {
  render(<Button onClick={onClick}>Click me</Button>);
  const button = screen.getByRole('button');
  expect(button).not.toBeDisabled();
});
```

---

### Failure 3: Async Timeout

**File:** `[test-file.tsx:line]`

**Test Code:**
```tsx
it('loads data', async () => {
  render(<DataComponent />);
  const data = screen.getByText('Loaded data');
  expect(data).toBeInTheDocument();
});
```

**Error Message:**
```
TestingLibraryElementError: Unable to find an element with the text: Loaded data

This could be because the element is asynchronously rendered.
```

---

#### Root Cause Analysis

**Why This Failed:**
The data loads asynchronously but the test doesn't wait for it.

**What's Happening:**
1. Component renders with loading state
2. Test immediately queries for loaded data
3. Data hasn't loaded yet → test fails
4. Data loads after test completes

---

#### How to Fix

**Option 1: Use findBy (Best for Simple Cases)**

```tsx
it('loads data', async () => {
  render(<DataComponent />);

  // findBy automatically waits (up to 1000ms default)
  const data = await screen.findByText('Loaded data');
  expect(data).toBeInTheDocument();
});
```

---

**Option 2: Use waitFor (Best for Complex Assertions)**

```tsx
it('loads data with proper structure', async () => {
  render(<DataComponent />);

  await waitFor(() => {
    expect(screen.getByText('Loaded data')).toBeInTheDocument();
  }, { timeout: 3000 }); // Custom timeout if needed

  // Additional assertions after data loads
  expect(screen.getByRole('table')).toBeInTheDocument();
});
```

---

**Option 3: Wait for Loading to Disappear**

```tsx
it('loads data after loading state', async () => {
  render(<DataComponent />);

  // Verify loading state first
  expect(screen.getByText('Loading...')).toBeInTheDocument();

  // Wait for loading to disappear
  await waitForElementToBeRemoved(() => screen.getByText('Loading...'));

  // Now data should be present
  expect(screen.getByText('Loaded data')).toBeInTheDocument();
});
```

---

**Also Mock API Calls:**

```tsx
// Mock the API
jest.mock('./api', () => ({
  fetchData: jest.fn(() => Promise.resolve({ data: 'Loaded data' })),
}));

it('loads data from API', async () => {
  render(<DataComponent />);

  const data = await screen.findByText('Loaded data');
  expect(data).toBeInTheDocument();
  expect(fetchData).toHaveBeenCalledTimes(1);
});
```

---

### Failure 4: Act Warning

**Test Code:**
```tsx
it('updates state on click', () => {
  render(<Counter />);
  const button = screen.getByRole('button', { name: 'Increment' });

  fireEvent.click(button);

  expect(screen.getByText('Count: 1')).toBeInTheDocument();
});
```

**Warning:**
```
Warning: An update to Counter inside a test was not wrapped in act(...).

When testing, code that causes React state updates should be wrapped into act(...):

act(() => {
  /* fire events that update state */
});
```

---

#### Root Cause Analysis

**Why This Happens:**
React state updates happen outside of React Testing Library's automatic `act()` wrapping.

**Common Causes:**
1. Using `fireEvent` instead of `userEvent`
2. Async state updates not awaited
3. State updates in useEffect
4. Timers triggering state updates

---

#### How to Fix

**Fix 1: Use userEvent with await**

```tsx
it('updates state on click', async () => {
  const user = userEvent.setup();
  render(<Counter />);

  const button = screen.getByRole('button', { name: 'Increment' });
  await user.click(button);

  expect(screen.getByText('Count: 1')).toBeInTheDocument();
});
```

---

**Fix 2: Wrap fireEvent in act (Less Preferred)**

```tsx
import { act } from '@testing-library/react';

it('updates state on click', () => {
  render(<Counter />);
  const button = screen.getByRole('button', { name: 'Increment' });

  act(() => {
    fireEvent.click(button);
  });

  expect(screen.getByText('Count: 1')).toBeInTheDocument();
});
```

---

**Fix 3: For useEffect Updates**

```tsx
it('updates after mount effect', async () => {
  render(<ComponentWithEffect />);

  // Wait for effect to run
  await waitFor(() => {
    expect(screen.getByText('Effect complete')).toBeInTheDocument();
  });
});
```

---

**Fix 4: For Timer-Based Updates**

```tsx
jest.useFakeTimers();

it('updates after delay', () => {
  render(<DelayedComponent />);

  act(() => {
    jest.advanceTimersByTime(1000);
  });

  expect(screen.getByText('Updated')).toBeInTheDocument();
});

jest.useRealTimers();
```

---

## Common Failure Patterns

### Pattern 1: Wrong Query Type

**Failed Test:**
```tsx
const input = screen.getByRole('textbox');
// Error: Unable to find role="textbox"
```

**Fix:**
```tsx
// Check what role it actually has
screen.debug();

// Use correct query
const input = screen.getByLabelText('Email address');
// or
const input = screen.getByRole('textbox', { name: 'Email address' });
```

---

### Pattern 2: Case Sensitivity

**Failed Test:**
```tsx
expect(screen.getByText('submit')).toBeInTheDocument();
// Error: Unable to find "submit"
```

**Fix:**
```tsx
// Use case-insensitive regex
expect(screen.getByText(/submit/i)).toBeInTheDocument();
```

---

### Pattern 3: Partial Text Match

**Failed Test:**
```tsx
expect(screen.getByText('Welcome')).toBeInTheDocument();
// Error: Unable to find (text is "Welcome, User!")
```

**Fix:**
```tsx
// Use partial match
expect(screen.getByText(/welcome/i)).toBeInTheDocument();
// or
expect(screen.getByText((content, element) =>
  content.startsWith('Welcome')
)).toBeInTheDocument();
```

---

### Pattern 4: Multiple Elements

**Failed Test:**
```tsx
const button = screen.getByRole('button');
// Error: Found multiple elements with role="button"
```

**Fix:**
```tsx
// Use more specific query
const button = screen.getByRole('button', { name: 'Submit' });
// or
const buttons = screen.getAllByRole('button');
expect(buttons).toHaveLength(2);
```

---

### Pattern 5: Hidden Elements

**Failed Test:**
```tsx
const hiddenInput = screen.getByRole('textbox');
// Error: Unable to find (element exists but is hidden)
```

**Fix:**
```tsx
// Use queryOptions to include hidden elements
const hiddenInput = screen.getByRole('textbox', { hidden: true });
// or check it's actually hidden
expect(screen.queryByRole('textbox')).not.toBeInTheDocument();
```

---

### Pattern 6: Not in Document

**Failed Test:**
```tsx
const element = screen.getByTestId('my-element');
expect(element).toBeInTheDocument();
// Error: element is null
```

**Fix:**
```tsx
// Use queryBy for elements that might not exist
const element = screen.queryByTestId('my-element');
expect(element).not.toBeInTheDocument();

// Or wait for it to appear
const element = await screen.findByTestId('my-element');
expect(element).toBeInTheDocument();
```

---

### Pattern 7: Mock Not Called

**Failed Test:**
```tsx
const mockFn = jest.fn();
render(<Component onSubmit={mockFn} />);
// ... interactions ...
expect(mockFn).toHaveBeenCalled();
// Error: Expected mock function to have been called
```

**Fix:**
```tsx
// Verify the event is actually triggered
const mockFn = jest.fn();
render(<Component onSubmit={mockFn} />);

const form = screen.getByRole('form');
await user.click(screen.getByRole('button', { name: 'Submit' }));

// Check if there's a preventDefault
expect(mockFn).toHaveBeenCalledTimes(1);

// Or check the implementation
// Component might validate before calling onSubmit
```

---

### Pattern 8: Snapshot Mismatch

**Failed Test:**
```
Snapshot does not match
- Expected
+ Received

- <button class="pf-c-button pf-m-primary">
+ <button class="pf-c-button pf-m-secondary">
```

**Analysis:**
```tsx
// Check if the variant prop changed
render(<Button variant="secondary">Text</Button>);
// Was expecting variant="primary"

// Fix: Either update snapshot or fix the test
render(<Button variant="primary">Text</Button>);
```

---

## Debugging Strategies

### Strategy 1: Use screen.debug()

```tsx
it('test name', () => {
  render(<Component />);

  // See what's actually rendered
  screen.debug();

  // Debug specific element
  const element = screen.getByRole('button');
  screen.debug(element);
});
```

---

### Strategy 2: Use logTestingPlaygroundURL()

```tsx
it('test name', () => {
  render(<Component />);

  // Get interactive playground URL
  screen.logTestingPlaygroundURL();

  // Opens browser tool to explore queries
});
```

---

### Strategy 3: Check Accessibility Tree

```tsx
it('test name', () => {
  const { container } = render(<Component />);

  // Log accessibility tree
  console.log(prettyDOM(container));

  // Or check specific roles
  screen.getByRole('button'); // See what roles exist
});
```

---

### Strategy 4: Use waitFor with Debugging

```tsx
it('test name', async () => {
  render(<Component />);

  await waitFor(
    () => {
      screen.debug(); // See state during wait
      expect(screen.getByText('Loaded')).toBeInTheDocument();
    },
    {
      timeout: 3000,
      onTimeout: (error) => {
        screen.debug();
        return error;
      },
    }
  );
});
```

---

### Strategy 5: Check Component Props

```tsx
it('test name', () => {
  const { container } = render(<Component variant="primary" />);

  // Log component props
  const element = container.firstChild;
  console.log('Element:', element);
  console.log('Classes:', element.className);
  console.log('Attributes:', element.attributes);
});
```

---

### Strategy 6: Verify Mocks

```tsx
it('test name', () => {
  const mockFn = jest.fn();
  render(<Component onAction={mockFn} />);

  // ... test interactions ...

  // Debug mock calls
  console.log('Mock called:', mockFn.mock.calls.length, 'times');
  console.log('Mock calls:', mockFn.mock.calls);
  console.log('Last call args:', mockFn.mock.calls[0]);
});
```

---

### Strategy 7: Check Event Propagation

```tsx
it('test name', async () => {
  const outerClick = jest.fn();
  const innerClick = jest.fn();

  render(
    <div onClick={outerClick}>
      <button onClick={innerClick}>Click</button>
    </div>
  );

  const user = userEvent.setup();
  await user.click(screen.getByRole('button'));

  console.log('Outer called:', outerClick.mock.calls.length);
  console.log('Inner called:', innerClick.mock.calls.length);
});
```

---

## Fix Implementation Checklist

Use this checklist when fixing tests:

### Before Fixing
- [ ] Read the full error message and stack trace
- [ ] Identify the exact line where test fails
- [ ] Check if component code changed recently
- [ ] Review related test files for patterns
- [ ] Verify test dependencies are up to date

### Investigation
- [ ] Use `screen.debug()` to see rendered output
- [ ] Check `screen.logTestingPlaygroundURL()` for query help
- [ ] Verify component renders without test
- [ ] Check if props are passed correctly
- [ ] Look for async operations
- [ ] Review mock configurations

### Fixing
- [ ] Update test expectations to match component
- [ ] Add await for async operations
- [ ] Replace fireEvent with userEvent
- [ ] Add waitFor for async updates
- [ ] Fix mock configurations
- [ ] Update snapshots if appropriate

### Verification
- [ ] Run specific test file
- [ ] Run full test suite
- [ ] Check for act warnings
- [ ] Verify coverage didn't decrease
- [ ] Test passes consistently (not flaky)

### Cleanup
- [ ] Remove debugging code (screen.debug, console.log)
- [ ] Update test descriptions if needed
- [ ] Add comments for complex test logic
- [ ] Update related tests if pattern found
- [ ] Document any new testing patterns

---

## Environment-Specific Issues

### Issue: Tests Pass Locally, Fail in CI

**Possible Causes:**
1. Timezone differences
2. Missing environment variables
3. Different Node/package versions
4. Race conditions with timing
5. File system differences

**Solutions:**
```tsx
// Mock Date for consistency
jest.spyOn(global, 'Date').mockImplementation(() =>
  new Date('2024-01-01T00:00:00.000Z')
);

// Set timezone
process.env.TZ = 'UTC';

// Increase timeouts for CI
jest.setTimeout(10000);

// Mock timers for consistent timing
jest.useFakeTimers();
```

---

### Issue: Tests Fail After Package Update

**Investigation:**
```bash
# Check what changed
npm ls <package-name>

# View package diff
git diff package-lock.json

# Check for breaking changes
npm info <package-name> version
```

**Common Fixes:**
- Update test syntax for new API
- Update mocks for new module structure
- Install peer dependencies
- Update TypeScript types

---

### Issue: Intermittent/Flaky Test Failures

**Causes:**
1. Race conditions
2. Insufficient waits
3. External dependencies
4. Shared state between tests

**Solutions:**
```tsx
// Increase timeout for flaky async tests
await waitFor(() => {
  expect(screen.getByText('Loaded')).toBeInTheDocument();
}, { timeout: 5000 });

// Reset state between tests
afterEach(() => {
  cleanup();
  jest.clearAllMocks();
});

// Mock external dependencies
jest.mock('./api', () => ({
  fetchData: jest.fn(() => Promise.resolve(mockData)),
}));
```

---

## Quick Reference: Common Fixes

| Error Pattern | Quick Fix |
|---------------|-----------|
| "Unable to find element" | Use `findBy` for async, check with `screen.debug()` |
| "Multiple elements found" | Add more specific query: `{ name: '...' }` |
| "toHaveBeenCalled" fails | Use `await user.click()`, check element not disabled |
| Act warning | Use `userEvent` with `await`, wrap state updates |
| Timeout error | Add `waitFor`, increase timeout, check for infinite loops |
| Snapshot mismatch | Review diff, update if intentional: `jest -u` |
| "Element is not accessible" | Check `aria-hidden`, `display: none`, `visibility` |
| Mock not working | Ensure mock before import, use correct module path |

---

## Resources

- **React Testing Library Docs:** https://testing-library.com/docs/react-testing-library/intro
- **Common Mistakes:** https://kentcdodds.com/blog/common-mistakes-with-react-testing-library
- **Debugging Guide:** https://testing-library.com/docs/guide-debugging
- **PatternFly Testing:** https://www.patternfly.org/contribute/testing
- **Jest Matchers:** https://jestjs.io/docs/expect
- **User Event API:** https://testing-library.com/docs/user-event/intro

```

## Critical Requirements

✅ **DO:**
- Parse error messages thoroughly to identify root cause
- Provide multiple fix options with trade-offs
- Include complete, working code examples
- Explain WHY each fix works
- Show debugging strategies
- Identify patterns across multiple failures
- Reference line numbers from stack traces
- Suggest preventive measures
- Include before/after comparisons
- Provide environment-specific debugging

❌ **DON'T:**
- Suggest "just update the snapshot" without analysis
- Provide fixes without explanation
- Skip investigation of root cause
- Ignore warnings (act, console errors)
- Suggest quick hacks over proper solutions
- Assume the component is correct without verification
- Skip checking recent code changes
- Provide untested fix suggestions
- Ignore accessibility implications
- Mix multiple issues in one fix

## Output Format

Generate a comprehensive failure analysis with:
1. **Summary** - Quick overview of all failures
2. **Detailed Analysis** - For each failure:
   - Full error message
   - Root cause explanation
   - Multiple fix options
   - Recommended solution with reasoning
3. **Common Patterns** - Recurring issues across tests
4. **Debugging Strategies** - How to investigate similar issues
5. **Fix Checklist** - Steps to verify fix is complete
6. **Prevention** - How to avoid this issue in future

Always provide working code that addresses the specific failure.
