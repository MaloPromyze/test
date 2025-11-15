Create a JWT authentication middleware to secure API endpoints by validating tokens and extracting user information from requests, ensuring only authenticated users can access protected routes.

## When to Use

- When implementing authentication for REST API endpoints
- When you need to protect routes from unauthorized access
- When integrating JWT tokens in Express.js or similar frameworks

## Context Validation Checkpoints

* [ ] Is the JWT secret key configured in environment variables?
* [ ] What is the expected token format and expiration time?
* [ ] Which routes need to be protected?
* [ ] What user information should be extracted from the token?

## Recipe Steps

### Step 1: Install Dependencies

Install the required JWT library (e.g., jsonwebtoken) and type definitions if using TypeScript.

```bash
npm install jsonwebtoken
npm install --save-dev @types/jsonwebtoken
```

### Step 2: Create Middleware Function

Create a middleware function that extracts the token from the Authorization header, verifies it using the secret key, and attaches user information to the request object.

```typescript
import { Request, Response, NextFunction } from 'express';
import jwt from 'jsonwebtoken';

interface AuthRequest extends Request {
  user?: { id: string; email: string };
}

export const authenticateToken = (
  req: AuthRequest,
  res: Response,
  next: NextFunction
) => {
  const authHeader = req.headers['authorization'];
  const token = authHeader && authHeader.split(' ')[1];

  if (!token) {
    return res.status(401).json({ error: 'Access token required' });
  }

  jwt.verify(token, process.env.JWT_SECRET!, (err, decoded) => {
    if (err) {
      return res.status(403).json({ error: 'Invalid or expired token' });
    }
    req.user = decoded as { id: string; email: string };
    next();
  });
};
```

### Step 3: Apply Middleware to Routes

Apply the authentication middleware to protected routes by adding it as a parameter in the route definition.

```typescript
import { authenticateToken } from './middleware/auth';

router.get('/protected', authenticateToken, (req, res) => {
  res.json({ message: 'Protected data', user: req.user });
});
```
