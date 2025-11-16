
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

* [Set Up New Domain Package in Monorepo](../../.packmind/recipes/set-up-new-domain-package-in-monorepo.md): Create a new domain package following DDD architecture principles in the Packmind monorepo structure
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
<!-- end: Packmind standards -->