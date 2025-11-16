Build a React form component with client-side validation and error handling using modern React patterns

## When to Use

- When creating user input forms that require validation
- When implementing forms with multiple fields and complex validation rules
- When building forms that need to display inline error messages

## Context Validation Checkpoints

* [ ] What fields are required in the form?
* [ ] What validation rules apply to each field?
* [ ] Should validation occur on blur, onChange, or onSubmit?
* [ ] What should happen on successful form submission?

## Recipe Steps

### Step 1: Set Up Form State

Initialize form state using useState or a form library, including field values, errors, and submission status.

```typescript
const [formData, setFormData] = useState({ email: '', name: '' });
const [errors, setErrors] = useState<Record<string, string>>({});
const [isSubmitting, setIsSubmitting] = useState(false);
```

### Step 2: Implement Validation Logic

Create validation functions for each field and form-level validation, returning error messages for invalid inputs.

```typescript
function validateEmail(email: string): string | null {
  if (!email) return 'Email is required';
  if (!/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email)) {
    return 'Invalid email format';
  }
  return null;
}
```

### Step 3: Create Form Component

Build the form JSX with input fields, error displays, and submit button, handling onChange and onSubmit events.

```typescript
<form onSubmit={handleSubmit}>
  <PMInput
    value={formData.email}
    onChange={(e) => handleChange('email', e.target.value)}
    error={errors.email}
  />
  {errors.email && <Text color='error'>{errors.email}</Text>}
  <PMButton type='submit' disabled={isSubmitting}>Submit</PMButton>
</form>
```

### Step 4: Handle Form Submission

Implement submit handler that validates all fields, prevents double submission, and processes the form data.

```typescript
async function handleSubmit(e: FormEvent) {
  e.preventDefault();
  if (isSubmitting) return;
  
  const validationErrors = validateForm(formData);
  if (Object.keys(validationErrors).length > 0) {
    setErrors(validationErrors);
    return;
  }
  
  setIsSubmitting(true);
  try {
    await submitForm(formData);
  } finally {
    setIsSubmitting(false);
  }
}
```
