# TypeScript Async Error Handling

This standard defines best practices for handling asynchronous operations in TypeScript, ensuring proper error handling, type safety, and maintainability. It covers async/await patterns, Promise handling, and error propagation strategies.

## Rules

* Always use async/await instead of .then() chains for better readability and error handling
* Wrap async operations in try-catch blocks to handle errors gracefully
* Use typed error classes instead of generic Error instances for better error handling
