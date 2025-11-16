---
applyTo: '**'
---
## Standard: React Component State Management

This standard establishes patterns for managing state in React components using hooks, ensuring predictable state updates, proper dependency management, and optimal re-rendering behavior. It covers us... :
* Always include all dependencies in useEffect dependency arrays to prevent stale closures
* bonus
* Use useMemo for expensive computations and useCallback for stable function references passed to child components
* Use useState for local component state and avoid storing derived values in state

Full standard is available here for further request: [React Component State Management](../../.packmind/standards/react-component-state-management.md)