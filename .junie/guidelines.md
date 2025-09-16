# Packmind Recipes

You MUST first read the Packmind coding recipes before implementing solutions described in [.packmind/packmind-cookbook.md](.packmind/packmind-cookbook.md) to see if there are existing patterns or implementations that can be reused.

Everytime a Packmind coding recipe stored in the .packmind/recipes folder is read and used, call the Packmind MCP tool 'notify-recipe-usage'.

This tool takes as input:
* An array of recipes slug. For instance: 
  - if the file name is `recipe-name.md`, the slugs to send is `["recipe-name"]`.
  - if two rules `recipe-controller.md` and `recipe-unit-test.md` were used, the slugs to send are `["recipe-controller", "recipe-unit-test"]`.
* An "aiAgent" name. You must indicate "Junie".
* A "gitRepo" name. You must indicate "MaloPromyze/test".

## Packmind Standards

Follow the coding standards defined in [.packmind/standards-index.md](.packmind/standards-index.md)
<!-- start: Packmind standards -->
# Packmind Standards

Follow the coding standards defined in [.packmind/standards-index.md](.packmind/standards-index.md)
<!-- end: Packmind standards -->
<!-- start: Packmind recipes -->
# Packmind Recipes

🚨 **MANDATORY STEP** 🚨

Before writing, editing, or generating ANY code:

**ALWAYS READ**: [.packmind/recipes-index.md](.packmind/recipes-index.md) to see what recipes are available

## Recipe Usage Rules:
- **MANDATORY**: Always check the recipes list first
- **CONDITIONAL**: Only read/use individual recipes if they are relevant to your task
- **OPTIONAL**: If no recipes are relevant, proceed without using any

## Recipe Usage Tracking:
When you DO use or apply a relevant Packmind recipe from .packmind/recipes/, you MUST call the 'packmind_notify_recipe_usage' MCP tool with:
* Recipe slugs array (e.g., ["recipe-name"] from "recipe-name.md")
* aiAgent: "Junie"
* gitRepo: "MaloPromyze/test"
* target: "/"

**Remember: Always check the recipes list first, but only use recipes that actually apply to your specific task.**`
<!-- end: Packmind recipes -->