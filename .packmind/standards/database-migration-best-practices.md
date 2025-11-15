# Database Migration Best Practices

This standard defines guidelines for creating database migrations that are safe, reversible, and maintainable. It covers migration naming conventions, data transformation strategies, and rollback procedures to ensure database schema changes can be applied and reverted reliably.

## Rules

* Always write both up and down migration methods to enable rollback
* Use transactions for multi-step migrations to ensure atomicity
* Never modify existing migration files after they have been deployed to production
