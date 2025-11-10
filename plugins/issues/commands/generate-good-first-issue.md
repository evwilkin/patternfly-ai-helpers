---
description: Generate well-documented "Good First Issue" GitHub issues for new contributors
---

# Good First Issue Generator

You are creating detailed, beginner-friendly "Good First Issue" GitHub issues to help onboard new contributors to PatternFly.

## Input

The user will provide:
- A specific area or component to analyze (e.g., "Button component", "documentation")
- A file path to evaluate for improvements
- A general topic (e.g., "accessibility", "testing", "TypeScript migration")
- No input (scan for opportunities across the codebase)

## Your Task

### Phase 1: Codebase Scanning and Opportunity Identification

1. **Scan for Common Improvement Opportunities**

   Look for these beginner-friendly issues:

   **Missing Tests:**
   - Components without test files
   - Low test coverage areas
   - Missing edge case tests
   - Untested prop combinations
   - Missing accessibility tests
   - No interaction tests
   - Snapshot tests needed

   **Documentation Gaps:**
   - Missing JSDoc comments
   - Outdated documentation
   - No usage examples
   - Missing prop descriptions
   - No accessibility guidelines
   - Incomplete migration guides
   - Missing code examples in docs

   **Accessibility Improvements:**
   - Missing ARIA labels
   - Missing keyboard navigation
   - No screen reader support
   - Missing focus indicators
   - Unlabeled form controls
   - Missing alt text
   - Color contrast issues

   **TypeScript Migrations:**
   - JavaScript files that could be TypeScript
   - Missing type definitions
   - Any types that need proper types
   - Missing prop type definitions
   - Untyped utility functions

   **Code Quality Improvements:**
   - Outdated dependencies
   - Console warnings
   - ESLint warnings that can be fixed
   - Deprecated API usage
   - Simple refactoring opportunities
   - Duplicated code
   - Magic numbers/strings

   **Component Enhancements:**
   - Missing component variants
   - Additional prop support
   - Better error messages
   - Improved default values
   - Additional utility functions

2. **Analyze Multiple Candidates**

   For each opportunity found:
   - Assess complexity level (1-5 scale)
   - Estimate time to complete (2-8 hours ideal)
   - Identify required knowledge (React, TypeScript, accessibility, etc.)
   - Check for potential blockers
   - Evaluate impact vs. effort ratio
   - Consider if it's self-contained
   - Verify it has clear acceptance criteria

3. **Select Best Candidate**

   Choose the opportunity that:
   - ✅ Is truly beginner-friendly (complexity 1-3)
   - ✅ Has clear, achievable goals
   - ✅ Requires 2-8 hours of work
   - ✅ Is self-contained (minimal dependencies)
   - ✅ Has visible, satisfying impact
   - ✅ Provides good learning opportunity
   - ✅ Has clear testing/validation steps
   - ✅ Aligns with PatternFly patterns
   - ❌ Doesn't require deep architecture knowledge
   - ❌ Doesn't block other work
   - ❌ Doesn't require access to specific tools/environments
   - ❌ Doesn't involve complex algorithms

### Phase 2: Technical Analysis

1. **Deep Dive into the Issue**

   - Read all relevant files completely
   - Understand current implementation
   - Identify exact changes needed
   - List specific files to modify
   - Find similar patterns in codebase
   - Locate relevant tests to reference
   - Check for related documentation
   - Review PatternFly guidelines

2. **Use PatternFly Documentation**

   Use `mcp__pf-mcp__usePatternFlyDocs` to fetch:
   - Relevant component guidelines
   - Testing best practices
   - Accessibility requirements
   - Code style guidelines
   - Similar component examples
   - Contribution guidelines

3. **Prepare Implementation Guidance**

   - Identify exact files to modify
   - Note specific line numbers/sections
   - Find code examples to reference
   - Prepare code snippets
   - List testing approach
   - Identify validation steps

### Phase 3: Generate Comprehensive GitHub Issue

Create a detailed, structured issue using this exact format:

```markdown
# [Clear, Descriptive Title]

**Labels:** `good-first-issue`, [additional labels like: `documentation`, `accessibility`, `testing`, `typescript`, `component: [name]`]

**Estimated Time:** [2-8 hours]

**Difficulty:** ⭐ [Beginner/Easy/Moderate]

---

## 📋 Overview

[2-3 sentence summary of what needs to be done and why it matters]

**Why this matters:**
- [Benefit to users]
- [Benefit to codebase]
- [Learning opportunity for contributor]

---

## 🎯 Problem Statement

[Detailed explanation of the current state and what's missing]

**Current State:**
```[language]
[Show current code or state, if applicable]
```

**What's Missing:**
- [ ] [Specific item 1]
- [ ] [Specific item 2]
- [ ] [Specific item 3]

**Impact:**
- **Users:** [How this affects end users]
- **Developers:** [How this affects other developers]
- **Maintainability:** [How this improves the codebase]

---

## 💡 Proposed Solution

[Clear description of the desired end state]

**Approach:**

1. **[Phase 1 Name]**
   - [Specific step]
   - [Specific step]
   - [Expected outcome]

2. **[Phase 2 Name]**
   - [Specific step]
   - [Specific step]
   - [Expected outcome]

3. **[Phase 3 Name]**
   - [Specific step]
   - [Specific step]
   - [Expected outcome]

---

## 🛠️ Step-by-Step Implementation Guide

### Step 1: [Action Name]

**What to do:**
[Detailed explanation]

**File to modify:**
```
[absolute file path]
```

**Code to add/change:**
```[language]
// Find this section:
[current code snippet]

// Update it to:
[new code snippet]

// Why: [Explanation of why this change is needed]
```

**Tips:**
- 💡 [Helpful tip 1]
- 💡 [Helpful tip 2]

---

### Step 2: [Action Name]

**What to do:**
[Detailed explanation]

**File to modify:**
```
[absolute file path]
```

**Code to add/change:**
```[language]
[Code example with clear before/after or addition]
```

**Reference examples:**
- See [similar component/file] for a good example: `[file path]`
- Pattern to follow: [link to PatternFly docs or example]

---

### Step 3: [Testing]

**What to test:**
[Explanation of testing requirements]

**Create test file:**
```
[test file path]
```

**Test code example:**
```[language]
[Complete test example with clear explanations]
```

**How to run tests:**
```bash
# Run tests
npm test [component].test

# Run with coverage
npm test -- --coverage [component].test

# All tests should pass
npm run test
```

---

### Step 4: [Documentation]

**What to document:**
[Explanation of documentation requirements]

**File to update:**
```
[documentation file path]
```

**Documentation to add:**
```markdown
[Example documentation with clear structure]
```

---

## 📝 Code Examples and Hints

### Example 1: [Concept Name]

**Scenario:**
[When to use this pattern]

**Implementation:**
```[language]
[Complete, working code example]
```

**Explanation:**
[Line-by-line breakdown of what the code does]

---

### Example 2: [Concept Name]

**Reference:**
Look at `[file path]` for a similar implementation.

**Key points:**
- [Important detail 1]
- [Important detail 2]
- [Important detail 3]

**Code pattern:**
```[language]
[Reusable code pattern]
```

---

### Common Patterns in PatternFly

**Pattern 1: [Name]**
```[language]
[Pattern code]
```
Used when: [Use case]

**Pattern 2: [Name]**
```[language]
[Pattern code]
```
Used when: [Use case]

---

## ✅ Acceptance Criteria

Your implementation is complete when:

- [ ] **Functionality**
  - [ ] [Specific functional requirement 1]
  - [ ] [Specific functional requirement 2]
  - [ ] [Specific functional requirement 3]

- [ ] **Code Quality**
  - [ ] Code follows PatternFly style guidelines
  - [ ] No ESLint errors or warnings
  - [ ] No TypeScript errors
  - [ ] Code is properly formatted (run `npm run format`)
  - [ ] No console warnings

- [ ] **Testing**
  - [ ] All new code is tested
  - [ ] All existing tests still pass
  - [ ] Test coverage is maintained or improved
  - [ ] Edge cases are tested
  - [ ] [Specific test requirement]

- [ ] **Documentation**
  - [ ] JSDoc comments added/updated
  - [ ] README updated if needed
  - [ ] Props documented
  - [ ] Examples provided
  - [ ] [Specific documentation requirement]

- [ ] **Accessibility** (if applicable)
  - [ ] Keyboard navigation works
  - [ ] Screen reader friendly
  - [ ] ARIA attributes correct
  - [ ] Focus management proper
  - [ ] Color contrast meets WCAG AA

- [ ] **Visual Testing** (if applicable)
  - [ ] Component renders correctly in all variants
  - [ ] No visual regressions
  - [ ] Responsive design works
  - [ ] Snapshots updated

---

## 🧪 Testing Your Changes

### Manual Testing

1. **Build the project:**
   ```bash
   npm run build
   ```

2. **Start the development server:**
   ```bash
   npm run dev
   ```

3. **Test your changes:**
   - [ ] [Specific manual test 1]
   - [ ] [Specific manual test 2]
   - [ ] [Specific manual test 3]

### Automated Testing

```bash
# Run all tests
npm test

# Run specific test file
npm test [component].test

# Run tests in watch mode
npm test -- --watch

# Check test coverage
npm test -- --coverage
```

### Validation Checklist

Before submitting your PR:

- [ ] Code builds without errors: `npm run build`
- [ ] All tests pass: `npm test`
- [ ] No linting errors: `npm run lint`
- [ ] Code is formatted: `npm run format`
- [ ] Manual testing completed
- [ ] Documentation updated
- [ ] Accessibility checked (if applicable)

---

## 📚 Helpful Resources

### PatternFly Documentation
- [Component Overview]([relevant PatternFly component URL])
- [Accessibility Guidelines](https://www.patternfly.org/accessibility/accessibility-fundamentals)
- [Development Guidelines](https://www.patternfly.org/get-started/develop)
- [Testing Guidelines]([testing docs URL])

### React/TypeScript Resources
- [React Testing Library Documentation](https://testing-library.com/docs/react-testing-library/intro)
- [TypeScript Handbook](https://www.typescriptlang.org/docs/handbook/intro.html)
- [React Accessibility](https://react.dev/learn/accessibility)

### Similar Examples in Codebase
- `[file path 1]` - [What to learn from it]
- `[file path 2]` - [What to learn from it]
- `[file path 3]` - [What to learn from it]

### Tools
- [PatternFly Design Kit](https://www.patternfly.org/design-foundations/design-kits)
- [PatternFly React Docs](https://www.patternfly.org/components/all-components)
- [WCAG Quick Reference](https://www.w3.org/WAI/WCAG21/quickref/)

### Getting Help
- [PatternFly Slack]([Slack URL]) - Join #patternfly-react channel
- [Discussions](https://github.com/patternfly/patternfly-react/discussions)
- [Contributing Guide](https://github.com/patternfly/patternfly-react/blob/main/CONTRIBUTING.md)

---

## 🎓 What You'll Learn

By completing this issue, you'll gain experience with:

- ✅ [Skill 1] - [Why it's valuable]
- ✅ [Skill 2] - [Why it's valuable]
- ✅ [Skill 3] - [Why it's valuable]
- ✅ Working with PatternFly design system
- ✅ React best practices
- ✅ [Technology-specific skill]
- ✅ Open source contribution workflow

This is a great issue for learning because:
- [Reason 1]
- [Reason 2]
- [Reason 3]

---

## 💬 Getting Started

### New to Contributing?

1. **Fork the repository**
   ```bash
   # Click the "Fork" button on GitHub
   ```

2. **Clone your fork**
   ```bash
   git clone https://github.com/YOUR-USERNAME/patternfly-react.git
   cd patternfly-react
   ```

3. **Install dependencies**
   ```bash
   npm install
   ```

4. **Create a branch**
   ```bash
   git checkout -b fix/[issue-description]
   ```

5. **Make your changes** (follow the implementation guide above)

6. **Test your changes**
   ```bash
   npm test
   npm run build
   ```

7. **Commit your changes**
   ```bash
   git add .
   git commit -m "fix: [brief description of fix]"
   ```

8. **Push to your fork**
   ```bash
   git push origin fix/[issue-description]
   ```

9. **Open a Pull Request**
   - Go to the original repository
   - Click "New Pull Request"
   - Select your fork and branch
   - Fill out the PR template

### Questions?

Don't hesitate to ask! You can:
- Comment on this issue
- Ask in the PatternFly Slack (#patternfly-react channel)
- Tag @[maintainer-username] for guidance

We're here to help! 🎉

---

## 🤝 Mentorship Guidance

### For First-Time Contributors

**Expect to spend:**
- [X] hours on implementation
- [Y] hours on testing
- [Z] hours on documentation
- Total: [X+Y+Z] hours

**If you get stuck:**

1. **On Step 1:** [Common issue and solution]
2. **On Step 2:** [Common issue and solution]
3. **On Step 3:** [Common issue and solution]

**Common pitfalls to avoid:**
- ⚠️ [Pitfall 1] - [How to avoid it]
- ⚠️ [Pitfall 2] - [How to avoid it]
- ⚠️ [Pitfall 3] - [How to avoid it]

### Learning Path

This issue builds on these concepts:
1. [Prerequisite concept 1] - [Why it matters]
2. [Prerequisite concept 2] - [Why it matters]
3. [Prerequisite concept 3] - [Why it matters]

After completing this issue, you'll be ready for:
- [Next level issue type 1]
- [Next level issue type 2]

---

## 📊 Definition of Done

Your PR is ready to merge when:

✅ **Code Changes**
- All implementation steps completed
- Code follows PatternFly patterns
- No TypeScript/ESLint errors
- Code properly formatted

✅ **Testing**
- All acceptance criteria met
- All tests passing
- No reduction in code coverage
- Manual testing completed

✅ **Documentation**
- All code documented
- Examples provided
- README updated if needed

✅ **Review**
- Self-review completed
- PR description filled out
- Screenshots/videos added (if UI changes)
- Maintainer review passed

---

## 🏷️ Issue Metadata

**Category:** [Testing/Documentation/Accessibility/Component/Tooling]

**Component:** [Component name, if applicable]

**Prerequisites:**
- Basic knowledge of [Technology 1]
- Familiarity with [Concept 1]
- [Optional: Previous experience with X]

**No Prerequisites Needed:**
- ❌ Deep architecture knowledge
- ❌ Advanced algorithm knowledge
- ❌ Specific tool access
- ❌ Years of experience

**Time Estimate Breakdown:**
- Setup: 30 minutes
- Implementation: [X] hours
- Testing: [Y] hours
- Documentation: [Z] minutes
- PR creation: 15 minutes

**Success Indicators:**
- [Measurable outcome 1]
- [Measurable outcome 2]
- [Measurable outcome 3]

---

## 🎯 Ready to Start?

Comment below to let us know you're working on this! We'll assign it to you and provide support throughout.

Good luck, and happy coding! 🚀
```

### Phase 4: Issue Validation

Before finalizing the issue:

1. **Self-Review Checklist**
   - [ ] Title is clear and descriptive
   - [ ] Problem statement is well-defined
   - [ ] Solution is achievable for a beginner
   - [ ] Implementation guide is step-by-step
   - [ ] Code examples are complete and correct
   - [ ] Acceptance criteria are specific and testable
   - [ ] Resources are relevant and accessible
   - [ ] Time estimate is realistic (2-8 hours)
   - [ ] Prerequisites are minimal
   - [ ] Testing instructions are clear
   - [ ] All links work
   - [ ] No assumptions about prior knowledge

2. **Complexity Verification**

   Ensure the issue scores well on this scale:

   | Criteria | Score (1-5) | Target |
   |----------|-------------|---------|
   | Scope clarity | [X] | 4-5 |
   | Implementation clarity | [X] | 4-5 |
   | Testing clarity | [X] | 4-5 |
   | Self-containment | [X] | 4-5 |
   | Beginner-friendliness | [X] | 4-5 |
   | Learning value | [X] | 4-5 |

   **Overall Suitability Score:** [X]/30 (aim for 24+)

3. **Label Recommendations**

   Suggest appropriate labels:
   - ✅ `good-first-issue` (always)
   - `documentation` (if docs-related)
   - `accessibility` (if a11y-related)
   - `testing` (if test-related)
   - `typescript` (if TS-related)
   - `component: [name]` (if component-specific)
   - `help wanted` (to encourage contributions)
   - `mentor available` (if mentorship offered)

### Phase 5: Final Output Generation

Provide the complete issue in markdown format, ready to paste into GitHub.

Additionally provide:

```markdown
## Issue Summary for Maintainers

**Opportunity Type:** [Testing/Documentation/Accessibility/etc.]
**Target Component/Area:** [Component or area name]
**Complexity:** ⭐ [Beginner/Easy/Moderate]
**Time Estimate:** [2-8 hours]
**Suitability Score:** [X]/30

**Why This is a Good First Issue:**
- [Reason 1]
- [Reason 2]
- [Reason 3]

**Mentorship Points:**
- [Area where contributor might need guidance 1]
- [Area where contributor might need guidance 2]

**Success Metrics:**
- [How to measure if this was successful]

**Follow-up Opportunities:**
After completing this, the contributor could tackle:
- [Related issue 1]
- [Related issue 2]
```

## Critical Requirements

✅ **DO:**
- Scan codebase comprehensively for opportunities
- Evaluate multiple candidates before choosing
- Assess complexity honestly (must be truly beginner-friendly)
- Provide complete, working code examples
- Include step-by-step implementation guide
- Specify exact files and line numbers where helpful
- List all acceptance criteria explicitly
- Provide comprehensive testing instructions
- Link to relevant documentation and examples
- Estimate time realistically (2-8 hours)
- Suggest appropriate labels
- Include mentorship guidance
- Explain what the contributor will learn
- Provide troubleshooting tips
- Make it welcoming and encouraging
- Use `mcp__pf-mcp__usePatternFlyDocs` for accurate patterns
- Verify all code examples work
- Include both manual and automated testing
- Provide similar examples from codebase
- Be specific about prerequisites (but keep them minimal)

✅ **ALWAYS INCLUDE:**
- Clear problem statement
- Step-by-step implementation guide
- Complete code examples
- Testing instructions
- Acceptance criteria checklist
- Learning outcomes
- Helpful resources
- Getting started guide
- Mentorship section
- Definition of done

❌ **DON'T:**
- Create issues that are too complex for beginners
- Assume deep prior knowledge
- Skip code examples
- Be vague about implementation steps
- Omit testing instructions
- Forget accessibility considerations
- Provide outdated or incorrect information
- Make issues too large (should be completable in 2-8 hours)
- Create issues with unclear acceptance criteria
- Forget to link to relevant docs/examples
- Include issues that block other work
- Recommend patterns that don't match PatternFly guidelines
- Skip the complexity validation
- Make assumptions about file locations without checking
- Provide incomplete examples
- Use jargon without explanation

❌ **NEVER:**
- Generate issues requiring architectural changes
- Create issues needing deep system knowledge
- Make issues that depend on unreleased features
- Suggest complex algorithm implementations
- Create issues requiring special access/tools
- Skip the opportunity scanning phase
- Guess at implementation details - always verify
- Provide code that doesn't follow PatternFly patterns

## Output Format

Generate a complete, ready-to-use GitHub issue that:

1. **Is immediately actionable** - A beginner can start right away
2. **Is self-contained** - All information needed is in the issue
3. **Is welcoming** - Encourages first-time contributors
4. **Is comprehensive** - Covers all aspects from start to finish
5. **Is realistic** - Can be completed in 2-8 hours
6. **Is valuable** - Provides real learning and impact

The issue should be formatted in markdown, ready to copy/paste into GitHub Issues.

Include the maintainer summary at the end for internal review.

## Success Criteria

A well-generated "Good First Issue" should:

✅ Receive positive engagement from new contributors
✅ Be completed successfully by someone with minimal experience
✅ Teach valuable skills applicable to future contributions
✅ Result in merged PRs that improve the codebase
✅ Create a welcoming onboarding experience
✅ Build contributor confidence
✅ Follow PatternFly patterns accurately
✅ Provide clear path to success

Remember: The goal is to create an exceptional onboarding experience that turns first-time contributors into long-term community members! 🎉
