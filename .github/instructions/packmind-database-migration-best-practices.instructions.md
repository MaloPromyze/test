---
applyTo: '**'
---
## Standard: Database Migration Best Practices

Write safe and reversible database migrations to maintain data integrity and enable rollback capabilities :
* Always write both up and down migration methods to enable rollback
* Never modify existing migration files after they have been deployed to production
* Use transactions for multi-step migrations to ensure atomicity

Full standard is available here for further request: [Database Migration Best Practices](../../.packmind/standards/database-migration-best-practices.md)