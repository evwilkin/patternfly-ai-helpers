# PatternFly Design Review Framework

## Purpose
This framework provides comprehensive instructions for evaluating Figma designs against PatternFly design guidelines and best practices. The analysis should be detailed, accurate, and actionable for designers before handoff to development.

---

## Review Process

### Phase 1: Data Extraction
Use Figma MCP tools to extract accurate component data rather than relying solely on screenshots.

**Required Steps:**
1. Get screenshot of the design using `mcp__figma__get_screenshot`
2. Get design context (component structure) using `mcp__figma__get_design_context` with `forceCode=true`
   - If this fails, use `mcp__figma__get_metadata` as fallback to get component structure
3. Fetch relevant PatternFly documentation using `mcp__pf-mcp__usePatternFlyDocs` for components identified in the design

**Do NOT:**
- Rely on visual inspection alone
- Guess at component properties
- Make assumptions about text content that can be extracted from Figma data
- Flag issues based on insufficient data - if you cannot verify a property from the available data, note it as "Unable to verify" rather than assuming it's incorrect

**Critical Analysis Rules:**
- **Position coordinates (x, y):** Use these to determine alignment. If x=0 or small values, element is LEFT-aligned. If x is close to container width, it's RIGHT-aligned.
- **Component properties:** Check Figma component properties/toggles (e.g., `sortable=true`, `state="selected"`, `variant="primary"`) to understand what features are present. These properties control visibility of child elements like icons, badges, etc.
- **Property-based verification:** If a component has `sortable=true`, it includes sort icons. If `showBadge=true`, it has a badge. Use properties, not assumptions.
- **Verification requirement:** Only flag an issue if you have explicit data showing the problem. If metadata doesn't provide enough detail, state "Cannot verify from available data" in your analysis.

---

### Phase 2: Component Identification

**Create a complete inventory of PatternFly components used:**

List format:
```
1. **ComponentName** - Brief description of usage
2. **ComponentName** - Brief description of usage
...
```

Include ALL components from the PatternFly design kit, including:
- Primary components (Cards, Tables, Forms, etc.)
- Layout components (Page, Masthead, Navigation, etc.)
- Helper components (Icons, Dividers, Spacers, etc.)
- Form components (Buttons, Inputs, Checkboxes, etc.)

---

### Phase 3: Component Property Analysis

For EACH component with issues, extract and analyze using this EXACT template:

**Component Analysis Template:**
```markdown
### [Number]. [Component Name] ([Severity Level])

**Properties Configured:**
```
property: value
property: value
```

**[Child Component Name] Components:** (if applicable)
```
1. property="value" property="value"
2. property="value" property="value"
```

**Analysis:**

✅ **Correct Configuration:**
- Property name - Why it's correct (reference guideline if relevant)
- Property name - Why it's correct

❌ **[Severity] Issue - [Brief Description]:**
- Current state from Figma data
- Why this is a problem
- Impact on users

**PatternFly Guideline:**
> "Direct quote from the PatternFly documentation"

❌ **[Severity] Issue - [Next Issue]:** (if multiple issues)
- Details

**How to Fix in Figma:**
1. Specific step with exact values
2. Next step
3. Final step

---
```

**Severity Levels for Component Headers:**
- Use format: `### 1. ComponentName (Critical)` or `### 1. ComponentName (Moderate)` or `### 1. ComponentName (Minor)`
- Only include severity if there ARE issues
- If no issues, component goes in "Correctly Configured Components" section instead

---

### Phase 4: Guideline Comparison

**For each component, check against PatternFly guidelines:**

1. **Component Selection**
   - Is the correct component type used for the use case?
   - Are there more appropriate alternatives?

2. **Property Configuration**
   - Are properties set appropriately?
   - Are there conflicting property values?
   - Are required properties present?

3. **Content & Labels**
   - Are placeholder texts still present?
   - Are labels meaningful and descriptive?
   - Is terminology consistent with PatternFly patterns?

4. **Visual Hierarchy**
   - Does component sizing follow guidelines?
   - Is spacing correct (check against design tokens)?
   - Are states properly configured (selected, disabled, hover)?

5. **Accessibility Considerations**
   - Are color contrasts appropriate?
   - Are required labels present?
   - Are interactive elements properly indicated?

6. **Responsive Behavior**
   - Are overflow behaviors configured?
   - Are mobile/tablet variants considered?
   - Are breakpoints appropriate?

---

## Analysis Criteria

### Issue Severity Levels

**Critical:**
- Violates core PatternFly pattern
- Creates significant usability problems
- Requires major restructuring
- Examples: Wrong component type, broken navigation hierarchy, missing required elements

**Major:**
- Misses important pattern recommendations
- Impacts user experience
- Requires notable changes
- Examples: Missing selection affordances, incorrect component variants, improper placement

**Moderate:**
- Deviates from best practices
- Reduces clarity or consistency
- Requires minor restructuring
- Examples: Missing group labels, inconsistent organization, suboptimal spacing

**Minor:**
- Enhancement opportunities
- Consistency improvements
- Optional optimizations
- Examples: Could use color variants, could add icons, could improve labels

---

## Report Structure

**IMPORTANT**: Each major section must be separated by a horizontal rule `---`

### Required Sections (in order):

#### 1. Report Header
```markdown
## Design Reviewed
- **Figma URL:** `[full Figma URL]`
- **Design Type:** [Brief description]
- **Date:** [YYYY-MM-DD]

---
```

#### 2. Complete List of PatternFly 6 Components Used
```markdown
## Complete List of PatternFly 6 Components Used

1. **ComponentName** - Brief description
2. **ComponentName** - Brief description
...

---
```

#### 3. Configuration Issues with PatternFly Components
```markdown
## Configuration Issues with PatternFly Components

### 1. Component Name (Severity Level)

**Properties Configured:**
```
property: value
property: value
```

**Child Components (if applicable):**
```
component details
```

**Analysis:**

✅ **Correct Configuration:**
- What's correct

❌ **Issue - Description (Severity):**
- Current state
- Problem description

**PatternFly Guideline:**
> "Quote from guideline"

**How to Fix in Figma:**
1. Step 1
2. Step 2

---

### 2. Next Component...

---
```

#### 4. Summary: Component Configuration Issues
```markdown
## Summary: Component Configuration Issues

| Component | Property | Current Value | Issue | Recommendation |
|-----------|----------|---------------|-------|----------------|
| ComponentName | property | value | description | fix |

---
```

#### 5. Correctly Configured Components
```markdown
## Correctly Configured Components

The following components demonstrate proper PatternFly implementation:

### ✅ Component Name
- **Property:** Description
- **Configuration:** Details

### ✅ Next Component...

---
```

#### 6. Overall Assessment
```markdown
## Overall Assessment

### Strengths
[Bulleted list of what's done well]

### Areas for Improvement
[Bulleted list with severity indicators 🔴 Critical, 🟡 Moderate, 🟢 Minor]

### Development Readiness
**Status:** [Ready/Not ready/Ready with modifications]

**Required Actions:**
1. Action 1
2. Action 2

**Estimated Effort:** [Low/Medium/High]

---
```

#### 7. PatternFly Guideline References
```markdown
## PatternFly Guideline References

- **Component Name Design Guidelines:** https://www.patternfly.org/components/component-name/design-guidelines
- **Component Name Accessibility:** https://www.patternfly.org/components/component-name/accessibility
...
```

---

## Report Format Guidelines

### Report Header

Every report must begin with:
```markdown
## Design Reviewed
- **Figma URL:** `[full Figma URL]`
- **Design Type:** [Brief description of design type]
- **Date:** [Current date in YYYY-MM-DD format]
```

**Important:**
- Use the actual current date (e.g., 2025-10-20), not a placeholder or old date
- Design Type should briefly describe what's being reviewed (e.g., "Desktop Page with Horizontal Navigation", "Catalog View", "Form with Validation")

### Tone & Audience
- **Audience:** Designers (not developers)
- **Focus:** Visual design decisions, not code implementation
- **Tone:** Constructive, specific, actionable
- **Avoid:** Code snippets (unless illustrating component properties)

### Content Requirements
- Use actual data from Figma MCP (text values, property settings)
- Quote PatternFly guidelines when citing violations
- Provide visual context with emoji indicators (✅ ❌ ℹ️ ⚠️)
- Include specific property values in code blocks for clarity
- Reference design token names when discussing spacing/sizing

### Formatting
- Use clear headings and subheadings
- Use tables for comparative data
- Use code blocks for component properties
- Use blockquotes for PatternFly guideline quotes
- Use bullet points for lists
- Use numbered lists for sequential steps

---

## Key Analysis Focus Areas

### Navigation Components
- Breadcrumb hierarchy and labels
- Navigation type appropriateness (vertical vs horizontal)
- Navigation item labels and states
- Overflow behavior

### Page Layout
- Masthead configuration
- Page section organization
- Header/footer usage
- Spacing and padding

### Data Display
- Card configurations
- Table structures
- List patterns
- Selection patterns

### Forms & Inputs
- Input types and labels
- Validation states
- Helper text
- Form organization

### Interactive Elements
- Button variants and labels
- Link usage
- Action placement
- State indicators

### Patterns
- Filter patterns
- Toolbar composition
- Pagination implementation
- Bulk selection
- Empty states

---

## Documentation References

### Fetching Documentation

Always fetch the appropriate PatternFly documentation using raw GitHub URLs:

**Component Guidelines:**
```
https://raw.githubusercontent.com/patternfly/patternfly-org/refs/heads/main/packages/documentation-site/patternfly-docs/content/design-guidelines/components/[component-name]/[component-name].md
```

**Accessibility Guidelines:**
```
https://raw.githubusercontent.com/patternfly/patternfly-org/refs/heads/main/packages/documentation-site/patternfly-docs/content/accessibility/[component-name]/[component-name].md
```

### Referencing in Report

**IMPORTANT:** In the final report, link to the user-friendly PatternFly website, NOT raw GitHub URLs.

**Format for report links:**
- **Design Guidelines:** `https://www.patternfly.org/components/[component-name]/design-guidelines`
- **Accessibility:** `https://www.patternfly.org/components/[component-name]/accessibility`

**Example Report Reference Section:**
```markdown
## PatternFly Guideline References

- **Tabs Design Guidelines:** https://www.patternfly.org/components/tabs/design-guidelines
- **Tabs Accessibility:** https://www.patternfly.org/components/tabs/accessibility
- **Breadcrumb Design Guidelines:** https://www.patternfly.org/components/breadcrumb/design-guidelines
- **Button Design Guidelines:** https://www.patternfly.org/components/button/design-guidelines
```

**Common Components to Reference:**
- Breadcrumb
- Card
- Toolbar
- Pagination
- Masthead
- Navigation
- Tabs
- Button
- Label
- Form components
- Search input
- Select
- Modal
- Alert
- etc.

---

## Quality Checklist

Before finalizing the report, verify:

- [ ] Report header includes current date in YYYY-MM-DD format
- [ ] Used Figma MCP to extract actual component data
- [ ] All PatternFly components identified and listed
- [ ] Each component analyzed for property configuration
- [ ] Issues categorized by severity
- [ ] PatternFly guidelines cited for violations
- [ ] Specific, actionable recommendations provided
- [ ] Correct implementations acknowledged
- [ ] Summary table includes actual values from Figma
- [ ] Report focuses on design decisions, not code
- [ ] Placeholder content identified and called out
- [ ] Consistent terminology throughout report
- [ ] PatternFly guideline references use patternfly.org URLs (not raw GitHub)
- [ ] **CRITICAL:** Verified alignment using x/y coordinates from metadata (not assumptions)
- [ ] **CRITICAL:** Only flagged issues when explicit data confirms the problem
- [ ] **CRITICAL:** Noted "Cannot verify from available data" when metadata is insufficient
- [ ] **CRITICAL:** Assumed standard component instances include their default child elements unless proven otherwise

---

## Data Interpretation Guidelines

### Reading Metadata Coordinates

**Alignment Detection:**
```
Frame at x="32" y="474" width="1218" height="41"
  └─ Button at x="0" y="4" → LEFT-aligned (x=0)
  └─ Button at x="1150" y="4" → RIGHT-aligned (x close to frame width)
  └─ Button at x="609" y="4" → CENTER-aligned (x ≈ half of frame width)
```

**Rules:**
- x coordinate near 0 = left-aligned
- x coordinate near frame width = right-aligned
- x coordinate near center = center-aligned
- Never assume alignment without checking coordinates

### Understanding Component Properties

**When you see component instances, look for their properties:**

```xml
<instance name="Column Header/Header cell" x="56" y="0" width="278" height="48">
  <properties sortable="true" />
</instance>
```

**This means:**
- The column header HAS sorting enabled (`sortable=true`)
- Sort icons ARE present and visible
- This is CORRECT - do not flag as missing

**Example - What TO flag:**
```xml
<instance name="Column Header/Header cell">
  <properties sortable="false" />  ← If column should be sortable, THIS is an issue
</instance>
```

**Example - What NOT to flag:**
```xml
<instance name="Column Header/Header cell">
  <properties sortable="true" />  ← Sort icons are present, do NOT flag as missing
</instance>
```

**Common Component Properties to Check:**
- `sortable=true/false` - Controls sort icon visibility
- `state="selected/default/disabled"` - Controls state styling
- `variant="primary/secondary/danger"` - Controls button/component styling
- `showBadge=true/false` - Controls badge visibility
- `isExpandable=true/false` - Controls expansion chevron visibility

### Data Insufficiency Protocol

**If you cannot verify something from the data:**

❌ **WRONG:**
```markdown
❌ **Issue - Missing Sort Icons:**
- Table columns do not have sort indicators
```

✅ **CORRECT:**
```markdown
**Note:** Cannot verify presence of sort icons from available metadata. Column header component instances are present, which typically include sort icons by default.
```

**When to include "Unable to Verify" notes:**
1. Component instances are present but internal structure isn't visible
2. Screenshot resolution doesn't show fine details
3. Metadata doesn't include property values you need to check
4. Color values or other visual properties aren't in the data

---

## Example Usage

When receiving a Figma URL for review:

1. **Extract the fileKey and nodeId from URL**
   - URL format: `https://www.figma.com/design/{fileKey}/{fileName}?node-id={nodeId}`
   - Example: `rxlWfeof9blmF1rZBCItoN` and `17:10064`

2. **Run Figma MCP tools**
   ```
   - mcp__figma__get_screenshot(fileKey, nodeId)
   - mcp__figma__get_design_context(fileKey, nodeId, forceCode=true)
   ```

3. **Identify components from CodeConnectSnippet elements**
   - Look for `<CodeConnectSnippet>` wrappers
   - Extract component names and properties
   - Note child components and their configurations

4. **Fetch PatternFly documentation**
   - Based on components identified
   - Use `mcp__pf-mcp__usePatternFlyDocs` with relevant URLs

5. **Analyze each component**
   - Compare Figma properties to guidelines
   - Document discrepancies
   - Provide recommendations

6. **Generate structured report**
   - Follow report structure above
   - Include all required sections
   - Use consistent formatting

---

## Common Issues to Watch For

### Placeholder Content
- "Section title" in breadcrumbs
- "Nav item" in navigation
- "Tab name" in tabs
- "Button" for button labels
- "Page title" and "Page description"
- Generic lorem ipsum text

### Configuration Conflicts
- Breadcrumb type vs. first item type mismatch
- Component variant doesn't match use case
- Missing required child components
- Incorrect property combinations

### Missing Elements
- Missing labels on form groups
- Missing selection checkboxes in catalog views
- Missing bulk selectors when needed
- Missing helper text or descriptions
- Missing icons where recommended

### Inconsistent Patterns
- Mixed labeling approaches
- Inconsistent spacing
- Mismatched component variants
- Items in wrong groups or categories

### Accessibility Concerns
- Missing labels
- Poor color contrast
- Missing disabled state explanations
- Unclear interactive affordances

---

## Deliverable

The final report should enable designers to:
1. Understand which components are correctly configured
2. Identify specific properties that need adjustment
3. Replace placeholder content with meaningful labels
4. Align their design with PatternFly best practices
5. Prepare the design for development handoff

The report should be detailed enough that a designer can make corrections without needing to research guidelines themselves, while citing sources for transparency and learning.
