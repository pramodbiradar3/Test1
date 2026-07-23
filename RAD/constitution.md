# Demo Project Constitution

## Core Principles

### I. Artifact-First Development
Before implementing or modifying code, the required capabilities of the requirement MUST be identified.

The approved artifact catalog MUST then be inspected to determine whether the organization already provides an artifact for any of those capabilities.

The default decision MUST be:

Approved Artifact Exists
        ↓
Use the Approved Artifact

A new library or custom implementation MUST NOT be introduced for a capability already provided by an approved organization artifact.

### II. Approved Artifacts Are the Capability Boundary

When an approved organization artifact provides a required capability, the artifact becomes the primary capability boundary for the consumer application.

The consumer application MUST use the approved artifact's public APIs, abstractions, extension points, and integration mechanisms.

The consumer application MUST NOT bypass the approved artifact and directly implement or configure the underlying technology when doing so violates the artifact contract.

The intended dependency direction is:

Consumer Application
        ↓
Approved Organization Artifact
        ↓
Underlying Frameworks / Libraries / Infrastructure

The consumer application MUST NOT bypass the approved artifact:

Consumer Application
        ├── Approved Organization Artifact
        └── Underlying Library ❌

unless the artifact contract explicitly permits that direct dependency.

### III. Contract Compliance
Any approved artifact used in implementation must be used according to its contract, including required dependencies, repository patterns, transaction handling, configuration, and usage restrictions.

Every approved artifact MUST be used according to its artifact contract.

The artifact contract is the authoritative source for determining how the artifact MUST be integrated and used.

The implementation MUST comply with all applicable contract requirements, including:

- Required dependencies
- Prohibited dependencies
- Dependency restrictions
- Required configuration
- APIs
- Interfaces
- Base classes
- Annotations
- Repository patterns
- Transaction management
- Integration patterns
- Extension points
- Usage constraints
- Prohibited usage patterns

The artifact contract MUST NOT be bypassed, overridden, or silently violated.

### IV. Strict Reuse Over Reinvention
If an approved artifact provides a required capability, the implementation MUST reuse that artifact.

The implementation MUST NOT:

Introduce an alternative library for the same capability.
Introduce a duplicate dependency for the same capability.
Reimplement functionality already provided by the artifact.
Create a parallel abstraction that duplicates the artifact.
Replace the artifact with a different technology based on personal preference.
Bypass the artifact's APIs, interfaces, base classes, or extension points.

### V. Explicit Fallback Only
A new external dependency or custom implementation MAY be introduced only when no applicable approved organization artifact exists for the required capability.

Before introducing a fallback:

The required capability MUST be identified.
The approved artifact catalog MUST be inspected.
The absence of an applicable approved artifact MUST be established.
The proposed dependency or implementation MUST be documented.
The reason for the fallback MUST be documented.

A fallback MUST NOT be introduced silently.

The fallback decision MUST be visible in the implementation plan or equivalent implementation documentation and the reason for the fallback must be documented.

### VI. Testability and Validation
All changes must remain testable through the existing project build and test workflow, and implementation decisions must be verifiable.

### VII.Authoritative Artifact Sources

The approved artifact catalog is located at:

.foundation/catalog.yaml

Artifact-specific information is located under:

.foundation/artifacts/

For every resolved artifact, the following sources MUST be reviewed where available:

Artifact Catalog
        ↓
Artifact Contract
        ↓
Artifact README / Integration Documentation
        ↓
Implementation

The sources have the following responsibilities:

## Artifact Catalog

The catalog is the source of truth for determining:

- Which artifacts are approved.
- Which capabilities an artifact provides.
- Which artifact should be considered for a capability.
- Artifact Contract

## The contract is the source of truth for:

- How the artifact MUST be used.
- Required dependencies.
- Prohibited dependencies.
- Required APIs.
- Required configuration.
- Required integration patterns.
- Usage restrictions.

## Artifact README / Integration Documentation

The artifact README or integration documentation is the source of truth for practical integration steps, including where applicable:

Installation instructions.
Dependency setup.
Configuration steps.
Initialization steps.
Usage examples.
Integration requirements.

The README MUST NOT override the artifact contract.

If the README and contract appear to conflict, the conflict MUST be identified and resolved before implementation proceeds.

## Additional Constraints

- The approved artifact catalog is the source of truth for identifying approved organization-provided artifacts.
- The artifact catalog and related contracts under .foundation/artifacts/ must be reviewed before implementation begins.
- Implementations must not bypass approved artifact APIs, interfaces, base classes, or extension points.
- Database persistence, authentication, messaging, logging, auditing, notifications, caching, observability, and any other capability covered by the catalog must use the approved artifact where one exists.

## Development Workflow

All implementation work must complete the following checks before coding begins:

1. Review the requirement and identify the required capabilities.
2. Inspect .foundation/artifacts/catalog.yaml.
3. Resolve every applicable approved artifact from the catalog.
4. Read the corresponding artifact contract(s).
5. Create or update the implementation plan using the approved artifacts.
6. Implement only using the approved artifacts unless no artifact exists for the required capability.

## Governance

This constitution supersedes ad-hoc implementation choices. Any implementation that introduces an alternative dependency or custom implementation for a capability covered by an approved artifact is non-compliant and must be corrected.

**Version**: 1.0.0 | **Ratified**: 2026-07-23 | **Last Amended**: 2026-07-23

### VI.Mandatory Rule

Before implementing or modifying any code, you MUST identify the required capabilities and resolve all applicable approved organization artifacts.

You MUST NOT start implementation until the artifact resolution process is complete.

### VII.Artifact Locations

The approved artifact catalog is located at:

.foundation/artifacts/catalog.yaml

Artifact contracts are located under:

.foundation/artifacts/

The catalog is the source of truth for identifying approved organization artifacts.

The artifact contract is the source of truth for determining how an artifact MUST be used.

### VIII.Mandatory Process

For every requirement, follow this exact sequence:

1. Understand the requirement
        ↓
2. Identify all required technical capabilities
        ↓
3. Read .foundation/artifacts/catalog.yaml
        ↓
4. Resolve an approved artifact for each capability
        ↓
5. Locate the corresponding artifact contract
        ↓
6. Read the complete artifact contract
        ↓
                ↓
6. Read the artifact README.md file for the steps to integrate
        ↓
8. Determine allowed and prohibited dependencies and APIs
        ↓
9. Create an implementation plan
        ↓
10. Validate the implementation plan against the contracts
        ↓
11. Implement using the approved artifacts
        ↓
12. Validate the final implementation

This process MUST be followed for every implementation task.


### IX.DO
Add the approved organization artifact.
Use the APIs and abstractions defined by its contract.
Use its required base classes and interfaces.
Use its prescribed configuration.

### X.DO NOT
Add the underlying framework dependency directly.
Add duplicate transitive dependencies.
Add an alternative library for the same capability.
Configure the underlying framework directly if the artifact owns that configuration.
Bypass the artifact's APIs or abstractions.

For example, if the approved persistence artifact encapsulates:

spring-boot-starter-data-jpa

do NOT add:

spring-boot-starter-data-jpa

directly to pom.xml.