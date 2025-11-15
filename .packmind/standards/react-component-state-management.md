# React Component State Management

This standard establishes patterns for managing state in React components using hooks, ensuring predictable state updates, proper dependency management, and optimal re-rendering behavior. It covers useState, useEffect, useMemo, and useCallback best practices.

## Rules

* Use useState for local component state and avoid storing derived values in state
* Always include all dependencies in useEffect dependency arrays to prevent stale closures
* Use useMemo for expensive computations and useCallback for stable function references passed to child components
