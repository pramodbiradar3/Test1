# Copilot Artifact-First Governance Instructions

## Mandatory Artifact-First Governance

Before implementing or modifying any code, you MUST inspect the approved artifact catalog and identify the organization-provided artifacts applicable to the requirement.

### Artifact Catalog

The approved artifact catalog is located at:

```text
.foundation/catalog.yaml
```

Artifact contracts are located under:

```text
.foundation/artifacts/
```

The catalog may contain multiple approved artifacts for different capabilities, use cases, and technical concerns.

The catalog is the source of truth for identifying approved organization-provided artifacts.

## Mandatory Artifact Resolution Process

For every requirement, before writing or modifying implementation code:

1. Understand the requirement.
2. Identify all technical capabilities required by the requirement.
3. Read and inspect:

   ```text
   .foundation/catalog.yaml
   ```

4. For each required capability, determine whether an approved artifact exists in the catalog.
5. If an approved artifact exists:

   * Identify the artifact.
   * Locate its corresponding artifact contract under:

     ```text
     .foundation/artifacts/
     ```

   * Read and understand the complete artifact contract.
   * Read and understand the complete artifact README.md.
   * Use the approved artifact according to its contract.

6. Repeat this process for every applicable capability.
7. Only begin implementation after all applicable artifacts and contracts have been identified and reviewed.

The required flow is:

```text
Requirement
    ↓
Identify Required Capabilities
    ↓
Inspect Artifact Catalog
    ↓
Resolve Applicable Approved Artifacts
    ↓
Read Corresponding Artifact Contracts
    ↓
Create Implementation Plan
    ↓
Implement Using Approved Artifacts
```

## Mandatory Artifact Reuse Rule

If the artifact catalog contains an approved artifact for a required capability, you MUST use that approved artifact.

This rule applies to every capability, including but not limited to:

* Database persistence
* Authentication and authorization
* Messaging and Kafka
* Logging
* Auditing
* Notifications
* Comments
* Caching
* Observability
* Any other capability listed in the artifact catalog

You MUST NOT:

* Add an alternative library for a capability already provided by an approved artifact.
* Add a duplicate dependency.
* Reimplement functionality already provided by an approved artifact.
* Bypass the approved artifact's APIs, base classes, interfaces, or extension points.
* Replace an approved artifact with a different library based on personal preference.
* Make assumptions about how an approved artifact should be used without reading its contract.

## Mandatory Rule

Before implementing or modifying any code, you MUST identify the required capabilities and resolve all applicable approved organization artifacts.

You MUST NOT start implementation until the artifact resolution process is complete.

## Artifact Contract Compliance

The artifact contract is the authoritative source for how an approved artifact must be used.

Before implementing with an approved artifact, read its corresponding contract and follow all applicable requirements, including:

* Required dependencies
* Dependency restrictions
* Configuration
* APIs
* Base classes
* Interfaces
* Extension points
* Annotations
* Repository patterns
* Transaction management
* Integration patterns
* Usage constraints
* Prohibited usage patterns

The implementation MUST conform to the artifact contract.

Do not bypass, replace, or recreate functionality defined by an approved artifact contract.

## Multiple Artifact Resolution

A single requirement may require multiple capabilities and therefore multiple approved artifacts.

You MUST:

1. Identify every required capability.
2. Resolve every applicable artifact from the catalog.
3. Read every corresponding artifact contract.
4. Use all applicable approved artifacts together.
5. Ensure the artifacts are used according to their individual contracts.

Example:

```text
Requirement
    │
    ├── Persistence Capability
    │       └── Approved Artifact → Read Contract
    │
    ├── Messaging Capability
    │       └── Approved Artifact → Read Contract
    │
    └── Logging Capability
            └── Approved Artifact → Read Contract
```

Do not stop after finding the first applicable artifact.

## Missing Artifact

If a required capability does not have an approved artifact in the catalog:

1. Clearly identify the missing capability.
2. Do not silently introduce a replacement library.
3. Do not assume that an external library is permitted.
4. Explain the proposed dependency or implementation.
5. Ask for approval before introducing a new external dependency or alternative implementation.

## Contract Conflicts

If the consumer requirement conflicts with an artifact contract:

1. Identify the conflict.
2. Preserve the artifact contract by default.
3. Do not silently deviate from the contract.
4. Ask for clarification or approval before implementing a deviation.

## Implementation Gate

Do not begin implementation until the following checks are complete:

* [ ] The requirement has been analyzed.
* [ ] All required technical capabilities have been identified.
* [ ] .foundation/catalog.yaml has been inspected.
* [ ] All applicable approved artifacts have been identified.
* [ ] The corresponding artifact contracts have been located.
* [ ] All applicable artifact contracts have been read.
* [ ] The implementation plan uses the approved artifacts.
* [ ] No duplicate or alternative library is being introduced for an existing approved capability.

An implementation is invalid if an approved artifact exists for a required capability but an alternative library, duplicate dependency, or duplicate implementation is introduced.

This artifact-first governance is mandatory for every implementation task.
