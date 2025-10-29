A test recipe to verify that space support is working correctly in the MCP server

## When to Use

- When testing space support functionality
- When verifying recipe creation works with spaces
- When debugging MCP server integration

## Context Validation Checkpoints

* [ ] Ensure the MCP server is running
* [ ] Verify that spaces exist in the organization
* [ ] Check that the recipe is created in the correct space

## Recipe Steps

### Step 1: Verify Space Support

Test that the recipe creation process correctly uses the first available space in the organization

```typescript
// The MCP server should automatically get the first space
const spaces = await spacesHexa.listSpacesByOrganization(organizationId);
const firstSpace = spaces[0];
```

### Step 2: Create Recipe

Create the recipe with the space ID

```typescript
const recipe = await recipesHexa.captureRecipe({
  name,
  spaceId: firstSpace.id,
  organizationId,
  userId
});
```

### Step 3: Verify Creation

Confirm the recipe was created successfully with space support

```typescript
// Recipe should now be associated with the space
console.log('Recipe created with space:', recipe.spaceId);
```
