
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
* aiAgent: "Gitlab Duo"
* gitRepo: "repository"
* target: "/"

**Remember: Always check the recipes list first, but only use recipes that actually apply to your specific task.**`

## Available recipes

* [Create React Form with Validation](../../.packmind/recipes/create-react-form-with-validation.md): Build a React form component with client-side validation and error handling using modern React patterns
* [Implement Authentication Middleware](../../.packmind/recipes/implement-authentication-middleware.md): Create authentication middleware to protect API routes and validate user sessions
<!-- end: Packmind recipes -->
<!-- start: Packmind standards -->
# Packmind Standards

Before starting your work, make sure to review the coding standards relevant to your current task.

Always consult the sections that apply to the technology, framework, or type of contribution you are working on.

All rules and guidelines defined in these standards are mandatory and must be followed consistently.

Failure to follow these standards may lead to inconsistencies, errors, or rework. Treat them as the source of truth for how code should be written, structured, and maintained.

## Standard: API Response Formatting

Standardize API response formats for consistent client-side handling and better developer experience :
* Always return responses in a consistent structure with data, error, and metadata fields
* Include pagination metadata for list endpoints using a standard pagination structure
* Use appropriate HTTP status codes and include error details in the response body

Full standard is available here for further request: [API Response Formatting](../../.packmind/standards/api-response-formatting.md)

## Standard: Database Migration Best Practices

This standard defines guidelines for creating database migrations that are safe, reversible, and maintainable. It covers migration naming conventions, data transformation strategies, and rollback proc... :
* Always write both up and down migration methods to enable rollback
* Never modify existing migration files after they have been deployed to production v2
* Use transactions for multi-step migrations to ensure atomicity

Full standard is available here for further request: [Database Migration Best Practices](../../.packmind/standards/database-migration-best-practices.md)

## Standard: TypeScript Async Error Handling

Handle asynchronous operations with proper error handling and type safety in TypeScript applications :
* Always use async/await instead of .then() chains for better readability and error handling
* Use typed error classes instead of generic Error instances for better error handling
* Wrap async operations in try-catch blocks to handle errors gracefully

Full standard is available here for further request: [TypeScript Async Error Handling](../../.packmind/standards/typescript-async-error-handling.md)
<!-- end: Packmind standards -->