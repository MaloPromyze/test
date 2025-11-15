---
applyTo: '**'
---
## Standard: Database Migration Best Practices

This standard defines guidelines for creating database migrations that are safe, reversible, and maintainable. It covers migration naming conventions, data transformation strategies, and rollback proc... :
* Always write both up and down migration methods to enable rollback
* Never modify existing migration files after they have been deployed to production v2
* Use transactions for multi-step migrations to ensure atomicity

Full standard is available here for further request: [Database Migration Best Practices](../../.packmind/standards/database-migration-best-practices.md)