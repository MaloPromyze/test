## Packmind Standards

Follow the coding standards defined in @.packmind/standards-index.md
<!-- start: Packmind standards -->
# Packmind Standards

Follow the coding standards defined in @.packmind/standards-index.md
<!-- end: Packmind standards -->
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

* [Add New MCP Tool to Packmind Server](.packmind/recipes/add-new-mcp-tool-to-packmind-server.md): Create a new MCP server tool endpoint that exposes Packmind domain functionality to AI agents, enabling seamless integration with Cursor, Claude, and other MCP-compatible tools when adding queryable features to the platform.
* [Creating a Hello World Test Component](.packmind/recipes/creating-a-hello-world-test-component.md): Create a simple Hello World component to verify the component creation workflow and test the basic React component structure, providing a quick validation that the development environment is properly configured.
* [Test Recipe with Space Support](.packmind/recipes/test-recipe-with-space-support.md): A test recipe to verify that space support is working correctly in the MCP server
<!-- end: Packmind recipes -->