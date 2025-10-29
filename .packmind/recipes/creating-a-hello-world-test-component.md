Create a simple Hello World component to verify the component creation workflow and test the basic React component structure, providing a quick validation that the development environment is properly configured.

## When to Use

- When you need to verify your React development environment is working correctly
- When you want to test the component creation and rendering pipeline
- When you need a minimal example to demonstrate component basics to new developers
- When setting up a new project and need a simple smoke test component

## Context Validation Checkpoints

* [ ] Confirm the target directory for the component (e.g., src/components/)
* [ ] Verify which UI library or framework is being used (React, Vue, etc.)
* [ ] Check if TypeScript or JavaScript is the project standard
* [ ] Determine if any specific naming conventions apply to components
* [ ] Confirm if tests should be co-located or in a separate test directory

## Recipe Steps

### Step 1: Create the component file

Create a new TypeScript file for the HelloWorld component in the appropriate components directory following the project's file naming conventions.

```typescript
// src/components/HelloWorld.tsx
export const HelloWorld = () => {
  return <div>Hello World</div>;
};
```

### Step 2: Add props interface (optional)

If the component needs to accept props, define a TypeScript interface for type safety and better developer experience.

```typescript
interface HelloWorldProps {
  name?: string;
}

export const HelloWorld = ({ name = 'World' }: HelloWorldProps) => {
  return <div>Hello {name}</div>;
};
```

### Step 3: Export from index

Add the component to the barrel export file (index.ts) in the components directory to make it easily importable throughout the application.

### Step 4: Create component test

Write a basic test file to verify the component renders correctly, following the project's testing conventions and using the appropriate testing library.

```typescript
import { render, screen } from '@testing-library/react';
import { HelloWorld } from './HelloWorld';

it('renders hello world message', () => {
  render(<HelloWorld />);
  expect(screen.getByText('Hello World')).toBeInTheDocument();
});
```

### Step 5: Verify and test

Run the test suite to ensure the component renders correctly and verify it can be imported and used in other parts of the application without errors.
