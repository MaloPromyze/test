Create authentication middleware to protect API routes and validate user sessions

## When to Use

- When securing API endpoints that require user authentication
- When implementing session-based or token-based authentication
- When adding authorization checks to existing routes

## Context Validation Checkpoints

* [ ] What authentication mechanism is being used (JWT, session cookies, API keys)?
* [ ] Which routes need to be protected?
* [ ] What user information needs to be available in the request context?
* [ ] How should authentication failures be handled?

## Recipe Steps

### Step 1: Create Authentication Middleware Function

Implement a middleware function that extracts and validates authentication tokens or session data from incoming requests.

```typescript
async function authMiddleware(
  request: Request,
  next: NextFunction
): Promise<void> {
  const token = extractToken(request);
  if (!token) {
    throw new UnauthorizedError('Missing authentication token');
  }
  // Validation logic
}
```

### Step 2: Validate Token and Extract User

Verify the authentication token, decode user information, and attach it to the request context for downstream handlers.

```typescript
const payload = await verifyToken(token);
const user = await userRepository.findById(payload.userId);
if (!user) {
  throw new UnauthorizedError('Invalid user');
}
request.user = user;
```

### Step 3: Apply Middleware to Routes

Register the authentication middleware on protected routes using your framework's middleware system.

```typescript
router.use('/api/protected', authMiddleware);
router.get('/api/protected/users', getUserHandler);
```

### Step 4: Handle Authentication Errors

Implement error handling for authentication failures, returning appropriate HTTP status codes and error messages.

```typescript
catch (error) {
  if (error instanceof UnauthorizedError) {
    return Response.json(
      { error: { code: 'UNAUTHORIZED', message: error.message } },
      { status: 401 }
    );
  }
  throw error;
}
```
