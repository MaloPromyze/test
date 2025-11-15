
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
* aiAgent: "AGENTS.md"
* gitRepo: "MaloPromyze/test"
* target: "/"

**Remember: Always check the recipes list first, but only use recipes that actually apply to your specific task.**`

## Available recipes

* [Create GraphQL Resolver with DataLoader](.packmind/recipes/create-graphql-resolver-with-dataloader.md): Implement a GraphQL resolver using DataLoader to batch and cache database queries, reducing N+1 query problems and improving API performance significantly.
* [Implement JWT Authentication Middleware](.packmind/recipes/implement-jwt-authentication-middleware.md): Create a JWT authentication middleware to secure API endpoints by validating tokens and extracting user information from requests, ensuring only authenticated users can access protected routes.
* [Implement Rate Limiting for API Endpoints](.packmind/recipes/implement-rate-limiting-for-api-endpoints.md): Add rate limiting to API endpoints to prevent abuse and ensure fair resource usage by restricting the number of requests a client can make within a specific time window.
* [Setup Docker Compose for Development Environment](.packmind/recipes/setup-docker-compose-for-development-environment.md): Configure Docker Compose to set up a complete development environment with database, cache, and application services, enabling consistent local development across team members.
<!-- end: Packmind recipes -->