# Organization Development Instructions

## Mandatory Foundation Artifact Process

Before implementing any requirement:

1. Understand the requirement.
2. Identify all required technical capabilities.
3. Check `.foundation/artifacts/catalog.yaml`.
4. For every required capability, identify the approved Foundation artifact.
5. Read the artifact's `artifact-contract.yaml`.
6. Read the artifact's `README.md`.
7. Follow all mandatory rules from every applicable artifact contract.
8. Use Foundation APIs instead of implementing equivalent functionality.
9. Do not introduce an alternative dependency if an approved Foundation artifact
   provides the required capability.
10. Only add an additional dependency when no approved Foundation artifact
    provides the required capability.

---

# Capability Mapping

Use the following mapping from the catalog:

| Capability | Approved Artifact |
|---|---|
| persistence | foundations-persistence |
| messaging | foundations-kafka |
| logging | foundations-logging |
| audit | foundations-audit |

---

# Required Implementation Process

Before writing implementation code, create an internal capability matrix:

| Requirement | Capability | Approved Artifact |
|---|---|---|
| Store customer | persistence | foundations-persistence |
| Publish event | messaging | foundations-kafka |
| Application logs | logging | foundations-logging |
| Audit creation | audit | foundations-audit |

Then read the applicable contracts.

---

# Important

Do not start implementation until all applicable Foundation artifact contracts
have been reviewed.

If an artifact does not provide a required capability:

1. State that the capability is not provided.
2. Explain why an additional dependency is required.
3. Propose the dependency.
4. Do not silently add the dependency.