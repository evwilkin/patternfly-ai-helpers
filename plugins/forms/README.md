# Forms Plugin

Build accessible forms, implement validation, and integrate with form libraries using PatternFly components.

## Overview

The Forms plugin helps you create production-ready forms with PatternFly React components, implementing best practices for accessibility, validation, and user experience. It supports integration with popular form libraries like React Hook Form and Formik while maintaining PatternFly's design system standards.

## Commands

### `/build-form`

Generate accessible forms with PatternFly components.

**Use cases:**
- Create new forms from scratch with appropriate PatternFly components
- Build complex multi-section forms with proper grouping
- Implement various input types (text, select, checkbox, radio, date, etc.)
- Add form layouts (horizontal, vertical, grid-based)
- Include helper text and field descriptions
- Set up proper labels and ARIA attributes
- Implement loading and disabled states
- Add form actions (submit, cancel, reset)

**Example usage:**
```
/build-form

I need a user registration form with email, password, and profile fields
```

**What it generates:**
- Complete form component with PatternFly Form, FormGroup, and input components
- Proper field organization and layout
- Accessible labels and helper text
- TypeScript interfaces for form data
- Form state management
- Submit and reset handlers
- Loading and error states

---

### `/add-validation`

Implement form validation with error handling.

**Use cases:**
- Add client-side validation rules to form fields
- Implement custom validation logic
- Display inline error messages
- Add field-level and form-level validation
- Implement async validation (API checks)
- Show validation on blur, change, or submit
- Add success/warning states
- Create reusable validation utilities

**Example usage:**
```
/add-validation

Add validation to the registration form: email format, password strength, required fields
```

**What it generates:**
- Validation rules and logic
- Error state management
- Helper text with error messages
- Validated state for FormGroup components
- Custom validation functions
- Error message utilities
- Accessibility announcements for errors
- TypeScript types for validation

---

### `/integrate-form-library`

Integrate with React Hook Form, Formik, or other form libraries.

**Use cases:**
- Connect PatternFly components with React Hook Form
- Integrate with Formik for complex forms
- Use validation schema libraries (Yup, Zod)
- Implement field arrays and dynamic forms
- Add form context and hooks
- Handle form submission with libraries
- Integrate with form state management
- Create reusable form field wrappers

**Example usage:**
```
/integrate-form-library

Integrate the registration form with React Hook Form and Zod validation
```

**What it generates:**
- Library-specific integration code
- Custom PatternFly component wrappers
- Form provider setup
- Validation schema definitions
- Hook implementations
- Field registration patterns
- Error handling with library APIs
- TypeScript types for library integration

---

## Features

### Comprehensive Form Components
- **Basic Inputs**: TextInput, TextArea, NumberInput
- **Selection**: Select, Checkbox, Radio, Switch
- **Specialized**: DatePicker, TimePicker, FileUpload
- **Advanced**: Multi-select, TypeAhead, SearchInput

### Validation Patterns
- Required field validation
- Format validation (email, URL, phone)
- Length constraints (min/max)
- Pattern matching (regex)
- Custom validation functions
- Async validation (server-side checks)
- Cross-field validation
- Conditional validation

### Accessibility Features
- Proper ARIA labels and descriptions
- Error announcements with screen readers
- Keyboard navigation support
- Focus management
- Required field indicators
- Invalid state communication
- Helper text associations

### Form Layouts
- Vertical forms
- Horizontal forms
- Grid-based layouts
- Multi-column forms
- Grouped sections
- Wizard/step forms
- Inline forms

### State Management
- Loading states during submission
- Disabled states for fields
- Read-only fields
- Success/error states
- Dirty/touched tracking
- Form reset functionality

### Integration Support
- React Hook Form
- Formik
- Final Form
- Custom solutions
- Validation libraries (Yup, Zod, Joi)

## Best Practices

### Accessibility
- Always provide labels for inputs
- Use helper text for field guidance
- Announce errors to screen readers
- Maintain logical tab order
- Include required field indicators
- Provide clear error messages

### User Experience
- Validate on appropriate events (blur vs. change)
- Show inline errors near fields
- Disable submit during loading
- Provide clear success feedback
- Support keyboard shortcuts
- Implement autosave when appropriate

### Performance
- Debounce validation for expensive checks
- Lazy load large select options
- Virtualize long lists
- Memoize validation functions
- Optimize re-renders

### Code Organization
- Separate validation logic
- Create reusable field components
- Extract form sections
- Type form data properly
- Use composition for complex forms

## Examples

### Simple Contact Form
```typescript
import { Form, FormGroup, TextInput, Button } from '@patternfly/react-core';

const ContactForm = () => {
  const [name, setName] = useState('');
  const [email, setEmail] = useState('');

  return (
    <Form>
      <FormGroup label="Name" isRequired fieldId="name">
        <TextInput
          id="name"
          value={name}
          onChange={(_, value) => setName(value)}
        />
      </FormGroup>
      <FormGroup label="Email" isRequired fieldId="email">
        <TextInput
          id="email"
          type="email"
          value={email}
          onChange={(_, value) => setEmail(value)}
        />
      </FormGroup>
      <Button type="submit">Submit</Button>
    </Form>
  );
};
```

### With Validation
```typescript
const [emailError, setEmailError] = useState('');

const validateEmail = (value: string) => {
  if (!value) {
    return 'Email is required';
  }
  if (!/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(value)) {
    return 'Invalid email format';
  }
  return '';
};

<FormGroup
  label="Email"
  isRequired
  fieldId="email"
  validated={emailError ? 'error' : 'default'}
  helperTextInvalid={emailError}
>
  <TextInput
    id="email"
    type="email"
    value={email}
    onChange={(_, value) => {
      setEmail(value);
      setEmailError(validateEmail(value));
    }}
    validated={emailError ? 'error' : 'default'}
  />
</FormGroup>
```

### With React Hook Form
```typescript
import { useForm, Controller } from 'react-hook-form';

const { control, handleSubmit } = useForm();

<Controller
  name="email"
  control={control}
  rules={{ required: 'Email is required' }}
  render={({ field, fieldState }) => (
    <FormGroup
      label="Email"
      isRequired
      fieldId="email"
      validated={fieldState.error ? 'error' : 'default'}
      helperTextInvalid={fieldState.error?.message}
    >
      <TextInput
        {...field}
        id="email"
        type="email"
        validated={fieldState.error ? 'error' : 'default'}
      />
    </FormGroup>
  )}
/>
```

## Resources

- [PatternFly Forms Documentation](https://www.patternfly.org/components/forms/form)
- [React Hook Form](https://react-hook-form.com/)
- [Formik](https://formik.org/)
- [Accessibility Guidelines](https://www.w3.org/WAI/WCAG21/Understanding/name-role-value.html)
- [Form Validation Patterns](https://www.patternfly.org/patterns/forms)

## Tips

1. **Start Simple**: Begin with basic forms and add complexity as needed
2. **Validate Appropriately**: Choose validation timing based on user experience
3. **Provide Feedback**: Always show clear success and error states
4. **Test Accessibility**: Use screen readers to verify form accessibility
5. **Handle Edge Cases**: Consider empty states, loading, and error scenarios
6. **Mobile Friendly**: Ensure forms work well on all device sizes
7. **Performance**: Monitor re-renders and optimize validation logic

## Support

For issues, questions, or contributions related to this plugin, please refer to the main PatternFly AI Helpers repository.
