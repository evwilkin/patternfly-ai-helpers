# Tables Plugin

Configure data tables, add advanced features, and optimize performance using PatternFly Table components.

## Commands

### `/configure-table`
Analyze your data structure and recommend the optimal table configuration for your use case.

**What it does:**
- Analyzes data structure and relationships
- Recommends table type (simple, compound expandable, tree, nested, etc.)
- Generates complete table implementation with proper column definitions
- Configures TypeScript types for type-safe data handling
- Sets up responsive table behavior
- Implements accessibility features (ARIA labels, keyboard navigation, screen reader support)
- Adds loading and empty states
- Provides testing examples

**Use when:**
- Starting a new table implementation
- Replacing legacy table components
- Unsure which table variant to use
- Need guidance on data structure organization

---

### `/add-table-features`
Add advanced features to existing tables including sorting, filtering, pagination, selection, and actions.

**What it does:**
- Implements single and multi-column sorting
- Adds column-specific and global filtering
- Configures pagination (front-end and back-end)
- Sets up row selection (single, multi, bulk actions)
- Adds expandable rows and compound expansion
- Implements tree table functionality
- Configures toolbar with actions and filters
- Adds row-level and bulk actions
- Implements drag-and-drop reordering
- Provides inline editing capabilities

**Use when:**
- Enhancing existing table implementations
- Adding interactive features to static tables
- Implementing complex data manipulation workflows
- Need user-driven data organization features

---

### `/optimize-table-performance`
Optimize large tables with virtualization, lazy loading, and performance best practices.

**What it does:**
- Implements virtualization for large datasets (1000+ rows)
- Sets up lazy loading and infinite scroll
- Optimizes re-render performance with memoization
- Configures efficient data fetching strategies
- Implements debounced search and filtering
- Adds loading skeletons and progressive enhancement
- Optimizes bundle size with code splitting
- Provides performance monitoring examples
- Implements client-side caching strategies
- Shows profiling and debugging techniques

**Use when:**
- Tables are slow or laggy with large datasets
- Need to display thousands of rows
- Performance is degrading user experience
- Want to implement best practices for scalability
- Need to optimize network requests

## Installation

This plugin is part of the PatternFly AI Helpers collection. It includes access to the PatternFly documentation through the MCP server.

## Examples

### Basic table setup
```bash
/configure-table
```
The command will analyze your data and create an appropriate table implementation.

### Adding features
```bash
/add-table-features
```
Enhances your existing table with sorting, filtering, pagination, and selection.

### Performance optimization
```bash
/optimize-table-performance
```
Optimizes your table for large datasets and better performance.

## Related Resources

- [PatternFly Table Documentation](https://www.patternfly.org/components/table)
- [PatternFly Table React](https://www.patternfly.org/components/table/react)
- [Accessibility Guidelines](https://www.patternfly.org/accessibility/table)

## Support

For issues or questions about this plugin, please refer to the main PatternFly AI Helpers documentation.
