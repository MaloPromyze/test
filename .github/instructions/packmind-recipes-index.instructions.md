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
- [Cross-Domain Integration with Port/Adapter Pattern](.packmind/recipes/cross-domain-integration-with-portadapter-pattern.md) : Integrate a consumer domain with a provider domain using lazy dependency injection through the Port/Adapter pattern to enable cross-domain operations while avoiding circular dependencies and maintaining loose coupling.
- [How to Write TypeORM Migrations in Packmind](.packmind/recipes/how-to-write-typeorm-migrations-in-packmind.md) : Write TypeORM migrations in the Packmind monorepo to manage database schema changes effectively while ensuring proper logging and rollback capabilities.