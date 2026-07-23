# Foundations Persistence

## Capability

Database persistence.

Use this artifact for:

- JPA entities
- Database repositories
- Database transactions

---

## Dependency

Use:

com.myorg.foundation:foundations-persistence

---

## Repository

Every application repository must extend:

JpaFoundationRepository

Example:

public interface CustomerRepository
        extends JpaFoundationRepository<Customer, Long> {
}

Do not use:

- JpaRepository
- CrudRepository
- Repository

---

## Transaction Management

Use:

foundationTransactionManager

Do not create:

- JpaTransactionManager
- DataSourceTransactionManager
- Custom transaction managers

---

## Environment Configuration

Support:

- dev
- test
- uat
- prod

Database credentials must come from environment variables or approved
secret management.