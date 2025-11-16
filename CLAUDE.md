
<!-- start: Packmind standards -->
# Packmind Standards

Before starting your work, make sure to review the coding standards relevant to your current task.

Always consult the sections that apply to the technology, framework, or type of contribution you are working on.

All rules and guidelines defined in these standards are mandatory and must be followed consistently.

Failure to follow these standards may lead to inconsistencies, errors, or rework. Treat them as the source of truth for how code should be written, structured, and maintained.

## Standard: Database Migration Best Practices

This standard defines guidelines for creating database migrations that are safe, reversible, and maintainable. It covers migration naming conventions, data transformation strategies, and rollback proc... :
* Always write both up and down migration methods to enable rollback
* Never modify existing migration files after they have been deployed to production v2
* Use transactions for multi-step migrations to ensure atomicity

Full standard is available here for further request: [Database Migration Best Practices](.packmind/standards/database-migration-best-practices.md)
<!-- end: Packmind standards -->