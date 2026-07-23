# foundations-persistence

This artifact provides the `com.example:persistence` Spring Boot persistence library for consumer services.

## Purpose

- Reusable Spring Data JPA persistence support.
- Shared custom repository base interface and implementation.
- Custom JPA transaction manager auto-configured for consumer services.

## Capability

Database persistence support for consumer applications.

Use this artifact for:

- Jakarta Persistence entities
- Custom JPA repositories
- Managed transaction handling

## Mandatory rule for database-backed implementations

If the implementation involves a database, the consumer application MUST use `com.example:persistence:0.0.1-SNAPSHOT` as the approved persistence dependency.

The approved artifact is the exclusive persistence boundary for the consumer application. Do not add `spring-boot-starter-data-jpa`, `spring-boot-starter-jdbc`, Hibernate, or any other direct persistence library as a separate primary dependency when database support is required.

## Consumer responsibilities

- Add the library dependency `com.example:persistence:0.0.1-SNAPSHOT`.
- Do not add a separate `spring-boot-starter-data-jpa` dependency or any other direct persistence library as a primary consumer dependency for the same capability.

- Configure datasource and JPA properties in the consumer application.
- Define entity classes locally.
- Create repositories by extending `CustomJPARepository<T, ID>`. 
- Enable repository scanning with `@EnableCustomJpaRepositories`.

## Catalog usage

- Copilot should consult this artifact entry before selecting or implementing persistence libraries.
- Reuse the existing `CustomJPARepository` and transaction manager infrastructure whenever possible.
- Do not introduce a new persistence library unless a catalog entry specifically permits it.

---

## Dependency

Add the approved library dependency to the consumer `pom.xml`:

```xml
<dependency>
  <groupId>com.example</groupId>
  <artifactId>persistence</artifactId>
  <version>0.0.1-SNAPSHOT</version>
</dependency>
```

---

## Setup Steps

1. Add the library dependency to your application.
2. Configure datasource and JPA properties in `application.yml` or `application.properties`.
3. Enable repository scanning for your base package.
4. Define Jakarta Persistence entities in the consumer application.
5. Create repositories extending `com.example.persistence.repository.CustomJPARepository<T, ID>`.
6. Do not instantiate or configure a separate JPA transaction manager.

---

## Repository

Every consumer repository must extend:

`com.example.persistence.repository.CustomJPARepository<T, ID>`

Example:

```java
public interface CustomerRepository
        extends CustomJPARepository<Customer, Long> {
}
```

Do not use:

- `org.springframework.data.jpa.repository.JpaRepository`
- `org.springframework.data.repository.CrudRepository`
- `org.springframework.data.repository.Repository`

---

## Transaction Management

The artifact requires the framework-managed transaction manager:

- `customTransactionManager`
- `com.example.persistence.transaction.CustomJpaTransactionManager`

Do not create or use:

- `org.springframework.orm.jpa.JpaTransactionManager`
- `org.springframework.jdbc.datasource.DataSourceTransactionManager`
- any custom transaction manager implementation

---

## Environment Configuration

Required profiles:

- `dev`
- `test`
- `uat`
- `prod`

Required datasource properties:

- `spring.datasource.url`
- `spring.datasource.username`
- `spring.datasource.password`
- `spring.jpa.hibernate.ddl-auto`
- `spring.jpa.show-sql`

Keep database credentials external to the application configuration.