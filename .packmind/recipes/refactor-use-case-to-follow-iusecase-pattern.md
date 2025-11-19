Refactor existing use cases to implement the IUseCase pattern for consistent command/response typing and enhanced business rule enforcement, ensuring maintainability and clarity across your application's architecture.

## When to Use

- When you have an existing use case that doesn't follow the IUseCase pattern
- When you need to add new business rules or validation to a use case
- When you want to standardize use case interfaces across your domain
- When you're migrating from legacy use case patterns to hexagonal architecture standards

## Context Validation Checkpoints

* [ ] Have you identified the use case that needs refactoring?
* [ ] Do you know what command parameters are needed?
* [ ] What business rules need to be enforced?
* [ ] Are there existing tests that need to be updated?
* [ ] Which repository methods are needed to support the business rules?

## Recipe Steps

### Step 1: Create Use Case Type Definitions

Create a new file following the naming convention I{UseCaseName}.ts in src/domain/useCases/. Define the command type extending PackmindCommand and the use case interface extending IUseCase. Return the entity directly, not wrapped in a response object.

```typescript
// src/domain/useCases/IAddGitRepo.ts
import { PackmindCommand, IUseCase } from '@packmind/shared';
import { GitRepo } from '../entities/GitRepo';
import { GitProviderId } from '../entities/GitProvider';

export type AddGitRepoCommand = PackmindCommand & {
  gitProviderId: GitProviderId;
  owner: string;
  repo: string;
  branch: string;
};

// Return entity directly, avoid wrapper types
export type IAddGitRepoUseCase = IUseCase<AddGitRepoCommand, GitRepo>;
```

### Step 2: Update Use Case Implementation

Refactor the existing use case class to implement the new interface. Change the execute method to accept a command object and include comprehensive business rule validation with clear error messages.

```typescript
export class AddGitRepoUseCase implements IAddGitRepoUseCase {
  async execute(command: AddGitRepoCommand): Promise<GitRepo> {
    const { organizationId, gitProviderId, owner, repo, branch } = command;
    
    // Business rule validation
    if (!gitProviderId) {
      throw new Error('Git provider ID is required');
    }
    
    // Domain logic with proper error messages
    const existingRepo = await this.service.findByUniqueConstraint(
      owner, repo, branch, organizationId
    );
    
    if (existingRepo) {
      throw new Error(
        `Repository ${owner}/${repo} on branch '${branch}' already exists`
      );
    }
    
    return this.service.create({ owner, repo, branch, providerId: gitProviderId });
  }
}
```

### Step 3: Update Repository Layer (If Needed)

Add new repository methods to support enhanced business rules. Create methods with proper TypeORM queries for uniqueness checks, organization scoping, and other validation needs.

```typescript
// Interface
export interface IGitRepoRepository extends IRepository<GitRepo> {
  findByOwnerRepoAndBranchInOrganization(
    owner: string,
    repo: string,
    branch: string,
    organizationId: OrganizationId,
  ): Promise<GitRepo | null>;
}

// Implementation with proper query
async findByOwnerRepoAndBranchInOrganization(
  owner: string,
  repo: string,
  branch: string,
  organizationId: OrganizationId,
): Promise<GitRepo | null> {
  return this.repository
    .createQueryBuilder('gitRepo')
    .innerJoin('provider', 'provider', 'gitRepo.providerId = provider.id')
    .where('gitRepo.owner = :owner', { owner })
    .andWhere('gitRepo.repo = :repo', { repo })
    .andWhere('gitRepo.branch = :branch', { branch })
    .andWhere('provider.organizationId = :organizationId', { organizationId })
    .getOne();
}
```

### Step 4: Update Service Layer

Refactor services to use the command pattern instead of spread parameters. Service methods should accept command objects and delegate to use cases.

```typescript
// After: Command pattern
public async addGitRepo(command: AddGitRepoCommand): Promise<GitRepo> {
  return this._addGitRepo.execute(command);
}
```

### Step 5: Update API Layer

Modify controllers and services to create command objects from request parameters. Ensure userId and organizationId are properly extracted from authentication context.

```typescript
// API Service
async addRepositoryToProvider(
  userId: UserId,
  organizationId: OrganizationId,
  gitProviderId: GitProviderId,
  owner: string,
  repo: string,
  branch: string,
): Promise<GitRepo> {
  const command = {
    userId,
    organizationId,
    gitProviderId,
    owner,
    repo,
    branch,
  };
  
  return await this.gitHexa.addGitRepo(command);
}
```

### Step 6: Update Tests

Refactor tests to use the new command structure. Create command objects with all required fields and test all business rule scenarios including validation errors.

```typescript
const command: AddGitRepoCommand = {
  userId,
  organizationId,
  gitProviderId,
  owner: 'testowner',
  repo: 'testrepo',
  branch: 'main',
};

const result = await useCase.execute(command);
expect(result).toEqual(expectedRepo); // Direct entity comparison
```

### Step 7: Implement Business Rules Pattern

Structure business rules in a consistent order: extract and validate required fields, perform basic validation, validate external dependencies, enforce business rules, check uniqueness constraints, and finally create and return the entity. Always throw errors with specific, actionable messages.
