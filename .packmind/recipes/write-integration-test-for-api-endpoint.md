Create comprehensive integration tests for API endpoints that verify request handling, database interactions, and response formatting

## When to Use

- When testing API endpoints that interact with databases
- When verifying complete request-response cycles
- When ensuring proper error handling and edge cases in API routes

## Context Validation Checkpoints

* [ ] Which endpoint needs to be tested?
* [ ] What are the success and failure scenarios?
* [ ] What test data setup is required?
* [ ] Should the test use a real database or mocks?

## Recipe Steps

### Step 1: Set Up Test Environment

Configure test database, test server, and test utilities before running integration tests.

```typescript
beforeAll(async () => {
  testDataSource = await createTestDataSource();
  await testDataSource.initialize();
});

afterAll(async () => {
  await testDataSource.destroy();
});
```

### Step 2: Create Test Data

Set up necessary test data using factories or fixtures before each test, ensuring clean state.

```typescript
beforeEach(async () => {
  await testDataSource.query('TRUNCATE TABLE users CASCADE');
  testUser = await createTestUser({ email: 'test@example.com' });
});
```

### Step 3: Write Test Cases

Implement test cases that make actual HTTP requests to the endpoint and assert on responses and database state.

```typescript
it('returns user data when authenticated', async () => {
  const response = await request(app)
    .get(`/api/users/${testUser.id}`)
    .set('Authorization', `Bearer ${testToken}`)
    .expect(200);
  
  expect(response.body.data.email).toBe('test@example.com');
});
```

### Step 4: Test Error Scenarios

Verify error handling by testing invalid inputs, unauthorized access, and edge cases.

```typescript
it('returns 401 when token is invalid', async () => {
  await request(app)
    .get('/api/users/123')
    .set('Authorization', 'Bearer invalid-token')
    .expect(401);
});
```
