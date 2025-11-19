# Packmind Standards Index

This standards index contains all available coding standards that can be used by AI agents (like Cursor, Claude Code, GitHub Copilot) to find and apply proven practices in coding tasks.

## Available Standards

- [Back-end repositories SQL queries using TypeORM](./standards/back-end-repositories-sql-queries-using-typeorm.md) : Implement SQL query guidelines using TypeORM's QueryBuilder in back-end repositories under /infra/repositories/*Repository.ts to enhance type safety, prevent SQL injection, and improve code maintainability when writing database queries, including lookups, joins, and handling soft-deleted entities.
- [Frontend Data Flow](./standards/frontend-data-flow.md) : Apply this standard when building frontend routes with React Router v7 and TanStack Query to ensure consistent data flow patterns and optimal user experience.
- [Port-Adapter Cross-Domain Integration](./standards/port-adapter-cross-domain-integration.md) : Apply the Port/Adapter pattern to enable cross-domain communication while preventing circular dependencies and maintaining loose coupling in the DDD monorepo.
- [TanStack Query Key Management](./standards/tanstack-query-key-management.md) : Manage TanStack Query key structures using hierarchical prefix matching and dedicated queryKeys.ts files in React applications to ensure efficient cache invalidation and type-safe query management when handling cross-domain data operations.
- [Use Case Architecture Patterns](./standards/use-case-architecture-patterns.md) : Structure use cases in the Packmind monorepo by following hexagonal architecture principles with command/response patterns, specific typing, and separation of concerns for authentication and authorization to ensure consistent, type-safe, and maintainable cross-domain integrations when creating or refactoring use cases.


---

*This standards index was automatically generated from deployed standard versions.*