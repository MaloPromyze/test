Implement a GraphQL resolver using DataLoader to batch and cache database queries, reducing N+1 query problems and improving API performance significantly.

## When to Use

- When implementing GraphQL resolvers that fetch related data
- When experiencing N+1 query performance issues
- When you need to batch multiple database queries efficiently

## Context Validation Checkpoints

* [ ] What entities need to be loaded in batches?
* [ ] What is the primary key used for batching?
* [ ] Should the DataLoader cache be per-request or shared?
* [ ] Are there any specific caching requirements?

## Recipe Steps

### Step 1: Install DataLoader

Install the DataLoader package which provides batching and caching functionality for GraphQL resolvers.

```bash
npm install dataloader
npm install --save-dev @types/dataloader
```

### Step 2: Create DataLoader Factory

Create a factory function that generates a new DataLoader instance for each request, ensuring proper batching and caching per request context.

```typescript
import DataLoader from 'dataloader';
import { User } from './models/User';

const createUserLoader = () => {
  return new DataLoader<string, User>(async (userIds) => {
    const users = await User.findByIds(userIds);
    const userMap = new Map(users.map(user => [user.id, user]));
    return userIds.map(id => userMap.get(id) || null);
  });
};
```

### Step 3: Add to Context

Add the DataLoader instances to the GraphQL context so they are available in all resolvers and properly scoped per request.

```typescript
const context = {
  userLoader: createUserLoader(),
  postLoader: createPostLoader(),
};
```

### Step 4: Use in Resolver

Use the DataLoader in your resolver to load related data, which will automatically batch multiple requests into a single database query.

```typescript
const postResolver = {
  author: async (post, args, context) => {
    return context.userLoader.load(post.authorId);
  },
};
```
