# Components Plugin

Expert guidance for selecting, comparing, and prototyping PatternFly React components for consumer applications.

## Available Commands

### `/suggest-component`

Recommends appropriate PatternFly components based on your use case requirements.

**Usage:**
```
/suggest-component [describe your use case]
```

**Example:**
```
/suggest-component I need to display a list of users with their roles, allow filtering and sorting
```

**What it does:**
1. Analyzes your use case requirements and constraints
2. Searches PatternFly documentation for relevant components
3. Recommends the best-fit component(s) with justification
4. Provides complete usage examples with actual props
5. Explains component capabilities and limitations
6. Suggests component composition patterns when needed
7. Includes accessibility considerations
8. Demonstrates responsive behavior

**Output:**
- Primary component recommendation with rationale
- Alternative component options with trade-offs
- Complete code examples with props configuration
- Composition patterns for complex use cases
- Accessibility and responsive design guidance
- Links to official documentation and examples

---

### `/compare-components`

Compares similar PatternFly components and explains when to use each.

**Usage:**
```
/compare-components [component-name-1] vs [component-name-2]
```

**Example:**
```
/compare-components Table vs DataList
```

**What it does:**
1. Fetches documentation for both components
2. Analyzes component APIs, props, and capabilities
3. Identifies key differences and similarities
4. Provides decision criteria for choosing between them
5. Shows side-by-side usage examples
6. Explains performance and accessibility implications
7. Recommends best use cases for each

**Output:**
- Feature comparison matrix
- Use case recommendations for each component
- Side-by-side code examples
- Performance and accessibility considerations
- Migration guidance between similar components
- Design system alignment

---

### `/component-playground`

Generates interactive, runnable examples to prototype and explore PatternFly components.

**Usage:**
```
/component-playground [component-name] [optional: specific feature to explore]
```

**Example:**
```
/component-playground Table with expandable rows and selection
```

**What it does:**
1. Fetches component documentation and examples
2. Generates complete, runnable React code
3. Demonstrates key component features and props
4. Includes multiple variations and states
5. Shows component composition patterns
6. Provides interactive controls to modify props
7. Includes accessibility features demonstration
8. Adds helpful code comments and explanations

**Output:**
- Complete React component with imports
- Multiple example variations (basic, intermediate, advanced)
- Interactive prop controls (commented examples)
- State management examples
- Event handler implementations
- Accessibility features demonstration
- Responsive design patterns
- Testing examples with React Testing Library

---

## How to Use

1. Describe your use case or specify components to compare
2. Run the appropriate command
3. Review recommendations and examples
4. Copy code examples into your project
5. Customize based on your specific needs

## Related Documentation

- [PatternFly React Components](https://www.patternfly.org/components/all-components)
- [PatternFly Component Groups](https://www.patternfly.org/get-started/develop#component-groups)
- [PatternFly Design Guidelines](https://www.patternfly.org/get-started/design)
- [PatternFly Accessibility](https://www.patternfly.org/accessibility/accessibility-fundamentals)
