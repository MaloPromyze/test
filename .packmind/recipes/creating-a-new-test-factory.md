Create a test factory for each entity to generate consistent and randomized test data, ensuring reliable testing and validation of your models.

## When to Use

- When you create a new entity and need to write tests for it
- When you need consistent test data across multiple test files
- When you want to generate randomized test data with sensible defaults

## Context Validation Checkpoints

* [ ] Have you identified all required properties of the entity?
* [ ] Do you have about five realistic examples to use in the factory?
* [ ] Is the Factory type imported from @packmind/shared/test?

## Recipe Steps

### Step 1: Create Factory File

Create a factory file in <package>/src/test/myModelFactory.ts for the entity MyModel. Each entity defined in a package should have a corresponding factory.

### Step 2: Implement Factory Function

Define the factory using the Factory type from @packmind/shared/test. The factory should include about five example objects and use randomIn to select one, then merge with any partial overrides passed as parameter.

```typescript
import { Factory, randomIn } from '@packmind/shared/test';

export const myModelFactory: Factory<MyModel> = (model?: Partial<MyModel>) => {
  const models: MyModel[] = [
    // About five examples generated
    { id: '1', name: 'Example 1', description: 'First example' },
    { id: '2', name: 'Example 2', description: 'Second example' },
    { id: '3', name: 'Example 3', description: 'Third example' },
    { id: '4', name: 'Example 4', description: 'Fourth example' },
    { id: '5', name: 'Example 5', description: 'Fifth example' },
  ];

  return {
    ...randomIn(models),
    ...model,
  };
};
```

### Step 3: Export Factory

Export the factory from the package's test folder so it can be imported and used in test files throughout the codebase.
