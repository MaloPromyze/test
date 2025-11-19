---
applyTo: '**'
---
## Standard: Frontend Data Flow

Apply this standard when building frontend routes with React Router v7 and TanStack Query to ensure consistent data flow patterns and optimal user experience. :
* Access data via query or mutation hooks in frontend route modules rather than calling gateways directly to maintain separation between data access and presentation layers
* Consume data in route module components using the useLoaderData() hook to access data returned by the clientLoader
* Define a crumb property in the handle export of route modules to enable automatic navigation breadcrumb generation
* Enable query options conditionally using the enabled property to prevent execution when required parameters are missing or invalid
* Export query hooks (e.g., useGetStandardByIdQuery) alongside query options to provide consistent component-level data access patterns
* Export query options as standalone functions (e.g., getStandardByIdOptions) separate from hooks to enable reuse in both hooks and route loaders
* Name route module default export functions with a suffix of RouteModule (e.g., StandardDetailRouteModule) to clearly identify route-level components
* Store domain queries in the domain folder organized by entity at apps/frontend/src/domains/{entity}/api/queries/ to maintain clear separation of concerns and domain boundaries
* Use clientLoader function (not loader) in route modules for data fetching when using React Router in SPA mode to ensure proper client-side data loading
* Use queryClient.ensureQueryData() or queryClient.fetchQuery() in clientLoader to preload data before rendering and leverage TanStack Query's caching mechanisms

Full standard is available here for further request: [Frontend Data Flow](../../.packmind/standards/frontend-data-flow.md)