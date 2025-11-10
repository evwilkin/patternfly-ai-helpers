---
description: Generate interactive examples to prototype and explore PatternFly components
---

# PatternFly Component Playground Generator

You are an expert in creating comprehensive, interactive examples of PatternFly React components for prototyping and learning.

## Input

The user will specify:
- A component name (e.g., "Table", "Modal", "Select")
- Optionally, specific features to explore (e.g., "with expandable rows", "with validation", "dark mode")
- Optionally, a specific use case context

Examples:
- "Table with sorting and filtering"
- "Modal with form validation"
- "Select component"
- "Card with actions"

## Your Task

### Phase 1: Component Analysis

**Parse and understand the request:**

1. **Identify the component:**
   - Extract the main component name
   - Identify any requested features or variants
   - Determine the complexity level (basic, intermediate, advanced)

2. **Clarify if needed:**
   - If the component name is ambiguous, ask for clarification
   - If the requested feature doesn't exist, suggest alternatives
   - If the component doesn't exist in PatternFly, suggest the correct one

### Phase 2: Fetch Component Documentation

Use `mcp__pf-mcp__usePatternFlyDocs` to retrieve comprehensive information:

**Fetch:**
1. Component overview and purpose
2. Complete props API documentation
3. All available examples and demos
4. Features and capabilities
5. Accessibility guidelines
6. Common patterns and best practices
7. Related components that might be composed together

**Analyze:**
- What are the core features of this component?
- What variations and states should be demonstrated?
- What common use cases should be covered?
- What props are essential vs. optional?
- What composition patterns are relevant?

### Phase 3: Generate Playground Code

Create a comprehensive, interactive playground following this structure:

```markdown
# [Component Name] Playground

Interactive examples to explore and prototype the PatternFly [Component Name] component.

## Overview

**Component:** [Component Name]

**Purpose:** [What this component does]

**Key Features:**
- [Feature 1]
- [Feature 2]
- [Feature 3]

**Installation:**
```bash
npm install @patternfly/react-core
```

---

## Example 1: Basic Usage

The simplest implementation to get started.

### Code

```tsx
import React from 'react';
import { [Component] } from '@patternfly/react-core';

export const Basic[Component]Example: React.FC = () => {
  return (
    <[Component]
      // Essential props only
      [requiredProp]={[value]}
      aria-label="Basic example"
    >
      {/* Minimal content to demonstrate component */}
    </[Component]>
  );
};

export default Basic[Component]Example;
```

### What This Demonstrates

- ✅ Minimal required props
- ✅ Basic component structure
- ✅ Default styling and behavior
- ✅ Essential accessibility attributes

### Try It Out

**Modify these props to experiment:**
```tsx
// Change the [prop] (try: [option1], [option2], [option3])
[prop]="[option1]"

// Toggle [feature] (try: true, false)
[featureProp]={true}

// Update the content
{/* Replace this content with your own */}
```

### Output

When you run this example, you'll see:
- [Description of what renders]
- [Default behavior]
- [How it responds to interaction]

---

## Example 2: Interactive States

Demonstrates different component states and user interactions.

### Code

```tsx
import React, { useState } from 'react';
import { [Component], [RelatedComponents] } from '@patternfly/react-core';

interface ExampleData {
  id: string;
  label: string;
  value: string;
}

export const Interactive[Component]Example: React.FC = () => {
  // State for tracking interactions
  const [selectedId, setSelectedId] = useState<string | null>(null);
  const [isOpen, setIsOpen] = useState(false);
  const [inputValue, setInputValue] = useState('');

  // Sample data
  const items: ExampleData[] = [
    { id: '1', label: 'Option 1', value: 'value1' },
    { id: '2', label: 'Option 2', value: 'value2' },
    { id: '3', label: 'Option 3', value: 'value3' },
  ];

  // Event handlers
  const handleSelect = (id: string) => {
    setSelectedId(id);
    console.log('Selected:', id);
  };

  const handleToggle = () => {
    setIsOpen(!isOpen);
    console.log('Toggled:', !isOpen);
  };

  const handleChange = (value: string) => {
    setInputValue(value);
    console.log('Changed:', value);
  };

  return (
    <div>
      {/* Display current state for debugging */}
      <div style={{ marginBottom: '1rem', padding: '1rem', background: '#f5f5f5' }}>
        <strong>Current State:</strong>
        <pre>{JSON.stringify({ selectedId, isOpen, inputValue }, null, 2)}</pre>
      </div>

      {/* Component with interactive features */}
      <[Component]
        // Props for interaction
        [selectedProp]={selectedId}
        [isOpenProp]={isOpen}
        on[SelectEvent]={handleSelect}
        on[ToggleEvent]={handleToggle}
        on[ChangeEvent]={handleChange}
        aria-label="Interactive example"
      >
        {items.map((item) => (
          <[ChildComponent]
            key={item.id}
            [itemProp]={item}
            isSelected={selectedId === item.id}
            onClick={() => handleSelect(item.id)}
          >
            {item.label}
          </[ChildComponent]>
        ))}
      </[Component>
    </div>
  );
};

export default Interactive[Component]Example;
```

### What This Demonstrates

- ✅ State management with useState
- ✅ Event handling and user interactions
- ✅ Controlled component pattern
- ✅ State visualization for debugging
- ✅ Multiple interactive features

### Try It Out

**Experiment with state:**
```tsx
// Try different initial states
const [selectedId, setSelectedId] = useState<string | null>('2'); // Pre-select item 2
const [isOpen, setIsOpen] = useState(true); // Start in open state

// Add more state
const [isDisabled, setIsDisabled] = useState(false);
const [variant, setVariant] = useState<'default' | 'alternate'>('default');

// Log events to console
console.log('Component rendered with state:', { selectedId, isOpen });
```

**Modify the data:**
```tsx
// Add more items
const items = [
  ...existingItems,
  { id: '4', label: 'Option 4', value: 'value4' },
];

// Change item properties
const items = [
  { id: '1', label: 'Custom Label', value: 'custom', isDisabled: true },
];
```

---

## Example 3: Advanced Features

Comprehensive example with multiple advanced features.

### Code

```tsx
import React, { useState, useMemo, useCallback } from 'react';
import {
  [Component],
  [AdvancedFeature1],
  [AdvancedFeature2],
  Toolbar,
  ToolbarContent,
  ToolbarItem,
  SearchInput,
  Button,
  Pagination,
  EmptyState,
  EmptyStateIcon,
  Title,
  Spinner
} from '@patternfly/react-core';
import { [Icon] } from '@patternfly/react-icons';

interface AdvancedData {
  id: string;
  name: string;
  description: string;
  status: 'active' | 'inactive' | 'pending';
  created: Date;
  metadata: {
    category: string;
    priority: 'low' | 'medium' | 'high';
    tags: string[];
  };
}

export const Advanced[Component]Example: React.FC = () => {
  // State management for all features
  const [data, setData] = useState<AdvancedData[]>(generateSampleData(50));
  const [selectedIds, setSelectedIds] = useState<string[]>([]);
  const [expandedIds, setExpandedIds] = useState<string[]>([]);
  const [searchValue, setSearchValue] = useState('');
  const [statusFilter, setStatusFilter] = useState<string>('all');
  const [sortBy, setSortBy] = useState<{
    key: keyof AdvancedData;
    direction: 'asc' | 'desc';
  }>({ key: 'name', direction: 'asc' });
  const [page, setPage] = useState(1);
  const [perPage, setPerPage] = useState(10);
  const [isLoading, setIsLoading] = useState(false);

  // Filtering logic
  const filteredData = useMemo(() => {
    return data.filter((item) => {
      // Search filter
      const matchesSearch = searchValue === '' ||
        item.name.toLowerCase().includes(searchValue.toLowerCase()) ||
        item.description.toLowerCase().includes(searchValue.toLowerCase());

      // Status filter
      const matchesStatus = statusFilter === 'all' ||
        item.status === statusFilter;

      return matchesSearch && matchesStatus;
    });
  }, [data, searchValue, statusFilter]);

  // Sorting logic
  const sortedData = useMemo(() => {
    const sorted = [...filteredData].sort((a, b) => {
      const aValue = a[sortBy.key];
      const bValue = b[sortBy.key];

      if (aValue < bValue) return sortBy.direction === 'asc' ? -1 : 1;
      if (aValue > bValue) return sortBy.direction === 'asc' ? 1 : -1;
      return 0;
    });

    return sorted;
  }, [filteredData, sortBy]);

  // Pagination
  const paginatedData = useMemo(() => {
    const start = (page - 1) * perPage;
    return sortedData.slice(start, start + perPage);
  }, [sortedData, page, perPage]);

  // Event handlers with useCallback for performance
  const handleSearch = useCallback((value: string) => {
    setSearchValue(value);
    setPage(1); // Reset to first page on search
  }, []);

  const handleSort = useCallback((key: keyof AdvancedData) => {
    setSortBy((prev) => ({
      key,
      direction: prev.key === key && prev.direction === 'asc' ? 'desc' : 'asc',
    }));
  }, []);

  const handleSelect = useCallback((id: string, isSelecting: boolean) => {
    setSelectedIds((prev) =>
      isSelecting
        ? [...prev, id]
        : prev.filter((selectedId) => selectedId !== id)
    );
  }, []);

  const handleSelectAll = useCallback((isSelecting: boolean) => {
    setSelectedIds(isSelecting ? paginatedData.map((item) => item.id) : []);
  }, [paginatedData]);

  const handleExpand = useCallback((id: string) => {
    setExpandedIds((prev) =>
      prev.includes(id)
        ? prev.filter((expandedId) => expandedId !== id)
        : [...prev, id]
    );
  }, []);

  const handleBulkAction = useCallback(async (action: string) => {
    setIsLoading(true);
    console.log(`Performing ${action} on:`, selectedIds);

    // Simulate async operation
    await new Promise((resolve) => setTimeout(resolve, 1000));

    // Update data based on action
    setData((prev) =>
      prev.map((item) =>
        selectedIds.includes(item.id)
          ? { ...item, status: action === 'activate' ? 'active' : 'inactive' }
          : item
      )
    );

    setIsLoading(false);
    setSelectedIds([]); // Clear selection after action
  }, [selectedIds]);

  const handlePageChange = useCallback((_event: any, newPage: number) => {
    setPage(newPage);
  }, []);

  const handlePerPageChange = useCallback((_event: any, newPerPage: number) => {
    setPerPage(newPerPage);
    setPage(1); // Reset to first page when changing page size
  }, []);

  return (
    <div>
      {/* Toolbar with filters and actions */}
      <Toolbar>
        <ToolbarContent>
          <ToolbarItem variant="search-filter">
            <SearchInput
              placeholder="Search by name or description"
              value={searchValue}
              onChange={(_event, value) => handleSearch(value)}
              onClear={() => handleSearch('')}
              aria-label="Search"
            />
          </ToolbarItem>

          <ToolbarItem>
            <select
              value={statusFilter}
              onChange={(e) => setStatusFilter(e.target.value)}
              style={{ padding: '0.5rem', borderRadius: '3px' }}
              aria-label="Filter by status"
            >
              <option value="all">All Status</option>
              <option value="active">Active</option>
              <option value="inactive">Inactive</option>
              <option value="pending">Pending</option>
            </select>
          </ToolbarItem>

          {selectedIds.length > 0 && (
            <>
              <ToolbarItem>
                <Button
                  variant="primary"
                  onClick={() => handleBulkAction('activate')}
                  isDisabled={isLoading}
                >
                  Activate Selected ({selectedIds.length})
                </Button>
              </ToolbarItem>
              <ToolbarItem>
                <Button
                  variant="secondary"
                  onClick={() => handleBulkAction('deactivate')}
                  isDisabled={isLoading}
                >
                  Deactivate Selected
                </Button>
              </ToolbarItem>
            </>
          )}

          <ToolbarItem variant="pagination" align={{ default: 'alignRight' }}>
            <Pagination
              itemCount={filteredData.length}
              perPage={perPage}
              page={page}
              onSetPage={handlePageChange}
              onPerPageSelect={handlePerPageChange}
              variant="top"
            />
          </ToolbarItem>
        </ToolbarContent>
      </Toolbar>

      {/* Loading state */}
      {isLoading && (
        <div style={{ padding: '2rem', textAlign: 'center' }}>
          <Spinner size="xl" />
        </div>
      )}

      {/* Empty state */}
      {!isLoading && paginatedData.length === 0 && (
        <EmptyState>
          <EmptyStateIcon icon={[Icon]} />
          <Title headingLevel="h4" size="lg">
            No results found
          </Title>
          <p>
            {searchValue
              ? `No items match "${searchValue}"`
              : 'No items available'}
          </p>
          {searchValue && (
            <Button variant="link" onClick={() => handleSearch('')}>
              Clear search
            </Button>
          )}
        </EmptyState>
      )}

      {/* Main component with all features */}
      {!isLoading && paginatedData.length > 0 && (
        <[Component]
          // Selection props
          [selectAllProp]={
            selectedIds.length === paginatedData.length &&
            paginatedData.length > 0
          }
          on[SelectAllEvent]={(isSelecting) => handleSelectAll(isSelecting)}
          // Sorting props
          [sortByProp]={sortBy}
          on[SortEvent]={(key) => handleSort(key as keyof AdvancedData)}
          // Accessibility
          aria-label="Advanced data table with all features"
        >
          {paginatedData.map((item) => {
            const isSelected = selectedIds.includes(item.id);
            const isExpanded = expandedIds.includes(item.id);

            return (
              <[ChildComponent]
                key={item.id}
                // Item data
                [itemProp]={item}
                // Selection state
                isSelected={isSelected}
                onSelect={(isSelecting) => handleSelect(item.id, isSelecting)}
                // Expansion state
                isExpanded={isExpanded}
                onToggle={() => handleExpand(item.id)}
              >
                {/* Main content */}
                <div>
                  <strong>{item.name}</strong>
                  <p>{item.description}</p>
                  <span
                    style={{
                      padding: '0.25rem 0.5rem',
                      borderRadius: '3px',
                      background:
                        item.status === 'active'
                          ? '#d4edda'
                          : item.status === 'inactive'
                          ? '#f8d7da'
                          : '#fff3cd',
                    }}
                  >
                    {item.status}
                  </span>
                </div>

                {/* Expanded content */}
                {isExpanded && (
                  <[ExpandedContent]>
                    <div style={{ padding: '1rem', background: '#f5f5f5' }}>
                      <h4>Additional Details</h4>
                      <dl>
                        <dt>Category:</dt>
                        <dd>{item.metadata.category}</dd>
                        <dt>Priority:</dt>
                        <dd>{item.metadata.priority}</dd>
                        <dt>Tags:</dt>
                        <dd>{item.metadata.tags.join(', ')}</dd>
                        <dt>Created:</dt>
                        <dd>{item.created.toLocaleDateString()}</dd>
                      </dl>
                    </div>
                  </[ExpandedContent]>
                )}
              </[ChildComponent]>
            );
          })}
        </[Component>
      )}

      {/* Bottom pagination */}
      {!isLoading && paginatedData.length > 0 && (
        <Pagination
          itemCount={filteredData.length}
          perPage={perPage}
          page={page}
          onSetPage={handlePageChange}
          onPerPageSelect={handlePerPageChange}
          variant="bottom"
        />
      )}

      {/* Debug panel */}
      <details style={{ marginTop: '2rem' }}>
        <summary>Debug Information</summary>
        <pre style={{ background: '#f5f5f5', padding: '1rem', overflow: 'auto' }}>
          {JSON.stringify(
            {
              totalItems: data.length,
              filteredItems: filteredData.length,
              paginatedItems: paginatedData.length,
              selectedIds,
              expandedIds,
              searchValue,
              statusFilter,
              sortBy,
              page,
              perPage,
            },
            null,
            2
          )}
        </pre>
      </details>
    </div>
  );
};

// Helper function to generate sample data
function generateSampleData(count: number): AdvancedData[] {
  const statuses: Array<'active' | 'inactive' | 'pending'> = ['active', 'inactive', 'pending'];
  const categories = ['Development', 'Design', 'Testing', 'Documentation'];
  const priorities: Array<'low' | 'medium' | 'high'> = ['low', 'medium', 'high'];
  const tags = ['frontend', 'backend', 'api', 'ui', 'ux', 'performance', 'security'];

  return Array.from({ length: count }, (_, i) => ({
    id: `item-${i + 1}`,
    name: `Item ${i + 1}`,
    description: `Description for item ${i + 1}`,
    status: statuses[i % statuses.length],
    created: new Date(Date.now() - Math.random() * 365 * 24 * 60 * 60 * 1000),
    metadata: {
      category: categories[i % categories.length],
      priority: priorities[i % priorities.length],
      tags: [
        tags[Math.floor(Math.random() * tags.length)],
        tags[Math.floor(Math.random() * tags.length)],
      ],
    },
  }));
}

export default Advanced[Component]Example;
```

### What This Demonstrates

- ✅ Complex state management with multiple useState hooks
- ✅ Performance optimization with useMemo and useCallback
- ✅ Search and filtering functionality
- ✅ Multi-column sorting
- ✅ Bulk selection and actions
- ✅ Expandable rows with detailed content
- ✅ Pagination (top and bottom)
- ✅ Loading states
- ✅ Empty states
- ✅ Toolbar integration
- ✅ Async operations
- ✅ Debug panel for development

### Try It Out

**Performance optimization:**
```tsx
// Remove useMemo to see performance impact
// const sortedData = useMemo(() => { ... }, [deps]); // Optimized
const sortedData = [...filteredData].sort(...); // Unoptimized - recalculates every render

// Add performance logging
console.time('Filter and sort');
const result = data.filter(...).sort(...);
console.timeEnd('Filter and sort');
```

**Add more features:**
```tsx
// Add export functionality
const handleExport = () => {
  const csv = convertToCSV(selectedIds.length ? selectedIds : data);
  downloadFile(csv, 'export.csv');
};

// Add drag and drop reordering
import { DragDropContext, Droppable, Draggable } from 'react-beautiful-dnd';

// Add real-time filtering
useEffect(() => {
  const debounced = debounce(() => {
    fetchData(searchValue);
  }, 300);
  debounced();
}, [searchValue]);
```

**Customize the data generator:**
```tsx
// Generate more realistic data
function generateSampleData(count: number): AdvancedData[] {
  return Array.from({ length: count }, (_, i) => ({
    id: `item-${i + 1}`,
    name: `${faker.commerce.productName()} ${i + 1}`,
    description: faker.commerce.productDescription(),
    status: faker.helpers.arrayElement(['active', 'inactive', 'pending']),
    created: faker.date.past(),
    metadata: {
      category: faker.commerce.department(),
      priority: faker.helpers.arrayElement(['low', 'medium', 'high']),
      tags: faker.helpers.arrayElements(tags, 3),
    },
  }));
}
```

---

## Example 4: Accessibility Showcase

Demonstrates comprehensive accessibility features.

### Code

```tsx
import React, { useState, useRef, useEffect } from 'react';
import { [Component], ScreenReaderContent } from '@patternfly/react-core';

export const Accessible[Component]Example: React.FC = () => {
  const [selectedId, setSelectedId] = useState<string | null>(null);
  const [announcement, setAnnouncement] = useState('');
  const componentRef = useRef<HTMLDivElement>(null);

  // Announce changes to screen readers
  const announce = (message: string) => {
    setAnnouncement(message);
    // Clear after announced
    setTimeout(() => setAnnouncement(''), 1000);
  };

  // Handle selection with announcement
  const handleSelect = (id: string, label: string) => {
    setSelectedId(id);
    announce(`Selected ${label}`);
  };

  // Keyboard navigation example
  const handleKeyDown = (event: React.KeyboardEvent, id: string) => {
    switch (event.key) {
      case 'Enter':
      case ' ':
        event.preventDefault();
        handleSelect(id, `Item ${id}`);
        break;
      case 'Escape':
        setSelectedId(null);
        announce('Selection cleared');
        break;
    }
  };

  const items = [
    { id: '1', label: 'First item', description: 'Description of first item' },
    { id: '2', label: 'Second item', description: 'Description of second item' },
    { id: '3', label: 'Third item', description: 'Description of third item' },
  ];

  return (
    <div>
      {/* Live region for screen reader announcements */}
      <div
        role="status"
        aria-live="polite"
        aria-atomic="true"
        style={{
          position: 'absolute',
          left: '-10000px',
          width: '1px',
          height: '1px',
          overflow: 'hidden',
        }}
      >
        {announcement}
      </div>

      {/* Skip link for keyboard users */}
      <a
        href="#main-content"
        style={{
          position: 'absolute',
          left: '-10000px',
          top: 'auto',
          width: '1px',
          height: '1px',
          overflow: 'hidden',
        }}
        onFocus={(e) => {
          e.currentTarget.style.position = 'static';
          e.currentTarget.style.width = 'auto';
          e.currentTarget.style.height = 'auto';
        }}
        onBlur={(e) => {
          e.currentTarget.style.position = 'absolute';
          e.currentTarget.style.left = '-10000px';
          e.currentTarget.style.width = '1px';
          e.currentTarget.style.height = '1px';
        }}
      >
        Skip to main content
      </a>

      <div id="main-content" ref={componentRef}>
        <[Component]
          // ARIA attributes
          aria-label="Accessible component example"
          aria-describedby="component-description"
          // Keyboard accessible
          onKeyDown={(e) => handleKeyDown(e, selectedId || '1')}
          // Focus management
          tabIndex={0}
        >
          {/* Hidden description for screen readers */}
          <ScreenReaderContent id="component-description">
            This component demonstrates accessibility features. Use arrow keys to
            navigate, Enter or Space to select, and Escape to clear selection.
          </ScreenReaderContent>

          {items.map((item) => {
            const isSelected = selectedId === item.id;

            return (
              <[ChildComponent]
                key={item.id}
                // Semantic HTML
                as="article"
                // ARIA attributes
                role="option"
                aria-selected={isSelected}
                aria-labelledby={`item-${item.id}-label`}
                aria-describedby={`item-${item.id}-desc`}
                // Keyboard accessible
                tabIndex={isSelected ? 0 : -1}
                onKeyDown={(e) => handleKeyDown(e, item.id)}
                onClick={() => handleSelect(item.id, item.label)}
                // Focus indicator
                style={{
                  outline: isSelected ? '2px solid #0066cc' : 'none',
                  outlineOffset: '2px',
                }}
              >
                <h3 id={`item-${item.id}-label`}>{item.label}</h3>
                <p id={`item-${item.id}-desc`}>{item.description}</p>

                {/* Visual indicator with screen reader text */}
                {isSelected && (
                  <span>
                    <ScreenReaderContent>Selected</ScreenReaderContent>
                    <span aria-hidden="true">✓</span>
                  </span>
                )}
              </[ChildComponent]>
            );
          })}
        </[Component>
      </div>

      {/* Accessibility testing checklist */}
      <details style={{ marginTop: '2rem', border: '1px solid #ccc', padding: '1rem' }}>
        <summary>
          <strong>Accessibility Testing Checklist</strong>
        </summary>
        <ul style={{ marginTop: '1rem' }}>
          <li>
            <label>
              <input type="checkbox" /> Tab through all interactive elements
            </label>
          </li>
          <li>
            <label>
              <input type="checkbox" /> Use Enter/Space to activate
            </label>
          </li>
          <li>
            <label>
              <input type="checkbox" /> Navigate with arrow keys
            </label>
          </li>
          <li>
            <label>
              <input type="checkbox" /> Test with screen reader (VoiceOver/NVDA/JAWS)
            </label>
          </li>
          <li>
            <label>
              <input type="checkbox" /> Verify focus is visible
            </label>
          </li>
          <li>
            <label>
              <input type="checkbox" /> Check color contrast (4.5:1 minimum)
            </label>
          </li>
          <li>
            <label>
              <input type="checkbox" /> Test at 200% zoom
            </label>
          </li>
          <li>
            <label>
              <input type="checkbox" /> Verify all images have alt text
            </label>
          </li>
          <li>
            <label>
              <input type="checkbox" /> Check form labels are associated
            </label>
          </li>
          <li>
            <label>
              <input type="checkbox" /> Test without mouse/trackpad
            </label>
          </li>
        </ul>
      </details>
    </div>
  );
};

export default Accessible[Component]Example;
```

### What This Demonstrates

- ✅ ARIA attributes (role, aria-label, aria-describedby, aria-selected)
- ✅ Screen reader announcements with live regions
- ✅ Keyboard navigation and shortcuts
- ✅ Focus management
- ✅ Skip links
- ✅ ScreenReaderContent for hidden text
- ✅ Semantic HTML elements
- ✅ Visual focus indicators
- ✅ Testing checklist

### Accessibility Guidelines

**WCAG 2.1 Compliance:**
- ✅ Level A: All basic criteria met
- ✅ Level AA: Enhanced criteria met
- ⚠️ Level AAA: Some criteria (check specific requirements)

**PatternFly Accessibility:**
- All PatternFly components include built-in accessibility
- Follow PatternFly guidelines for consistent experience
- Test with actual assistive technologies

### Try It Out

**Test keyboard navigation:**
```tsx
// Try different keyboard shortcuts
onKeyDown={(e) => {
  switch (e.key) {
    case 'ArrowUp':
      // Navigate to previous item
      break;
    case 'ArrowDown':
      // Navigate to next item
      break;
    case 'Home':
      // Go to first item
      break;
    case 'End':
      // Go to last item
      break;
    case 'Enter':
    case ' ':
      // Activate/select
      break;
  }
}}
```

**Customize announcements:**
```tsx
// More descriptive announcements
announce(`Selected ${label}. ${selectedIds.length} of ${totalItems} items selected.`);
announce(`Sorting by ${column} in ${direction} order`);
announce(`Page ${page} of ${totalPages}. Showing ${itemsOnPage} items.`);
```

---

## Example 5: Responsive Design

Demonstrates responsive behavior across different screen sizes.

### Code

```tsx
import React, { useState, useEffect } from 'react';
import {
  [Component],
  Stack,
  StackItem,
  Grid,
  GridItem,
} from '@patternfly/react-core';

export const Responsive[Component]Example: React.FC = () => {
  const [viewport, setViewport] = useState({
    width: window.innerWidth,
    height: window.innerHeight,
  });

  // Track viewport size
  useEffect(() => {
    const handleResize = () => {
      setViewport({
        width: window.innerWidth,
        height: window.innerHeight,
      });
    };

    window.addEventListener('resize', handleResize);
    return () => window.removeEventListener('resize', handleResize);
  }, []);

  // Determine device type
  const isMobile = viewport.width < 768;
  const isTablet = viewport.width >= 768 && viewport.width < 1024;
  const isDesktop = viewport.width >= 1024;

  return (
    <div>
      {/* Viewport indicator */}
      <div
        style={{
          padding: '0.5rem',
          background: '#f0f0f0',
          marginBottom: '1rem',
          textAlign: 'center',
        }}
      >
        <strong>Current Viewport:</strong> {viewport.width}px × {viewport.height}px
        {' | '}
        <strong>Device:</strong>{' '}
        {isMobile ? 'Mobile' : isTablet ? 'Tablet' : 'Desktop'}
      </div>

      {/* Responsive component */}
      <[Component]
        // Responsive props
        variant={isMobile ? 'compact' : 'default'}
        [breakpointProp]={{
          default: 'stack',
          md: 'grid',
          lg: 'grid',
        }}
      >
        {/* Mobile layout */}
        {isMobile && (
          <Stack hasGutter>
            <StackItem>
              <div style={{ padding: '1rem', background: '#e3f2fd' }}>
                Mobile: Stacked layout
              </div>
            </StackItem>
            <StackItem>
              <div style={{ padding: '1rem', background: '#f3e5f5' }}>
                Full width content
              </div>
            </StackItem>
          </Stack>
        )}

        {/* Tablet layout */}
        {isTablet && (
          <Grid hasGutter>
            <GridItem span={6}>
              <div style={{ padding: '1rem', background: '#e3f2fd' }}>
                Tablet: 2 column grid
              </div>
            </GridItem>
            <GridItem span={6}>
              <div style={{ padding: '1rem', background: '#f3e5f5' }}>
                Side by side content
              </div>
            </GridItem>
          </Grid>
        )}

        {/* Desktop layout */}
        {isDesktop && (
          <Grid hasGutter>
            <GridItem span={4}>
              <div style={{ padding: '1rem', background: '#e3f2fd' }}>
                Desktop: 3 column grid
              </div>
            </GridItem>
            <GridItem span={4}>
              <div style={{ padding: '1rem', background: '#f3e5f5' }}>
                Multiple columns
              </div>
            </GridItem>
            <GridItem span={4}>
              <div style={{ padding: '1rem', background: '#e8f5e9' }}>
                Maximum space usage
              </div>
            </GridItem>
          </Grid>
        )}
      </[Component>

      {/* Responsive design tips */}
      <details style={{ marginTop: '2rem' }}>
        <summary>
          <strong>Responsive Design Tips</strong>
        </summary>
        <ul style={{ marginTop: '1rem' }}>
          <li>
            <strong>Mobile (< 768px):</strong>
            <ul>
              <li>Stack content vertically</li>
              <li>Use compact variants</li>
              <li>Hide non-essential information</li>
              <li>Increase touch target sizes</li>
            </ul>
          </li>
          <li>
            <strong>Tablet (768px - 1024px):</strong>
            <ul>
              <li>2-column layouts</li>
              <li>Show more information</li>
              <li>Balance content density</li>
            </ul>
          </li>
          <li>
            <strong>Desktop (> 1024px):</strong>
            <ul>
              <li>Multi-column layouts</li>
              <li>Full feature set</li>
              <li>Optimize for productivity</li>
            </ul>
          </li>
        </ul>
      </details>
    </div>
  );
};

export default Responsive[Component]Example;
```

### What This Demonstrates

- ✅ Responsive breakpoints
- ✅ Viewport size detection
- ✅ Conditional rendering based on screen size
- ✅ PatternFly Grid and Stack layouts
- ✅ Mobile-first design approach
- ✅ Touch-friendly sizing

### Try It Out

**Test different breakpoints:**
```tsx
// Custom breakpoints
const breakpoints = {
  xs: 0,
  sm: 576,
  md: 768,
  lg: 992,
  xl: 1200,
  xxl: 1400,
};

const getCurrentBreakpoint = (width: number) => {
  if (width < breakpoints.sm) return 'xs';
  if (width < breakpoints.md) return 'sm';
  if (width < breakpoints.lg) return 'md';
  if (width < breakpoints.xl) return 'lg';
  if (width < breakpoints.xxl) return 'xl';
  return 'xxl';
};
```

---

## Example 6: Testing

Comprehensive testing examples with React Testing Library.

### Code

```tsx
import { render, screen, waitFor } from '@testing-library/react';
import userEvent from '@testing-library/user-event';
import { [Component]Example } from './[Component]Example';

describe('[Component]', () => {
  describe('Rendering', () => {
    it('renders with default props', () => {
      render(<[Component]Example />);

      expect(screen.getByRole('[role]')).toBeInTheDocument();
      expect(screen.getByLabelText('[aria-label]')).toBeInTheDocument();
    });

    it('renders all items from data', () => {
      render(<[Component]Example />);

      const items = screen.getAllByRole('[itemRole]');
      expect(items).toHaveLength(expectedCount);
    });

    it('applies correct ARIA attributes', () => {
      render(<[Component]Example />);

      const component = screen.getByRole('[role]');
      expect(component).toHaveAttribute('aria-label', '[expectedLabel]');
      expect(component).toHaveAttribute('aria-describedby');
    });
  });

  describe('User Interactions', () => {
    it('handles selection', async () => {
      const user = userEvent.setup();
      render(<[Component]Example />);

      const firstItem = screen.getAllByRole('[itemRole]')[0];
      await user.click(firstItem);

      await waitFor(() => {
        expect(firstItem).toHaveAttribute('aria-selected', 'true');
      });
    });

    it('handles keyboard navigation', async () => {
      const user = userEvent.setup();
      render(<[Component]Example />);

      const component = screen.getByRole('[role]');
      component.focus();

      await user.keyboard('{ArrowDown}');
      await user.keyboard('{Enter}');

      // Assert expected behavior
    });

    it('handles multiple selection', async () => {
      const user = userEvent.setup();
      render(<[Component]Example />);

      const items = screen.getAllByRole('[itemRole]');

      await user.click(items[0]);
      await user.click(items[1], { ctrlKey: true });

      expect(items[0]).toHaveAttribute('aria-selected', 'true');
      expect(items[1]).toHaveAttribute('aria-selected', 'true');
    });
  });

  describe('States', () => {
    it('shows loading state', () => {
      render(<[Component]Example isLoading />);

      expect(screen.getByRole('progressbar')).toBeInTheDocument();
      expect(screen.queryByRole('[itemRole]')).not.toBeInTheDocument();
    });

    it('shows empty state', () => {
      render(<[Component]Example data={[]} />);

      expect(screen.getByText(/no results/i)).toBeInTheDocument();
    });

    it('shows error state', () => {
      const errorMessage = 'Failed to load data';
      render(<[Component]Example error={errorMessage} />);

      expect(screen.getByText(errorMessage)).toBeInTheDocument();
      expect(screen.getByRole('alert')).toBeInTheDocument();
    });
  });

  describe('Accessibility', () => {
    it('is keyboard accessible', async () => {
      const user = userEvent.setup();
      render(<[Component]Example />);

      // Tab through interactive elements
      await user.tab();
      expect(screen.getByRole('[firstInteractiveRole]')).toHaveFocus();

      await user.tab();
      expect(screen.getByRole('[secondInteractiveRole]')).toHaveFocus();
    });

    it('announces changes to screen readers', async () => {
      const user = userEvent.setup();
      render(<[Component]Example />);

      const liveRegion = screen.getByRole('status');
      const firstItem = screen.getAllByRole('[itemRole]')[0];

      await user.click(firstItem);

      await waitFor(() => {
        expect(liveRegion).toHaveTextContent(/selected/i);
      });
    });

    it('has no accessibility violations', async () => {
      const { container } = render(<[Component]Example />);

      // Using jest-axe or similar
      const results = await axe(container);
      expect(results).toHaveNoViolations();
    });
  });

  describe('Integration', () => {
    it('integrates with forms', async () => {
      const handleSubmit = jest.fn();
      render(
        <form onSubmit={handleSubmit}>
          <[Component]Example />
          <button type="submit">Submit</button>
        </form>
      );

      const user = userEvent.setup();
      const item = screen.getAllByRole('[itemRole]')[0];

      await user.click(item);
      await user.click(screen.getByText('Submit'));

      expect(handleSubmit).toHaveBeenCalledWith(
        expect.objectContaining({
          // Expected form data
        })
      );
    });

    it('handles async data loading', async () => {
      const mockFetch = jest.fn().mockResolvedValue({
        json: () => Promise.resolve([/* data */]),
      });
      global.fetch = mockFetch;

      render(<[Component]Example />);

      await waitFor(() => {
        expect(screen.getAllByRole('[itemRole]')).toHaveLength(expectedCount);
      });

      expect(mockFetch).toHaveBeenCalledTimes(1);
    });
  });
});
```

### What This Demonstrates

- ✅ Component rendering tests
- ✅ User interaction tests
- ✅ State management tests
- ✅ Accessibility tests
- ✅ Keyboard navigation tests
- ✅ Integration tests
- ✅ Async behavior tests

### Try It Out

**Add more test cases:**
```tsx
// Edge cases
it('handles empty string values', () => {
  render(<[Component]Example value="" />);
  // Assertions
});

// Performance testing
it('renders large datasets efficiently', () => {
  const largeDataset = Array.from({ length: 10000 }, (_, i) => ({ id: i }));
  const startTime = performance.now();
  render(<[Component]Example data={largeDataset} />);
  const endTime = performance.now();
  expect(endTime - startTime).toBeLessThan(1000); // Under 1 second
});

// Snapshot testing
it('matches snapshot', () => {
  const { container } = render(<[Component]Example />);
  expect(container).toMatchSnapshot();
});
```

---

## Props Reference

Quick reference for all available props.

### Essential Props

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `[prop1]` | `[type]` | `[default]` | [Description] |
| `[prop2]` | `[type]` | `[default]` | [Description] |
| `[prop3]` | `[type]` | `[default]` | [Description] |

### Optional Props

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `[optionalProp1]` | `[type]` | `undefined` | [Description] |
| `[optionalProp2]` | `[type]` | `undefined` | [Description] |

### Event Props

| Prop | Type | Description |
|------|------|-------------|
| `on[Event1]` | `(params) => void` | [When this fires] |
| `on[Event2]` | `(params) => void` | [When this fires] |

### Styling Props

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `variant` | `[variants]` | `'default'` | Visual variant |
| `className` | `string` | `undefined` | Custom CSS class |

---

## Common Patterns

### Pattern 1: [Pattern Name]

**Use case:** [When to use this pattern]

```tsx
// Implementation
<[Component]
  [pattern-specific-props]
>
  {/* Pattern content */}
</[Component>
```

### Pattern 2: [Pattern Name]

**Use case:** [When to use this pattern]

```tsx
// Implementation
```

---

## Troubleshooting

### Issue: [Common Problem]

**Symptoms:**
- [Symptom 1]
- [Symptom 2]

**Solution:**
```tsx
// Fixed code
```

**Explanation:** [Why this fixes it]

---

## Next Steps

1. **Copy an example** that matches your needs
2. **Customize** the props and data
3. **Test** with your actual use case
4. **Enhance** with additional features
5. **Review** accessibility with testing checklist

## Resources

- **Component Documentation:** [Link]
- **API Reference:** [Link]
- **Live Examples:** [Link]
- **Accessibility Guide:** [Link]

---

## Questions?

Need help with a specific feature or use case? Let me know what you want to build and I can provide a customized example!
```

## Phase 4: Quality Assurance

Before finalizing the playground:

✅ **Verify:**
- All code examples are complete and runnable
- Imports are correct and current
- Props match PatternFly documentation
- TypeScript types are accurate
- Examples demonstrate realistic use cases
- Progression from basic to advanced makes sense
- Accessibility features are properly implemented
- Testing examples are accurate

✅ **Include:**
- At least 5 diverse examples (basic, interactive, advanced, accessibility, responsive)
- Complete testing suite example
- Props reference table
- Common patterns
- Troubleshooting section
- Debug/logging features for learning
- Performance optimization examples
- Integration examples

❌ **Avoid:**
- Code with syntax errors
- Missing imports or dependencies
- Unrealistic or trivial examples
- Skipping accessibility or responsive design
- Examples without explanation
- Deprecated patterns
- Incomplete error handling

## Output Format

Provide a comprehensive playground with:

1. Overview and installation instructions
2. Progressive examples (basic → advanced)
3. Each example includes:
   - Complete, runnable code
   - Explanation of what it demonstrates
   - "Try it out" suggestions for experimentation
   - Debugging/logging features
4. Accessibility showcase
5. Responsive design example
6. Complete testing suite
7. Props reference
8. Common patterns
9. Troubleshooting guide
10. Next steps and resources

The playground should be a complete learning resource that someone can copy, run, and learn from immediately.
