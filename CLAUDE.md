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
* [Create UseCase Test Class Template](.packmind/recipes/create-usecase-test-class-template.md): Create a comprehensive test class for UseCases to ensure consistent testing patterns and thorough coverage of various execution scenarios in the Packmind monorepo.
* [Creating a new test factory](.packmind/recipes/creating-a-new-test-factory.md): Create a test factory for each entity to generate consistent and randomized test data, ensuring reliable testing and validation of your models.
* [Cross-Domain Integration with Port/Adapter Pattern](.packmind/recipes/cross-domain-integration-with-portadapter-pattern.md): Integrate a consumer domain with a provider domain using lazy dependency injection through the Port/Adapter pattern to enable cross-domain operations while avoiding circular dependencies and maintaining loose coupling.
* [How to Write TypeORM Migrations in Packmind](.packmind/recipes/how-to-write-typeorm-migrations-in-packmind.md): Write TypeORM migrations in the Packmind monorepo to manage and version database schema changes with consistent logging, reversible rollbacks, and shared helpers so you can safely create or modify tables, columns, and foreign-key relationships whenever schema changes need to be tracked and reversible.
* [Refactor Use Case to Follow IUseCase Pattern](.packmind/recipes/refactor-use-case-to-follow-iusecase-pattern.md): Refactor existing use cases to implement the IUseCase pattern for consistent command/response typing and enhanced business rule enforcement, ensuring maintainability and clarity across your application's architecture.
* [Wrapping Chakra UI with Slot Components](.packmind/recipes/wrapping-chakra-ui-with-slot-components.md): Create slot components to wrap Chakra UI primitives for enhanced custom composition and API consistency in your design system.
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

## Standard: Front-end UI and Design Systems

Adopt guidelines for using Chakra UI v3 through the @packmind/ui design system in React applications to ensure consistent UI implementation and visual consistency, applying this standard when building or modifying any frontend components. :
* Never use vanilla HTML tags (div, span, button, input, etc.) in frontend component code; always use corresponding @packmind/ui components (PMBox, PMText, PMButton, PMInput, etc.) to ensure consistent styling and theming.
* Prefer using the design token 'full' instead of the literal value '100%' for width or height properties in UI components to maintain consistency with the design system.
* Use components imported from '@packmind/ui' instead of '@chakra-ui' packages to maintain a consistent UI abstraction layer, e.g., import { PMButton } from '@packmind/ui'; not import { Button } from '@chakra-ui/react';
* Use only semantic tokens to customize @packmind/ui components, such as colorPalette for color schemes, background.primary/secondary/tertiary for backgrounds, text.primary/secondary/tertiary for text colors, and border.primary/secondary/tertiary for borders, rather than hardcoded color values.

Full standard is available here for further request: [Front-end UI and Design Systems](.packmind/standards/front-end-ui-and-design-systems.md)

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

## Standard: Frontend Error Management

Establish frontend error management for apps/frontend/**/*.tsx that prescribes when to add React error boundaries beyond the global root.tsx fallback and how to handle errors they don't catch—such as event handlers, async code, SSR, or errors thrown in the boundary—by using TypeScript-typed guards (e.g., isPackmindError), try/catch for async operations, TanStack Query onError callbacks and mutation-pending checks to prevent double submissions, inline validation for expected API/user errors, and selective page- or component-level boundaries for isolated third-party widgets like CodeMirror, to reduce complexity, improve UX, and keep error flows maintainable in React/TypeScript projects built with Node.js and typical tooling (Vite/Webpack, ESLint/Prettier) and tested with Jest/Cypress. :
* Avoid overusing error boundaries as they increase code complexity and make error flows harder to trace
* Display validation errors inline near the relevant form fields for better user experience
* Do NOT use error boundaries for errors that should be handled explicitly such as form validation, expected API errors, and user input errors
* Handle TanStack Query mutation errors using onError callbacks to display contextual error messages
* Only add a page-level error boundary when you need custom error UI for a specific route that differs from the default error page
* Only add component-level error boundaries for isolated critical features where partial failure is acceptable, such as independent dashboard widgets that can fail without affecting the rest of the page. Use this mainly when using components we do not manage internally (eg: CodeMirror).
* Prevent double submissions by checking mutation pending state before triggering operations
* Use typed error guards such as isPackmindError to safely extract error details from API responses before displaying to users
* Wrap async operations in try-catch blocks since error boundaries do NOT catch errors in event handlers or async code

Full standard is available here for further request: [Frontend Error Management](.packmind/standards/frontend-error-management.md)

## Standard: Frontend Navigation with React Router

Standardize frontend navigation using React Router v7 with centralized utilities in React applications to ensure consistent URL parameter handling and simplify navigation management, particularly when organizing and scoping URLs, across apps/frontend/**/*.tsx. :
* Omit orgSlug and spaceSlug parameters to use current organization and space context by default and only specify them explicitly when navigating to a different organization or space.
* Use authentication route methods (routes.auth.*) for authentication-related navigation.
* Use organization-scoped route methods (routes.org.*) for pages that require only organization context.
* Use space-scoped route methods (routes.space.*) for pages that require both organization and space context.
* Use the routes utility from shared/utils/routes for all declarative navigation with Link and NavLink components.
* Use the useNavigation() hook from shared/hooks/useNavigation for all programmatic navigation with navigate().

Full standard is available here for further request: [Frontend Navigation with React Router](.packmind/standards/frontend-navigation-with-react-router.md)

## Standard: Frontend Routing and Bundling

Configure frontend routing and bundling to ensure React Router v7 routes are correctly grouped and bundled via Vite's rollupOptions.output.manualChunks in apps/frontend/vite.config.ts using id.includes() path matching to emit named chunks (routes-public-auth, routes-org-analytics, routes-org-settings, routes-org-artifacts) for public auth, org analytics/deployments/account settings, org settings, and artifacts to optimize code splitting, minimize bundle sizes, and improve loading performance in TypeScript React applications. :
* Configure manual chunks in Vite's rollupOptions.output.manualChunks to group related routes into shared bundles for optimal code splitting
* Group organization analytics, deployments, and account settings routes into a routes-org-analytics chunk
* Group organization artifacts (dashboard, recipes, and standards routes) into a routes-org-artifacts chunk
* Group organization settings routes (app/routes/org.$orgSlug._protected.settings) into a routes-org-settings chunk
* Group public authentication routes (app/routes/_public) into a routes-public-auth chunk
* Use path matching with id.includes() to identify route files for chunk grouping in the manual chunks function

Full standard is available here for further request: [Frontend Routing and Bundling](.packmind/standards/frontend-routing-and-bundling.md)

## Standard: Jest Test Suite Organization and Patterns

Establish Jest test suite organization and patterns governing test file structure, describe/it hierarchy, typed mocking using jest.Mocked<ServiceType> and createMockInstance, factory-based test data and @packmind/types createUserId/createOrganizationId/createStandardId helpers, assertion conventions (single primary assertion, .not.toHaveBeenCalled()), test ordering (happy path, error cases, edge cases, complex scenarios), and validation/error-handling patterns for TypeScript/Node.js monorepo code (including Express or frontend React/Vue components where applicable) and toolchains (ESLint, Prettier, Webpack/Vite) with CI/infrastructure considerations (Docker, Kubernetes, AWS) to ensure reliable, maintainable, and debuggable unit and integration tests when writing or refactoring test suites with Jest. :
* Define reusable test data at the describe block level before test cases when the data is shared across multiple tests
* Group related complex scenarios in dedicated describe blocks (e.g., 'rate limiting', 'multiple organizations') with multiple test cases covering different aspects
* Order tests within each describe block: happy path first, then error cases, then edge cases (null/undefined/empty/whitespace), then complex scenarios
* Organize describe blocks using 'with...' prefix for input/state conditions and 'when...' prefix for action-based scenarios
* Test all validation edge cases systematically in separate describe blocks: empty string, whitespace-only, null, undefined, and minimal valid input
* Use .not.toHaveBeenCalled() to verify services were not invoked in error or validation failure scenarios
* Use `createXXXId` functions from @packmind/types (createUserId, createOrganizationId, createStandardId, createRecipeId) for creating typed IDs in test data
* Use createMockInstance to create mock instances
* Use typed mocks with 'jest.Mocked<ServiceType>' and initialize them in beforeEach using the pattern '{ methodName: jest.fn() } as unknown as jest.Mocked<ServiceType>'

Full standard is available here for further request: [Jest Test Suite Organization and Patterns](.packmind/standards/jest-test-suite-organization-and-patterns.md)

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
