<!-- start: Packmind recipes -->
# Packmind Recipes

🚨 **MANDATORY STEP** 🚨

Before writing, editing, or generating ANY code:

**ALWAYS READ**: the available recipes below to see what recipes are available

## Recipe Usage Rules:
- **MANDATORY**: Always check the recipes list first
- **CONDITIONAL**: Only read/use individual recipes if they are relevant to your task
- **OPTIONAL**: If no recipes are relevant, proceed without using any

## Recipe Usage Tracking:
When you DO use or apply a relevant Packmind recipe from .packmind/recipes/, you MUST call the 'packmind_notify_recipe_usage' MCP tool with:
* Recipe slugs array (e.g., ["recipe-name"] from "recipe-name.md")
* aiAgent: "Claude Code"
* gitRepo: "repository"
* target: "/"

**Remember: Always check the recipes list first, but only use recipes that actually apply to your specific task.**`

## Available recipes

* [Create New Package in Monorepo](.packmind/recipes/create-new-package-in-monorepo.md): Create a new buildable TypeScript package in the Packmind monorepo using Nx tools to establish a shared library for code reuse across applications and packages when setting up common utilities or implementing domain-specific logic.
* [Cross-Domain Integration with Port/Adapter Pattern](.packmind/recipes/cross-domain-integration-with-portadapter-pattern.md): Integrate a consumer domain with a provider domain using lazy dependency injection through the Port/Adapter pattern to enable cross-domain operations while avoiding circular dependencies and maintaining loose coupling.
* [How to Write TypeORM Migrations in Packmind](.packmind/recipes/how-to-write-typeorm-migrations-in-packmind.md): Write TypeORM migrations in the Packmind monorepo to manage database schema changes effectively while ensuring proper logging and rollback capabilities.
<!-- end: Packmind recipes -->
<!-- start: Packmind standards -->
# Packmind Standards

Before starting your work, make sure to review the coding standards relevant to your current task.

Always consult the sections that apply to the technology, framework, or type of contribution you are working on.

All rules and guidelines defined in these standards are mandatory and must be followed consistently.

Failure to follow these standards may lead to inconsistencies, errors, or rework. Treat them as the source of truth for how code should be written, structured, and maintained.

## Standard: Back-end repositories SQL queries using TypeORM

Implement SQL query guidelines using TypeORM's QueryBuilder in back-end repositories under /infra/repositories/*Repository.ts to enhance type safety, prevent SQL injection, and improve code maintainability when writing database queries, including lookups, joins, and handling soft-deleted entities. :
* Handle soft-deleted entities properly using withDeleted() or includeDeleted options. Always respect the QueryOption parameter when provided, and only include deleted entities when explicitly requested.
* Use IN clause with array parameterization for filtering by multiple values. Always pass arrays as spread parameters using :...paramName syntax to ensure proper parameterization.
* Use TypeORM's QueryBuilder with parameterized queries instead of raw SQL strings. Always pass parameters as objects to where(), andWhere(), and other query methods to prevent SQL injection and ensure type safety.

Full standard is available here for further request: [Back-end repositories SQL queries using TypeORM](.packmind/standards/back-end-repositories-sql-queries-using-typeorm.md)

## Standard: Frontend Data Flow

Apply this standard when building frontend routes with React Router v7 and TanStack Query to ensure consistent data flow patterns and optimal user experience. :
* Access data via query or mutation hooks in frontend route modules rather than calling gateways directly to maintain separation between data access and presentation layers
* Consume data in route module components using the useLoaderData() hook to access data returned by the clientLoader
* Define a crumb property in the handle export of route modules to enable automatic navigation breadcrumb generation
* Enable query options conditionally using the enabled property to prevent execution when required parameters are missing or invalid
* Export query hooks (e.g., useGetStandardByIdQuery) alongside query options to provide consistent component-level data access patterns
* Export query options as standalone functions (e.g., getStandardByIdOptions) separate from hooks to enable reuse in both hooks and route loaders
* Name route module default export functions with a suffix of RouteModule (e.g., StandardDetailRouteModule) to clearly identify route-level components
* Store domain queries in the domain folder organized by entity at apps/frontend/src/domains/{entity}/api/queries/ to maintain clear separation of concerns and domain boundaries
* Use clientLoader function (not loader) in route modules for data fetching when using React Router in SPA mode to ensure proper client-side data loading
* Use queryClient.ensureQueryData() or queryClient.fetchQuery() in clientLoader to preload data before rendering and leverage TanStack Query's caching mechanisms

Full standard is available here for further request: [Frontend Data Flow](.packmind/standards/frontend-data-flow.md)

## Standard: Port-Adapter Cross-Domain Integration

Apply the Port/Adapter pattern to enable cross-domain communication while preventing circular dependencies and maintaining loose coupling in the DDD monorepo. :
* Declare all Command and Response types that define contracts between domains in packages/types/src/<domain>/contracts/ to ensure a single source of truth and prevent import cycles between domain packages.
* Define port interfaces in @packmind/types with domain-specific contracts that expose only the operations needed by consumers, where each method accepts a Command type and returns a Response type or domain entity.
* Expose adapters through public getter methods in the Hexa class that return the port interface implementation, as this is the only way external domains should access another domain's functionality.
* Import only port interfaces from @packmind/types in consumer domain Hexas, allowing direct imports of provider Hexa classes only for retrieving the adapter via the registry, but storing the reference typed as the port interface.
* Use async initialize methods for deferred cross-domain dependencies by implementing an async initialize() method on the HexaFactory when a domain needs dependencies that aren't available during construction, retrieving dependencies from the registry using isRegistered() checks before calling get().

Full standard is available here for further request: [Port-Adapter Cross-Domain Integration](.packmind/standards/port-adapter-cross-domain-integration.md)

## Standard: TanStack Query Key Management

Manage TanStack Query key structures using hierarchical prefix matching and dedicated queryKeys.ts files in React applications to ensure efficient cache invalidation and type-safe query management when handling cross-domain data operations. :
* Define base query key arrays as const to enable precise invalidation patterns and avoid duplication
* Define domain query scope as a separate const outside enum to maintain clear separation between scope and operations
* Define query keys in a dedicated queryKeys.ts file in the domain's api folder for centralized management
* Follow hierarchical query key structure: organization scope, domain scope, operation, then identifiers for consistent invalidation patterns
* Limit cross-domain imports to only query key constants and enums to prevent runtime coupling and circular dependencies
* Use query invalidation with prefix matching from key start in correct hierarchical order

Full standard is available here for further request: [TanStack Query Key Management](.packmind/standards/tanstack-query-key-management.md)

## Standard: Use Case Architecture Patterns

Structure use cases in the Packmind monorepo by following hexagonal architecture principles with command/response patterns, specific typing, and separation of concerns for authentication and authorization to ensure consistent, type-safe, and maintainable cross-domain integrations when creating or refactoring use cases. :
* Accept commands as single parameters in hexagon facade methods rather than multiple individual parameters to ensure consistency and easier parameter additions
* Define each use case contract in its own file at packages/types/src/{domain}/contracts/{UseCaseName}.ts with Command type, Response type, and UseCase interface exports
* Export exactly three type definitions from each use case contract file: {Name}Command for input parameters, {Name}Response for return value, and I{Name}UseCase as the interface combining both
* Extend AbstractAdminUseCase and implement executeForAdmins method for use cases requiring admin privileges, with automatic validation that the user is a member with admin role
* Extend AbstractMemberUseCase and implement executeForMembers method for use cases requiring the user to be a member of an organization, with automatic user and organization validation
* Extend PackmindCommand for authenticated use case commands that include userId and organizationId, or extend PublicPackmindCommand for public endpoints without authentication
* Implement IPublicUseCase interface directly with an execute method for public use cases that don't require authentication, without extending any abstract use case class
* Never spread commands as multiple arguments in hexagon or UseCase classes; always pass the complete command object to maintain type safety and reduce errors
* Restrict use case classes to expose only the execute method for public use cases or executeForMembers/executeForAdmins methods for member/admin use cases, with no other public methods
* Reuse existing use cases through port/adapter interfaces instead of instantiating them directly within use cases
* Use Gateway<IUseCase> type helper for authenticated operations or PublicGateway<IPublicUseCase> for public operations in frontend gateway interfaces to ensure proper command/response typing

Full standard is available here for further request: [Use Case Architecture Patterns](.packmind/standards/use-case-architecture-patterns.md)
<!-- end: Packmind standards -->
