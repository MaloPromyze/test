Create a comprehensive test class for UseCases to ensure consistent testing patterns and thorough coverage of various execution scenarios in the Packmind monorepo.

## When to Use

- When creating a new UseCase and need to write comprehensive tests
- When following the established testing patterns for UseCases in the monorepo
- When ensuring proper mock setup, test organization, and coverage

## Context Validation Checkpoints

* [ ] Have you identified all dependencies (repositories, services) used by the UseCase?
* [ ] Do you know the command and response types for the UseCase?
* [ ] Are there test factories available for the entities used in the UseCase?
* [ ] Have you reviewed similar UseCase tests in the codebase for reference?

## Recipe Steps

### Step 1: Set up Test File Structure

Create a test file named {UseCaseName}.spec.ts in the same directory as your UseCase implementation.

### Step 2: Import Required Dependencies

Import the UseCase, command types, repositories, services, stubLogger from @packmind/shared/test, test factories, and shared utilities like createOrganizationId and createUserId.

```typescript
import { UseCaseName } from './UseCaseName';
import { CommandType } from '../../../domain/useCases/IUseCaseName';
import { RepositoryInterface } from '../../domain/repositories/RepositoryInterface';
import { stubLogger } from '@packmind/shared/test';
import { PackmindLogger } from '@packmind/shared';
import { entityFactory } from '../../../../test/entityFactory';
import { createOrganizationId, createUserId } from '@packmind/shared';
```

### Step 3: Create Test Class Structure

Set up describe blocks with beforeEach for initialization, afterEach for cleanup, and nested describes for different scenarios (successful execution, validation fails, repository errors, service errors).

```typescript
describe('UseCaseName', () => {
  let useCase: UseCaseName;
  let mockRepository: jest.Mocked<RepositoryInterface>;
  let stubbedLogger: jest.Mocked<PackmindLogger>;

  beforeEach(() => {
    mockRepository = {
      methodName: jest.fn(),
    } as unknown as jest.Mocked<RepositoryInterface>;

    stubbedLogger = stubLogger();

    useCase = new UseCaseName(mockRepository, stubbedLogger);
  });

  afterEach(() => jest.clearAllMocks());

  describe('execute', () => {
    const validCommand: CommandType = { /* properties */ };

    describe('when successful execution', () => {
      let result: ReturnType;

      beforeEach(async () => {
        mockRepository.methodName.mockResolvedValue(expectedData);
        result = await useCase.execute(validCommand);
      });

      it('returns expected result', () => {
        expect(result).toEqual(expectedResult);
      });

      it('calls repository with correct parameters', () => {
        expect(mockRepository.methodName).toHaveBeenCalledWith(expectedParameters);
      });
    });

    describe('when validation fails', () => {
      it('throws error for invalid input', async () => {
        const invalidCommand = { /* invalid data */ };
        await expect(useCase.execute(invalidCommand)).rejects.toThrow('Expected error message');
      });
    });
  });
});
```

### Step 4: Test Organization Patterns

Follow established patterns: main describe for execute method, scenario-based nested describes (successful execution, validation fails, dependency errors), shared setup in beforeEach blocks, and clear assertive test names that describe expected behavior.

### Step 5: Mock Setup Best Practices

Mock all dependencies using jest.Mocked<Type>, include all methods used by the UseCase, use 'as unknown as jest.Mocked<Type>' pattern for complete mocks, and use test factories for creating consistent test data.

### Step 6: Ensure Test Coverage

Cover happy path with valid inputs, validation errors with invalid inputs, dependency errors from repositories and services, edge cases and boundary conditions, verify mock calls with correct parameters, and assert on returned data structure and content.

### Step 7: Apply Common Testing Patterns

Use stubLogger() instead of manually mocking PackmindLogger, use test factories for consistent data, create reusable command objects for different scenarios, verify both calls made to mocks and their parameters, and test both validation errors and dependency errors.
