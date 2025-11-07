# Claude Code Slash Commands

This directory contains custom slash commands for the PatternFly Design Reviewer project.

## Available Commands

### `/review-design`

Conducts a comprehensive PatternFly design review following the framework in `DESIGN_REVIEW_PROMPT.md`.

**Usage:**
```
/review-design https://www.figma.com/design/[fileKey]/[fileName]?node-id=[nodeId]
```

**Example:**
```
/review-design https://www.figma.com/design/rxlWfeof9blmF1rZBCItoN/Untitled?node-id=31-3576
```

**What it does:**
1. Extracts component data from Figma using MCP
2. Fetches relevant PatternFly documentation
3. Analyzes component configurations against guidelines
4. Generates a detailed, actionable review report

**Output:**
A comprehensive design review report with:
- Complete component inventory
- Property-level analysis with actual Figma data
- Issues categorized by severity (Critical/Major/Moderate/Minor)
- Specific "How to Fix" recommendations
- Correct implementations acknowledged
- Links to PatternFly documentation

## How Slash Commands Work

When you type `/review-design` in Claude Code, it:
1. Loads the prompt from `review-design.md`
2. Expands it in the conversation
3. Follows the instructions automatically

You can verify the command is available by typing `/` in Claude Code and looking for "review-design" in the autocomplete list.

## Creating New Commands

To create a new slash command:
1. Create a `.md` file in this directory
2. Add a frontmatter with `description`
3. Write the prompt/instructions
4. Save the file
5. Restart Claude Code (if needed)

**Example structure:**
```markdown
---
description: Brief description of what this command does
---

# Command Title

Your detailed instructions here...
```

## Related Files

- **DESIGN_REVIEW_PROMPT.md** - Complete review methodology and framework
- **QUICK_REVIEW_TEMPLATE.md** - Quick reference for manual reviews
- **EXAMPLE_REVIEW_REPORT.md** - Example of completed review output
