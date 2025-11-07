---
description: Review a PatternFly Figma design against design guidelines and best practices
---

# PatternFly Design Review

You are conducting a comprehensive PatternFly design review following the methodology in DESIGN_REVIEW_PROMPT.md.

**CRITICAL: Use EXAMPLE_REVIEW_REPORT.md as your formatting template. Match its structure EXACTLY, including:**
- Horizontal rules (`---`) between all major sections
- Exact heading format for each section
- Code block formatting for properties
- Table structure for summary
- Bullet list format for correctly configured components

## Input
The user will provide a Figma URL in the format:
`https://www.figma.com/design/{fileKey}/{fileName}?node-id={nodeId}`

## Your Task

Follow the framework in `DESIGN_REVIEW_PROMPT.md` exactly:

### Phase 1: Data Extraction
1. Extract fileKey and nodeId from the provided URL
2. Use `mcp__figma__get_screenshot(fileKey, nodeId)` to get visual context
3. Use `mcp__figma__get_design_context(fileKey, nodeId, forceCode=true)` to extract component data
4. If errors occur with get_design_context, use `mcp__figma__get_metadata(fileKey, nodeId)` as fallback
5. **CRITICAL:** Use x/y coordinates from metadata to determine alignment (x=0 is left-aligned, x near frame width is right-aligned)
6. **CRITICAL:** Assume component instances include their standard child elements unless explicitly marked as hidden in the data

### Phase 2: Fetch Documentation
Based on components identified in the design, fetch relevant PatternFly documentation using `mcp__pf-mcp__usePatternFlyDocs` with raw GitHub URLs for common components like:
- Breadcrumb
- Navigation
- Masthead
- Tabs
- Button
- Card
- Toolbar
- Pagination
- Page
- etc.

### Phase 3: Analyze Components
For EACH PatternFly component:
1. Extract actual property values from Figma MCP data including component properties/toggles (e.g., `sortable=true`, `state="selected"`)
2. Use the Figma component properties to determine features (e.g., if `sortable=true`, sort icons are present)
3. Compare against PatternFly guidelines
4. Identify correct configurations (✅)
5. **ONLY** identify issues with severity when you have explicit data proving the issue (❌)
   - Check component property values before flagging issues
   - If property data is unavailable, note "Cannot verify from available metadata" instead of assuming an issue exists
6. Provide specific "How to Fix in Figma" steps for confirmed issues only

### Phase 4: Generate Report

Create a structured report with:

#### Report Header (REQUIRED)
```markdown
# PatternFly Design Review Report

## Design Reviewed
- **Figma URL:** `[paste full URL here]`
- **Design Type:** [Brief description of what's being reviewed]
- **Date:** [Current date in YYYY-MM-DD format - e.g., 2025-10-20]
```

#### Required Sections (EXACT FORMAT - see EXAMPLE_REVIEW_REPORT.md)

**CRITICAL: Separate each section with `---` horizontal rule**

1. **Complete List of PatternFly 6 Components Used**
   ```markdown
   ## Complete List of PatternFly 6 Components Used

   1. **ComponentName** - Brief description
   2. **ComponentName** - Brief description

   ---
   ```

2. **Configuration Issues with PatternFly Components**
   For each component WITH issues, use this EXACT template:
   ```markdown
   ### 1. ComponentName (Severity)

   **Properties Configured:**
   ```
   property: value
   ```

   **Child Components:** (if applicable)
   ```
   details
   ```

   **Analysis:**

   ✅ **Correct Configuration:**
   - What's correct

   ❌ **[Severity] Issue - Description:**
   - Current state
   - Why it's wrong

   **PatternFly Guideline:**
   > "Quote from docs"

   **How to Fix in Figma:**
   1. Step 1
   2. Step 2

   ---
   ```

3. **Summary: Component Configuration Issues**
   ```markdown
   ## Summary: Component Configuration Issues

   | Component | Property | Current Value | Issue | Recommendation |
   |-----------|----------|---------------|-------|----------------|

   ---
   ```

4. **Correctly Configured Components**
   ```markdown
   ## Correctly Configured Components

   The following components demonstrate proper PatternFly implementation:

   ### ✅ ComponentName
   - **Property:** Details

   ---
   ```

5. **Overall Assessment**
   ```markdown
   ## Overall Assessment

   ### Strengths
   - Bullet points

   ### Areas for Improvement
   - 🔴 **Critical:** Issues
   - 🟡 **Moderate:** Issues
   - 🟢 **Minor:** Issues

   ### Development Readiness
   **Status:** [Ready/Not ready/Ready with modifications]

   **Required Actions:**
   1. Action

   **Estimated Effort:** [Low/Medium/High]

   ---
   ```

6. **PatternFly Guideline References**
   ```markdown
   ## PatternFly Guideline References

   - **Component Design Guidelines:** https://www.patternfly.org/components/component/design-guidelines

   (NO TRAILING ---)
   ```

## Critical Requirements

✅ **DO:**
- **Match EXAMPLE_REVIEW_REPORT.md format exactly** (most important!)
- Use horizontal rules (`---`) between ALL major sections
- Use actual component property values from Figma MCP data
- Use current date (e.g., 2025-11-04) in report header
- Quote PatternFly guidelines when noting violations
- Provide designer-focused, actionable feedback
- Link to patternfly.org in final references section
- Acknowledge correct implementations alongside issues
- Categorize issues by severity
- Use "Summary: Component Configuration Issues" as table header (NOT "Summary Table")

❌ **DON'T:**
- Deviate from the EXAMPLE_REVIEW_REPORT.md template structure
- Forget horizontal rules between sections
- Rely only on visual inspection - extract actual data
- Use placeholder or old dates in report header
- Focus on code implementation (focus on design)
- Link to raw GitHub markdown in report references
- Skip the report header
- Make assumptions about component properties - check Figma property values (e.g., `sortable=true`)
- Flag issues when you cannot verify them from the available data
- Assume alignment without checking x/y coordinates from metadata

## Output

Generate a complete PatternFly design review report following the exact structure outlined above and in DESIGN_REVIEW_PROMPT.md.
