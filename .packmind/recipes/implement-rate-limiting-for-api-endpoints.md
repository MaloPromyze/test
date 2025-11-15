Add rate limiting to API endpoints to prevent abuse and ensure fair resource usage by restricting the number of requests a client can make within a specific time window.

## When to Use

- When protecting API endpoints from abuse or DDoS attacks
- When implementing fair usage policies for public APIs
- When you need to throttle requests from specific IP addresses or users

## Context Validation Checkpoints

* [ ] What is the maximum number of requests allowed per time window?
* [ ] What time window should be used (per minute, hour, day)?
* [ ] Should rate limits be applied globally or per endpoint?
* [ ] How should rate limit information be communicated to clients?

## Recipe Steps

### Step 1: Install Rate Limiting Library

Install express-rate-limit package for Express.js applications or equivalent for your framework.

```bash
npm install express-rate-limit
```

### Step 2: Configure Rate Limiter

Create a rate limiter configuration with appropriate window size and maximum request limits, optionally using Redis for distributed rate limiting.

```typescript
import rateLimit from 'express-rate-limit';

const limiter = rateLimit({
  windowMs: 15 * 60 * 1000, // 15 minutes
  max: 100, // limit each IP to 100 requests per windowMs
  message: 'Too many requests from this IP, please try again later.',
  standardHeaders: true,
  legacyHeaders: false,
});
```

### Step 3: Apply to Routes

Apply the rate limiter middleware to specific routes or globally to all routes depending on your requirements.

```typescript
import { limiter } from './middleware/rateLimit';

// Apply globally
app.use(limiter);

// Or apply to specific routes
app.use('/api/', limiter);
```

### Step 4: Handle Rate Limit Headers

Ensure rate limit information (remaining requests, reset time) is properly communicated through response headers for better client experience.

```typescript
// Headers are automatically added when standardHeaders: true
// X-RateLimit-Limit: 100
// X-RateLimit-Remaining: 99
// X-RateLimit-Reset: 1234567890
```
