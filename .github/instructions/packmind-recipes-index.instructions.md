---
applyTo: '**'
---

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
* aiAgent: "GitHub Copilot"
* gitRepo: "repository"
* target: "/"

**Remember: Always check the recipes list first, but only use recipes that actually apply to your specific task.**`

## Available recipes

- [Create New Package in Monorepo](.packmind/recipes/create-new-package-in-monorepo.md) : Create a new buildable TypeScript package in the Packmind monorepo using Nx tools to establish a shared library for code reuse across applications and packages when setting up common utilities or implementing domain-specific logic.
- [Create UseCase Test Class Template](.packmind/recipes/create-usecase-test-class-template.md) : Create a comprehensive test class for UseCases to ensure consistent testing patterns and thorough coverage of various execution scenarios in the Packmind monorepo.
- [Creating a new test factory](.packmind/recipes/creating-a-new-test-factory.md) : Create a test factory for each entity to generate consistent and randomized test data, ensuring reliable testing and validation of your models.
- [Cross-Domain Integration with Port/Adapter Pattern](.packmind/recipes/cross-domain-integration-with-portadapter-pattern.md) : Integrate a consumer domain with a provider domain using lazy dependency injection through the Port/Adapter pattern to enable cross-domain operations while avoiding circular dependencies and maintaining loose coupling.
- [How to Write TypeORM Migrations in Packmind](.packmind/recipes/how-to-write-typeorm-migrations-in-packmind.md) : Write TypeORM migrations in the Packmind monorepo to manage and version database schema changes with consistent logging, reversible rollbacks, and shared helpers so you can safely create or modify tables, columns, and foreign-key relationships whenever schema changes need to be tracked and reversible.
- [Refactor Use Case to Follow IUseCase Pattern](.packmind/recipes/refactor-use-case-to-follow-iusecase-pattern.md) : Refactor existing use cases to implement the IUseCase pattern for consistent command/response typing and enhanced business rule enforcement, ensuring maintainability and clarity across your application's architecture.
- [Wrapping Chakra UI with Slot Components](.packmind/recipes/wrapping-chakra-ui-with-slot-components.md) : Create slot components to wrap Chakra UI primitives for enhanced custom composition and API consistency in your design system.