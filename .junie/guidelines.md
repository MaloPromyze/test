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
* aiAgent: "Junie"
* gitRepo: "repository"
* target: "/"

**Remember: Always check the recipes list first, but only use recipes that actually apply to your specific task.**`

## Available recipes

* [Apple Recipe](../.packmind/recipes/apple-recipe.md): Recipe for testing sorting.
* [Implementing Feature Flags](../.packmind/recipes/implementing-feature-flags.md): Implement feature flags to enable safe deployment of new features, A/B testing, and gradual rollouts while maintaining code stability and allowing instant rollback capabilities.
* [Mango Recipe](../.packmind/recipes/mango-recipe.md): Recipe for testing sorting.
* [Zebra Recipe](../.packmind/recipes/zebra-recipe.md): Recipe for testing sorting.
<!-- end: Packmind recipes -->
<!-- start: Packmind standards -->
# Packmind Standards

Before starting your work, make sure to review the coding standards relevant to your current task.

Always consult the sections that apply to the technology, framework, or type of contribution you are working on.

All rules and guidelines defined in these standards are mandatory and must be followed consistently.

Failure to follow these standards may lead to inconsistencies, errors, or rework. Treat them as the source of truth for how code should be written, structured, and maintained.

## Standard: API Response Consistency API Response Consistency API Response Consistency API Response ConsistencyAPI Response Consistency API Response Consistency

This standard defines how API responses should be structured across the application. Consistent response formats make it easier for clients to handle responses, improve error handling, and reduce inte... :
* Always return responses with a consistent envelope structure containing data, metadata, and error fields
* Include pagination metadata in list responses with total count, page size, and current page information
* Return meaningful error messages with error codes, human-readable descriptions, and optional field-level errors for validation failures
* Use consistent HTTP status codes where 2xx indicates success, 4xx indicates client errors, and 5xx indicates server errors

Full standard is available here for further request: [API Response Consistency API Response Consistency API Response Consistency API Response ConsistencyAPI Response Consistency API Response Consistency](../.packmind/standards/api-response-consistency.md)

## Standard: Mango Best Practices

Use mangos for testing. :
* Always use mangos

Full standard is available here for further request: [Mango Best Practices](../.packmind/standards/mango-best-practices.md)

## Standard: Zebra Pattern

Use zebra patterns for testing. :
* Always use zebras

Full standard is available here for further request: [Zebra Pattern](../.packmind/standards/zebra-pattern.md)
<!-- end: Packmind standards -->
