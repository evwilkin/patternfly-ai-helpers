---
description: Analyze whether something is suitable for a "Good First Issue"
---

# Issue Opportunity Analyzer

You are analyzing code, features, or tasks to determine if they are suitable for a "Good First Issue" for new contributors to PatternFly.

## Input

The user will provide:
- A file path to analyze
- A component or feature description
- A specific task or improvement idea
- An area of the codebase to evaluate
- An existing GitHub issue to assess

## Your Task

### Phase 1: Comprehensive Analysis

1. **Read and Understand the Target**

   If given a file:
   - Read the complete file(s)
   - Understand the current implementation
   - Identify dependencies
   - Map related files
   - Check existing tests
   - Review related documentation

   If given a description:
   - Search codebase for relevant files
   - Understand scope of changes
   - Identify affected components
   - Map dependencies
   - Find similar implementations

2. **Use PatternFly Documentation**

   Use `mcp__pf-mcp__usePatternFlyDocs` to:
   - Get component guidelines
   - Review best practices
   - Find similar examples
   - Check accessibility requirements
   - Understand testing patterns

### Phase 2: Suitability Evaluation

Evaluate the opportunity across these dimensions:

#### 1. Scope and Complexity Assessment

**Scope Evaluation:**

```markdown
## Scope Analysis

**What needs to change:**
- [ ] [Specific change 1]
- [ ] [Specific change 2]
- [ ] [Specific change 3]

**Files affected:** [X] file(s)
- `[file path 1]` - [type of change]
- `[file path 2]` - [type of change]

**Lines of code (estimate):**
- To add: ~[X] lines
- To modify: ~[Y] lines
- To remove: ~[Z] lines
- **Total impact:** ~[X+Y+Z] lines

**Scope Score:** [1-5]
- 5 = Very small, focused change
- 4 = Small, well-defined change
- 3 = Medium scope, manageable
- 2 = Large scope, multiple areas
- 1 = Very large, complex scope

**Justification:**
[Explain the scope rating]
```

**Complexity Evaluation:**

```markdown
## Complexity Analysis

**Technical Complexity:**

| Aspect | Level (1-5) | Explanation |
|--------|-------------|-------------|
| React concepts | [X] | [Why] |
| TypeScript usage | [X] | [Why] |
| State management | [X] | [Why] |
| Component composition | [X] | [Why] |
| Styling/CSS | [X] | [Why] |
| Testing requirements | [X] | [Why] |
| Build/tooling | [X] | [Why] |
| Documentation | [X] | [Why] |

**Overall Technical Complexity:** [X]/40

**Complexity Rating:**
- 1-10: ⭐ Beginner (Perfect for first contribution)
- 11-20: ⭐⭐ Easy (Good for first issue)
- 21-30: ⭐⭐⭐ Moderate (Needs some experience)
- 31-40: ⭐⭐⭐⭐ Advanced (Not suitable for first issue)

**Current Rating:** [Symbol] ([Description])
```

**Cognitive Complexity:**

```markdown
## Cognitive Load Assessment

**Concepts Required:**
- [ ] Basic React hooks
- [ ] TypeScript types
- [ ] Component patterns
- [ ] Testing with React Testing Library
- [ ] Accessibility principles
- [ ] Git workflow
- [ ] [Other concept 1]
- [ ] [Other concept 2]

**Domain Knowledge Needed:**
- [ ] PatternFly design system
- [ ] Component API design
- [ ] [Specific domain 1]
- [ ] [Specific domain 2]

**Cognitive Complexity Score:** [1-5]
- 5 = Minimal context needed
- 4 = Basic React/TS knowledge sufficient
- 3 = Need to understand some patterns
- 2 = Need to understand architecture
- 1 = Need deep system knowledge

**Justification:**
[Explain cognitive complexity]
```

#### 2. Prerequisites Analysis

```markdown
## Prerequisites Assessment

### Required Skills

**Must Have:**
- [X] Basic JavaScript/TypeScript
- [X] Git basics (clone, branch, commit, push)
- [X] [Required skill 1]
- [X] [Required skill 2]

**Should Have:**
- [ ] React fundamentals
- [ ] Testing basics
- [ ] [Helpful skill 1]
- [ ] [Helpful skill 2]

**Nice to Have:**
- [ ] PatternFly experience
- [ ] Accessibility knowledge
- [ ] [Optional skill 1]

### Knowledge Prerequisites

**React Knowledge:**
- Level needed: [Beginner/Intermediate/Advanced]
- Specific concepts: [list concepts]
- Can be learned while doing: [Yes/No]

**TypeScript Knowledge:**
- Level needed: [Beginner/Intermediate/Advanced]
- Specific concepts: [list concepts]
- Can be learned while doing: [Yes/No]

**PatternFly Knowledge:**
- Level needed: [None/Beginner/Intermediate]
- Specific patterns: [list patterns]
- Documentation available: [Yes/No - with links]

**Testing Knowledge:**
- Level needed: [None/Beginner/Intermediate]
- Testing types: [Unit/Integration/E2E]
- Examples to follow: [Yes/No - with paths]

**Accessibility Knowledge:**
- Level needed: [None/Beginner/Intermediate]
- Specific requirements: [list requirements]
- Guidelines provided: [Yes/No - with links]

### Tool Requirements

**Required Tools:**
- [X] Node.js and npm
- [X] Git
- [X] Code editor
- [ ] [Other tool 1]
- [ ] [Other tool 2]

**Special Access Needed:**
- [ ] Figma access
- [ ] Design tokens
- [ ] Specific test environment
- [ ] None ✅

**Prerequisites Score:** [1-5]
- 5 = Minimal prerequisites (just basic dev setup)
- 4 = Basic React/TS knowledge needed
- 3 = Some specialized knowledge needed
- 2 = Multiple specialized areas
- 1 = Expert-level knowledge required

**Suitability for Beginners:** [High/Medium/Low]
```

#### 3. Blockers and Dependencies

```markdown
## Potential Blockers

### Technical Blockers

**Dependency Issues:**
- [ ] Depends on unreleased features
- [ ] Blocked by open PRs
- [ ] Requires infrastructure changes
- [ ] Needs dependency upgrades
- [ ] Breaking changes required
- [ ] None identified ✅

**If blockers exist:**
- Blocker 1: [Description] - [Can be resolved? How?]
- Blocker 2: [Description] - [Can be resolved? How?]

**Architecture Blockers:**
- [ ] Requires architectural decisions
- [ ] Needs design review
- [ ] Multiple approaches possible
- [ ] Unclear requirements
- [ ] None identified ✅

**Testing Blockers:**
- [ ] No test infrastructure
- [ ] Difficult to test
- [ ] Requires manual testing only
- [ ] Missing test utilities
- [ ] None identified ✅

### Process Blockers

**Documentation Blockers:**
- [ ] Guidelines unclear
- [ ] No examples to follow
- [ ] Conflicting patterns
- [ ] None identified ✅

**Review Blockers:**
- [ ] Subject matter expert needed
- [ ] Design approval needed
- [ ] Multiple stakeholders
- [ ] None identified ✅

**Blocker Score:** [1-5]
- 5 = No blockers at all
- 4 = Minor blockers, easily addressed
- 3 = Some blockers, need guidance
- 2 = Significant blockers
- 1 = Major blockers, not suitable

### Dependencies

**Code Dependencies:**
- Depends on [X] other components/files
- Dependencies are: [stable/unstable]
- Can work independently: [Yes/No]

**Knowledge Dependencies:**
- Must understand [concept 1]
- Must understand [concept 2]
- Documentation available: [Yes/No]

**Temporal Dependencies:**
- Blocks other work: [Yes/No]
- Blocked by other work: [Yes/No]
- Can proceed immediately: [Yes/No]
```

#### 4. Impact vs. Effort Analysis

```markdown
## Impact Assessment

### User Impact

**Who Benefits:**
- [X] End users of PatternFly components
- [X] Developers using PatternFly
- [X] Contributors to PatternFly
- [X] [Other stakeholder]

**How They Benefit:**
- [Specific benefit 1]
- [Specific benefit 2]
- [Specific benefit 3]

**Impact Visibility:**
- User-facing: [Yes/No]
- Developer-facing: [Yes/No]
- Internal improvement: [Yes/No]

**Impact Scope:**
- Affects [X] component(s)
- Used by [estimate] applications
- Impact level: [High/Medium/Low]

**User Impact Score:** [1-5]
- 5 = High impact, many users benefit
- 4 = Good impact, clear benefits
- 3 = Moderate impact
- 2 = Low impact, niche benefit
- 1 = Minimal impact

### Codebase Impact

**Code Quality Impact:**
- Improves maintainability: [Yes/No]
- Reduces technical debt: [Yes/No]
- Adds test coverage: [Yes/No]
- Improves documentation: [Yes/No]
- Enhances accessibility: [Yes/No]

**Long-term Value:**
- [Value 1]
- [Value 2]
- [Value 3]

**Codebase Impact Score:** [1-5]
- 5 = Significant quality improvement
- 4 = Good improvement
- 3 = Moderate improvement
- 2 = Minor improvement
- 1 = Negligible improvement

### Effort Estimation

**Time Breakdown:**
- Understanding context: [X] hours
- Implementation: [Y] hours
- Writing tests: [Z] hours
- Documentation: [W] hours
- PR process: [V] hours
- **Total:** [X+Y+Z+W+V] hours

**Ideal Range for Good First Issue:** 2-8 hours
**This Task:** [X] hours - [Within/Above/Below] ideal range

**Effort Score:** [1-5]
- 5 = 2-4 hours (quick win)
- 4 = 4-6 hours (good size)
- 3 = 6-8 hours (manageable)
- 2 = 8-12 hours (too large)
- 1 = 12+ hours (way too large)

### Impact/Effort Ratio

**Calculation:**
- Impact: ([User Impact] + [Codebase Impact]) / 2 = [X]
- Effort: [Effort Score] = [Y]
- **Ratio:** [X]/[Y] = [Z]

**Interpretation:**
- > 1.5 = Excellent (high impact, low effort)
- 1.0-1.5 = Good (balanced)
- 0.7-1.0 = Acceptable (effort justified)
- < 0.7 = Poor (effort outweighs impact)

**This Opportunity:** [Z] - [Excellent/Good/Acceptable/Poor]
```

#### 5. Learning Value Assessment

```markdown
## Learning Opportunity Analysis

### Skills Developer Will Gain

**Technical Skills:**
- [Skill 1] - [How they'll learn it]
- [Skill 2] - [How they'll learn it]
- [Skill 3] - [How they'll learn it]

**PatternFly-Specific Skills:**
- [Skill 1] - [Why it's valuable]
- [Skill 2] - [Why it's valuable]

**General Skills:**
- Open source contribution workflow
- Code review process
- Testing best practices
- [Other transferable skill]

**Learning Value Score:** [1-5]
- 5 = Excellent learning opportunity
- 4 = Good learning experience
- 3 = Some learning value
- 2 = Limited learning
- 1 = Minimal learning value

### Teaching Opportunities

**Mentorship Points:**

Areas where contributor will likely need guidance:
1. [Area 1] - [Type of help needed]
2. [Area 2] - [Type of help needed]
3. [Area 3] - [Type of help needed]

**Self-Service Potential:**
- Can contributor self-serve: [High/Medium/Low]
- Documentation available: [Yes/No - with links]
- Examples to follow: [Yes/No - with paths]

**Mentorship Requirements:**
- Time needed from maintainer: [Low/Medium/High]
- Frequency of check-ins: [None/Occasional/Frequent]
- Specialized knowledge required: [Yes/No]
```

### Phase 3: Overall Suitability Scoring

```markdown
## Comprehensive Suitability Score

| Criteria | Score (1-5) | Weight | Weighted Score |
|----------|-------------|---------|----------------|
| Scope Clarity | [X] | 2.0 | [X * 2.0] |
| Technical Complexity (inverted) | [6-X] | 2.5 | [(6-X) * 2.5] |
| Cognitive Complexity (inverted) | [6-X] | 2.0 | [(6-X) * 2.0] |
| Prerequisites (inverted) | [6-X] | 2.0 | [(6-X) * 2.0] |
| No Blockers | [X] | 2.5 | [X * 2.5] |
| Impact/Effort Ratio | [X] | 1.5 | [X * 1.5] |
| Learning Value | [X] | 1.5 | [X * 1.5] |

**Total Weighted Score:** [Sum] / 70 = [%]

**Suitability Rating:**
- 85-100%: ✅✅✅ **Excellent** - Ideal for good first issue
- 70-84%: ✅✅ **Good** - Suitable with minor adjustments
- 55-69%: ✅ **Acceptable** - Can work with proper support
- 40-54%: ⚠️ **Marginal** - Needs significant simplification
- <40%: ❌ **Not Suitable** - Too complex for first issue

**This Opportunity:** [X]% - [Rating]

### Recommendation

**Primary Recommendation:**
[Clear statement: "This IS/IS NOT suitable for a Good First Issue"]

**Reasoning:**
[3-4 sentences explaining the recommendation based on the scores and analysis]

**Strengths:**
- ✅ [Strength 1]
- ✅ [Strength 2]
- ✅ [Strength 3]

**Concerns:**
- ⚠️ [Concern 1]
- ⚠️ [Concern 2]
- ⚠️ [Concern 3]
```

### Phase 4: Improvement Suggestions

If the opportunity is marginal or not suitable, provide specific recommendations:

```markdown
## How to Make This Suitable

### If Too Complex: Breaking Down Strategy

**Original Scope:**
[Description of full scope]

**Breakdown Strategy:**

**Phase 1 Issue (Good First Issue):** ⭐
- Scope: [Simplified scope]
- Deliverable: [Specific deliverable]
- Time: [2-4 hours]
- Why it's better: [Explanation]

**Phase 2 Issue (Follow-up):** ⭐⭐
- Scope: [Next piece]
- Deliverable: [Specific deliverable]
- Time: [4-6 hours]
- Builds on: Phase 1

**Phase 3 Issue (If needed):** ⭐⭐⭐
- Scope: [Final piece]
- Deliverable: [Specific deliverable]
- Time: [6-8 hours]
- Builds on: Phase 1 & 2

**Benefits of Breaking Down:**
- Each phase is independently valuable
- Contributor builds knowledge progressively
- Easier to review and merge
- Less risk of abandonment

### If Prerequisites Too High: Simplification Strategy

**Current Prerequisites:**
[List current prerequisites]

**Simplification Approaches:**

1. **Add More Documentation**
   - Document [concept 1] with examples
   - Create guide for [concept 2]
   - Link to [existing resource]

2. **Provide More Examples**
   - Point to similar implementation at [path]
   - Create code template
   - Add inline comments explaining patterns

3. **Reduce Scope**
   - Remove [complex part 1]
   - Simplify [complex part 2]
   - Make [aspect 3] optional

4. **Add Mentorship**
   - Assign mentor for [area 1]
   - Schedule kick-off call
   - Provide checkpoint reviews

### If Blockers Exist: Resolution Strategy

**Blocker 1:** [Description]
- **Resolution:** [How to resolve]
- **Timeline:** [When can be resolved]
- **Can proceed without resolution:** [Yes/No]

**Blocker 2:** [Description]
- **Resolution:** [How to resolve]
- **Timeline:** [When can be resolved]
- **Can proceed without resolution:** [Yes/No]

**Recommended Actions:**
1. [Action 1]
2. [Action 2]
3. [Action 3]

### If Impact Too Low: Enhancement Strategy

**Ways to Increase Impact:**

1. **Expand Scope (Carefully):**
   - Also apply to [component 2]
   - Add [related feature]
   - Time impact: +[X] hours

2. **Increase Visibility:**
   - Add to showcase
   - Document in migration guide
   - Highlight in release notes

3. **Connect to Larger Initiative:**
   - Part of [initiative name]
   - Enables [future work]
   - Supports [goal]

**Recommended Enhancement:**
[Specific recommendation that keeps it beginner-friendly while increasing impact]
```

### Phase 5: Mentorship Approach

```markdown
## Recommended Mentorship Strategy

### Onboarding Approach

**Initial Contact:**
1. Welcome contributor
2. Verify understanding of scope
3. Share [specific resource 1]
4. Share [specific resource 2]
5. Offer kick-off call if helpful

**Setup Guidance:**
- Help with: [specific setup step 1]
- Point to: [documentation for step 2]
- Verify: [environment is working]

### During Implementation

**Check-in Points:**

**After Initial Setup (Day 1-2):**
- Verify environment working
- Confirm understanding of task
- Answer initial questions

**After First Implementation (Day 3-5):**
- Review approach
- Provide early feedback
- Course-correct if needed

**Before PR Submission:**
- Pre-review checklist
- Ensure tests passing
- Documentation complete

**Expected Questions:**

**Likely Question 1:** [Question]
- **Answer:** [Clear answer with example]

**Likely Question 2:** [Question]
- **Answer:** [Clear answer with example]

**Likely Question 3:** [Question]
- **Answer:** [Clear answer with example]

### Review Strategy

**First Review Focus:**
- ✅ Functionality works
- ✅ Tests pass
- ✅ Follows patterns
- 📚 Teaching moments (not blocking):
  - [Learning point 1]
  - [Learning point 2]

**Second Review (if needed):**
- ✅ Feedback addressed
- ✅ Code quality
- ✅ Documentation

**Common Pitfalls to Watch For:**
1. [Pitfall 1] - [How to guide them]
2. [Pitfall 2] - [How to guide them]
3. [Pitfall 3] - [How to guide them]

### Success Criteria

**Contributor Success:**
- Completes the issue
- Learns [key concept]
- Feels supported
- Wants to contribute again

**Maintainer Success:**
- Reasonable mentorship time investment
- Quality contribution
- Positive experience
- Contributor becomes community member
```

### Phase 6: Alternative Approaches

If not suitable as-is, suggest alternatives:

```markdown
## Alternative Recommendations

### Alternative 1: [Different Scope]

**What to do instead:**
[Description of alternative approach]

**Why it's better:**
- [Reason 1]
- [Reason 2]
- [Reason 3]

**Suitability Score:** [X]% - [Rating]

### Alternative 2: [Different Component/Area]

**What to do instead:**
[Description of alternative]

**Why it's better:**
- [Reason 1]
- [Reason 2]
- [Reason 3]

**Suitability Score:** [X]% - [Rating]

### Alternative 3: [Related but Simpler]

**What to do instead:**
[Description of alternative]

**Why it's better:**
- [Reason 1]
- [Reason 2]
- [Reason 3]

**Suitability Score:** [X]% - [Rating]

**Recommended Alternative:** [Number] - [Brief explanation]
```

## Critical Requirements

✅ **DO:**
- Analyze all files mentioned thoroughly
- Evaluate complexity honestly and objectively
- Consider the contributor's perspective
- Assess impact realistically
- Identify specific blockers
- Provide concrete improvement suggestions
- Use the scoring rubric consistently
- Consider learning value
- Think about mentorship requirements
- Suggest alternatives if not suitable
- Use `mcp__pf-mcp__usePatternFlyDocs` for accurate information
- Verify file paths and code references
- Be specific about prerequisites
- Estimate time realistically
- Consider both user and codebase impact
- Evaluate if it can be broken down
- Think about documentation needs
- Consider testing complexity
- Assess accessibility requirements
- Provide actionable recommendations

✅ **ALWAYS INCLUDE:**
- Comprehensive suitability score
- Clear recommendation (suitable or not)
- Specific reasoning for recommendation
- Strengths and concerns
- Breakdown strategy if too complex
- Mentorship approach
- Alternative suggestions if not suitable
- Realistic time estimates

❌ **DON'T:**
- Be overly optimistic about complexity
- Ignore prerequisites
- Overlook blockers
- Assume contributor knowledge
- Skip impact assessment
- Forget about mentorship needs
- Provide vague recommendations
- Ignore the learning value
- Skip the effort estimation
- Forget to suggest alternatives
- Make assumptions without verifying code
- Recommend patterns that don't match PatternFly
- Underestimate time requirements
- Overlook testing complexity

❌ **NEVER:**
- Recommend something too complex just because it's needed
- Ignore significant blockers
- Skip the detailed analysis
- Provide scores without justification
- Recommend breaking the issue into dependent pieces
- Suggest issues requiring architectural knowledge
- Ignore accessibility implications
- Forget about documentation requirements

## Evaluation Framework Summary

Use this decision tree:

```
Is scope clear and well-defined?
├─ No → ❌ Not suitable (need requirements clarification)
└─ Yes ↓

Is technical complexity manageable? (Score 4-5 on inverted scale)
├─ No → Can it be simplified?
│       ├─ Yes → ✅ Suitable with modifications
│       └─ No → ❌ Not suitable (suggest alternatives)
└─ Yes ↓

Are prerequisites minimal? (Score 4-5)
├─ No → Can we provide better documentation/examples?
│       ├─ Yes → ✅ Suitable with more guidance
│       └─ No → ❌ Not suitable (too specialized)
└─ Yes ↓

Are there blockers? (Score 4-5)
├─ Yes → Can they be resolved first?
│       ├─ Yes → ✅ Suitable after resolution
│       └─ No → ❌ Not suitable now
└─ No ↓

Is effort reasonable? (2-8 hours)
├─ No → Can it be broken down?
│       ├─ Yes → ✅ Create smaller issues
│       └─ No → ❌ Not suitable
└─ Yes ↓

Is impact/effort ratio good? (>0.7)
├─ No → Can impact be increased?
│       ├─ Yes → ✅ Suitable with enhancement
│       └─ No → ⚠️ Marginal (reconsider)
└─ Yes ↓

✅✅✅ EXCELLENT GOOD FIRST ISSUE!
```

## Output Format

Provide a comprehensive analysis structured as:

1. **Executive Summary** (2-3 sentences)
   - Clear recommendation
   - Overall suitability score
   - Key reason

2. **Detailed Analysis** (using all Phase 2 sections)
   - Scope and complexity
   - Prerequisites
   - Blockers and dependencies
   - Impact vs. effort
   - Learning value

3. **Suitability Score** (Phase 3)
   - Numerical scores
   - Final percentage
   - Rating and recommendation

4. **Improvement Suggestions** (Phase 4, if needed)
   - How to make it suitable
   - Specific modifications
   - Breaking down strategy

5. **Mentorship Approach** (Phase 5)
   - Onboarding strategy
   - Expected questions
   - Review strategy

6. **Alternatives** (Phase 6, if not suitable)
   - Other opportunities
   - Why they're better
   - Suitability scores

The analysis should be thorough, honest, and actionable.

## Success Criteria

A good analysis will:

✅ Provide clear, justified recommendation
✅ Score objectively using the rubric
✅ Identify all significant concerns
✅ Suggest concrete improvements
✅ Consider the contributor experience
✅ Provide alternatives if needed
✅ Be actionable for maintainers
✅ Help create better good first issues

Remember: It's better to honestly say something ISN'T suitable than to set a new contributor up for frustration! 🎯
