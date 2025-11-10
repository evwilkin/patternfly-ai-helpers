# Issues Plugin

Generate well-documented "Good First Issue" GitHub issues to help onboard new contributors to PatternFly.

## Available Commands

### `/generate-good-first-issue`

Scans codebase for improvement opportunities and creates detailed, beginner-friendly GitHub issues.

**Usage:**
```
/generate-good-first-issue [area or component]
```

**What it does:**
1. Scans for common improvement opportunities (missing tests, docs, accessibility)
2. Evaluates complexity and impact
3. Creates detailed issue with clear steps
4. Provides code guidance and examples
5. Suggests appropriate labels
6. Includes acceptance criteria

**Output:**
- Complete GitHub issue markdown
- Issue title and description
- Step-by-step implementation guide
- Code examples and hints
- Helpful resources for beginners
- Estimated difficulty level

---

### `/analyze-issue-opportunity`

Analyzes a specific area to determine if it's suitable for a "Good First Issue".

**Usage:**
```
/analyze-issue-opportunity [file or feature description]
```

**What it does:**
1. Evaluates scope and complexity
2. Assesses prerequisite knowledge needed
3. Identifies potential blockers
4. Estimates time to complete
5. Suggests mentorship points

---

## Related Documentation

- [PatternFly Contributing Guide](https://www.patternfly.org/contribute/about)
- [GitHub Good First Issue Best Practices](https://github.blog/2020-01-22-how-we-write-github-issues/)
