Create a new MCP server tool endpoint that exposes Packmind domain functionality to AI agents, enabling seamless integration with Cursor, Claude, and other MCP-compatible tools when adding queryable features to the platform.

## When to Use

- When you need to expose an existing use case or service method to AI agents via MCP
- When adding a new list/query endpoint that mirrors existing patterns (e.g., list_standards)
- When creating CRUD operations for Packmind entities through the MCP protocol
- When enabling AI agents to interact with Packmind domain functionality

## Context Validation Checkpoints

* [ ] Confirm the target Hexa domain has the required use case/method already implemented
* [ ] Verify the user context requirements (does this need authentication?)
* [ ] Check if similar MCP tools exist that can serve as a template

## Recipe Steps

### Step 1: Identify the Target Hexa Method

Locate the domain Hexa class (e.g., RecipesHexa, StandardsHexa) and find the method to expose. Verify the method signature and return type to ensure it matches the expected MCP tool interface.

```typescript
// Example from RecipesHexa
public async listRecipesByOrganization(
  organizationId: OrganizationId
): Promise<Recipe[]>
```

### Step 2: Define the MCP Tool Schema

Create the tool definition using mcpServer.tool() with name, description, and Zod schema for parameters. Follow naming convention: ${mcpToolPrefix}_<action>_<entity>

```typescript
mcpServer.tool(
  `${mcpToolPrefix}_list_recipes`,
  'Get a list of current recipes in Packmind',
  {}, // Zod schema for params
  async () => { /* handler */ }
)
```

### Step 3: Implement User Context Validation

Add user context check if the operation requires authentication. Return appropriate error message if context is missing to prevent unauthorized access.

```typescript
if (!userContext) {
  throw new Error('User context is required to list recipes');
}
```

### Step 4: Call the Hexa Method

Invoke the domain Hexa method with appropriate parameters. Handle organizationId/userId extraction from userContext using the branded type factory functions.

```typescript
const recipes = await recipesHexa.listRecipesByOrganization(
  createOrganizationId(userContext.organizationId)
);
```

### Step 5: Format the Response

Transform domain entities into MCP-compatible response format. Handle empty results with friendly messages. Apply sorting, filtering, or pagination as needed (typically limit to 20 items).

```typescript
const sortedRecipes = recipes
  .sort((a, b) => a.slug.localeCompare(b.slug))
  .slice(0, 20);
const formattedList = sortedRecipes
  .map((recipe) => `• ${recipe.slug}: ${recipe.name}`)
  .join('\n');
return {
  content: [{ type: 'text', text: formattedList }]
};
```

### Step 6: Add Error Handling

Wrap the logic in try-catch block. Return descriptive error messages in MCP response format to help users debug issues.

```typescript
try {
  // ... tool logic
} catch (error) {
  return {
    content: [{
      type: 'text',
      text: `Failed to list recipes: ${error instanceof Error ? error.message : String(error)}`
    }]
  };
}
```

### Step 7: Test the Tool

Connect to the local MCP server and call the new tool directly to verify functionality. Check both success and error cases to ensure robust behavior.

```typescript
// Test the tool via MCP
mcp_packmind_packmind_list_recipes()
```

### Step 8: Run Quality Gate and Commit

Execute npm run quality-gate to ensure all checks pass (lint, test, packmind-cli). Stage only the relevant files and commit with descriptive gitmoji message following project conventions.

```bash
npm run quality-gate
git add apps/mcp-server/src/app/mcp-server.ts
git commit -m "✨ Add MCP tool to list recipes"
```
