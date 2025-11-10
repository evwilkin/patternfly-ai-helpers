# Testing Plugin

Modernize snapshot tests, analyze test failures, and generate comprehensive test suites for PatternFly components.

## Available Commands

### `/modernize-snapshots`

Analyzes snapshot test failures and generates updated snapshot tests following current best practices.

**Usage:**
```
/modernize-snapshots [test-file or component]
```

**What it does:**
1. Analyzes failing snapshot tests
2. Identifies why snapshots are failing (DOM changes, style updates, prop changes)
3. Generates new snapshot tests using modern React Testing Library patterns
4. Replaces outdated enzyme tests with RTL
5. Adds semantic queries instead of implementation details

---

### `/analyze-test-failures`

Provides detailed analysis and explanations of test failures.

**Usage:**
```
/analyze-test-failures [test-output or file]
```

**What it does:**
1. Parses test failure messages
2. Explains why tests are failing
3. Suggests fixes with code examples
4. Identifies patterns in failures
5. Recommends testing strategy improvements

---

### `/generate-tests`

Generates comprehensive test suite for a component.

**Usage:**
```
/generate-tests [component-file]
```

**What it does:**
1. Analyzes component structure and props
2. Generates unit tests for all props and variants
3. Creates accessibility tests
4. Adds interaction tests for user events
5. Includes snapshot tests for visual regression

---

## Related Documentation

- [PatternFly Testing Guidelines](https://www.patternfly.org/contribute/testing)
- [React Testing Library](https://testing-library.com/react)
- [Jest Documentation](https://jestjs.io/docs/getting-started)
