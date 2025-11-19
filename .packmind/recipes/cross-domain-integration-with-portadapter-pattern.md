Integrate a consumer domain with a provider domain using lazy dependency injection through the Port/Adapter pattern to enable cross-domain operations while avoiding circular dependencies and maintaining loose coupling.

## When to Use

- When a domain needs functionality from another domain (e.g., Accounts needs Spaces)
- When you want to avoid tight coupling between domain packages
- When circular dependencies need to be prevented through lazy loading
- When the dependency is optional and the consumer should gracefully handle its absence
- When you need to mock cross-domain dependencies easily in tests

## Context Validation Checkpoints

* [ ] Does the provider domain already expose an adapter via a getter method (e.g., getSpacesAdapter())?
* [ ] Is the port interface defined in @packmind/shared/types/ports/?
* [ ] Is the provider domain registered in HexaRegistry before the consumer domain?
* [ ] Should the cross-domain dependency be optional or required?
* [ ] Which use cases in the consumer domain need to call the provider's operations?

## Recipe Steps

### Step 1: Import Port Interface in Consumer Hexa

Import only the port interface from @packmind/shared/types, never the concrete hexa implementation. This ensures loose coupling and prevents circular dependencies.

```typescript
import { ISpacesPort } from '@packmind/shared/types';
import { SpacesHexa } from '@packmind/spaces';
```

### Step 2: Add Optional Port to Consumer Hexa Options

Extend the consumer's hexa options to accept an optional port injection for flexibility in testing and runtime configuration.

```typescript
export type AccountsHexaOpts = BaseHexaOpts & {
  spacesPort?: ISpacesPort;
};
```

### Step 3: Retrieve Port from Registry with Lazy Loading

Use the registry to get the provider hexa and extract its adapter with try-catch for optional dependencies. This enables lazy loading and graceful degradation.

```typescript
let spacesPort: ISpacesPort | undefined = opts?.spacesPort;
if (!spacesPort) {
  try {
    const spacesHexa = registry.get(SpacesHexa);
    spacesPort = spacesHexa.getSpacesAdapter();
  } catch (error) {
    this.logger.debug('SpacesHexa not available');
  }
}
this.hexa = new AccountsHexaFactory(dataSource, spacesPort);
```

### Step 4: Thread Port Through Factory and Use Cases

Pass the port through the factory to the use cases aggregator, then to individual use cases. This maintains clean dependency flow and enables injection at all layers.

```typescript
export class AccountsHexaFactory {
  constructor(
    private readonly dataSource: DataSource,
    private readonly spacesPort?: ISpacesPort,
  ) {
    this.useCases = new AccountsUseCases(
      this.services,
      this.spacesPort,
    );
  }
}
```

### Step 5: Use Null-Safe Calls in Consumer Use Cases

Check if the port is available before calling it, handling absence gracefully. This ensures the use case works whether the dependency is present or not.

```typescript
export class CreateOrganizationUseCase {
  constructor(
    private readonly orgService: OrganizationService,
    private readonly spacesPort?: ISpacesPort,
  ) {}

  async execute(cmd: CreateOrganizationCommand) {
    const org = await this.orgService.createOrganization(cmd.name);
    
    if (this.spacesPort) {
      await this.spacesPort.createSpace('Global', org.id);
    }
    
    return { organization: org };
  }
}
```

### Step 6: Register Provider Before Consumer in App Module

Ensure the provider hexa is registered in the registry before the consumer to enable lazy lookup. Order matters for dependency resolution.

```typescript
HexaRegistryModule.register({
  hexas: [
    SpacesHexa,     // Provider first
    AccountsHexa,   // Consumer after
  ],
}),
```

### Step 7: Add Consumer Package Dependency

Update the consumer's package.json to include the provider package if direct type imports are needed. This ensures TypeScript and webpack can resolve the imports.

```json
{
  "dependencies": {
    "@packmind/shared": "*",
    "@packmind/spaces": "*"
  }
}
```
