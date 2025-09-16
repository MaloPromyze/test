# How to Use Packmind Recipes

## Overview
Packmind recipes are reusable coding patterns and procedures that help developers implement consistent solutions across projects. This recipe explains how to discover, understand, and apply recipes effectively in your development workflow.

## When to Use This Recipe
- When you're new to Packmind and want to understand the recipe system
- When you need to find existing solutions for common coding problems
- When you want to ensure consistency across your codebase
- When onboarding team members to Packmind workflows

## Prerequisites
- Access to a Packmind-enabled repository
- Basic understanding of your project's technology stack
- Familiarity with your code editor (Cursor, VS Code, etc.)

## Step-by-Step Process

### 1. Discover Available Recipes
```bash
# Check what recipes are available in your project
ls .packmind/recipes/

# Or use the Packmind CLI to list recipes
npm run packmind-cli recipes list
```

**What to look for:**
- Recipe names that match your current task
- Recipes related to your technology stack
- Recently updated recipes (often the most relevant)

### 2. Read and Understand a Recipe
```markdown
# Recipe files are in markdown format
# Open any recipe file to see its structure:
# - Overview: What the recipe does
# - When to Use: Specific scenarios
# - Prerequisites: What you need before starting
# - Step-by-Step Process: Detailed instructions
# - Examples: Real code samples
# - Best Practices: Tips for success
```

**Key sections to focus on:**
- **Overview**: Quick understanding of the recipe's purpose
- **When to Use**: Confirms this recipe fits your needs
- **Prerequisites**: Ensures you're ready to apply it
- **Examples**: Shows real implementation

### 3. Apply a Recipe to Your Code

#### Option A: Manual Application
1. Read through the recipe completely
2. Adapt the examples to your specific use case
3. Follow the step-by-step process
4. Test your implementation

#### Option B: AI-Assisted Application
```prompt
# When using AI coding assistants (Cursor, GitHub Copilot, etc.)
"Apply the [Recipe Name] pattern to implement [your specific requirement]. 
Follow the Packmind recipe guidelines for [technology/framework]."
```

### 4. Verify Recipe Implementation
```bash
# Run your project's quality checks
npm run lint
npm run test
npm run build

# Use Packmind CLI to check standards compliance
npm run packmind-cli check
```

### 5. Document Your Implementation
```markdown
# Add comments referencing the recipe used
/**
 * Implementation following Packmind recipe: [Recipe Name]
 * See: .packmind/recipes/[recipe-file].md
 */
```

## Examples

### Example 1: Finding a Repository Pattern Recipe
```bash
# Look for repository-related recipes
ls .packmind/recipes/ | grep -i repository

# Typical output might show:
# repository-implementation-and-testing-pattern.md
```

### Example 2: Applying a Test Factory Recipe
```typescript
// Before: Manual test data creation
const user = {
  id: 'user-123',
  name: 'John Doe',
  email: 'john@example.com',
  organizationId: 'org-456'
};

// After: Using Test Factory pattern from recipe
const user = createUserFactory({
  name: 'John Doe',
  email: 'john@example.com'
}); // ID and organizationId auto-generated
```

### Example 3: Using AI with Recipe Context
```prompt
# Good prompt when working with Cursor or similar AI tools:
"I need to implement user authentication following the Packmind authentication recipe. 
Please help me create the login endpoint using the patterns shown in 
.packmind/recipes/authentication-pattern.md"
```

## Best Practices

### 1. Always Read First
- Don't jump straight to copying code
- Understand the "why" behind the recipe
- Check if the recipe fits your specific context

### 2. Adapt, Don't Copy Blindly
- Recipes are templates, not exact solutions
- Adapt variable names to match your domain
- Adjust patterns to fit your specific requirements

### 3. Stay Updated
```bash
# Regularly check for recipe updates
git pull origin main
# Check if new recipes have been added
ls -la .packmind/recipes/
```

### 4. Combine Recipes When Appropriate
- Many recipes work well together
- Example: Use "Repository Pattern" + "Test Factory" + "TypeORM Migration"
- Follow the dependency order suggested in recipes

### 5. Provide Feedback
- If a recipe doesn't work as expected, document the issue
- Suggest improvements based on your experience
- Share successful adaptations with your team

## Common Pitfalls to Avoid

### ❌ Don't Do This
```typescript
// Copying recipe code without understanding context
// This might not work in your specific setup
const genericRepository = new GenericRepository(); // From recipe example
```

### ✅ Do This Instead
```typescript
// Adapting recipe pattern to your domain
const userRepository = new UserRepository(
  dataSource,
  UserSchema,
  logger
); // Adapted from repository recipe
```

### Other Pitfalls:
- **Ignoring Prerequisites**: Skipping required setup steps
- **Version Mismatches**: Using old recipes with new frameworks
- **Over-Engineering**: Applying complex recipes to simple problems
- **Under-Engineering**: Not using recipes when they would help

## Troubleshooting

### Recipe Doesn't Seem to Apply
1. Check the "When to Use" section - might not be the right recipe
2. Verify prerequisites are met
3. Look for similar recipes that might be more appropriate

### Implementation Fails
1. Double-check you followed all steps
2. Ensure dependencies are correctly installed
3. Check if your project structure matches recipe assumptions
4. Review examples more carefully

### Code Doesn't Pass Quality Checks
1. Run `npm run packmind-cli check` for specific guidance
2. Compare your implementation with recipe examples
3. Check if you need to combine with other recipes (e.g., testing recipes)

## Advanced Usage

### Creating Recipe Combinations
```markdown
# Document when you successfully combine recipes
/**
 * This component uses:
 * - Component Architecture Recipe (structure)
 * - Error Handling Recipe (error boundaries)
 * - Testing Recipe (test setup)
 */
```

### Recipe-Driven Development
1. **Start with Recipes**: Look for applicable recipes before coding
2. **Recipe First**: Choose your recipes, then implement
3. **Validate with Recipes**: Use recipes as a checklist for code review

## Related Recipes
- Creating a New Test Factory
- Repository Implementation and Testing Pattern
- TypeORM Migration Guidelines
- Component Architecture Patterns

## Conclusion
Recipes are most effective when you understand their purpose and adapt them thoughtfully to your specific needs. They provide proven patterns while allowing flexibility for your unique requirements.

Remember: Recipes are guides, not rigid rules. Use them as a foundation to build consistent, maintainable code that follows your team's best practices.