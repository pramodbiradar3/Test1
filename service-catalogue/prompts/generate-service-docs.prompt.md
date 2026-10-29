---
description: Generate isolated service documentation and API contract
---

# Generate Service Documentation

Analyze the current repository and generate exactly two files inside a new directory named `service-catalogue-docs/`:

- `service-catalogue-docs/README.md`
- `service-catalogue-docs/service-contract.yaml`

## Instructions

1. Inspect only relevant API controllers, GraphQL schemas, existing API specifications, DTOs, security/configuration files, and focused tests. Skip build output, generated code, dependencies, and unrelated files.

2. Do not overwrite or modify the service's existing README, source code, or any other files.

3. Generate `service-catalogue-docs/README.md` containing:
   - Service name, purpose, and protocol
   - Datasets and capabilities
   - DEV, QA, UAT, and PROD URLs, if known
   - Authentication requirements
   - Available operations
   - Brief usage and security guidance

4. Generate `service-catalogue-docs/service-contract.yaml`:
   - **REST:** Valid OpenAPI 3.1.0 with servers, paths, parameters, request/response schemas, status codes, security, and examples.
   - **GraphQL:** YAML with service metadata, environments, authentication, datasets, capabilities, and documented operations. Each operation must include arguments, the complete GraphQL document, `sampleRequest`, and `sampleResponse`.

5. Use the actual implementation and authoritative specifications. Do not invent endpoints, fields, arguments, URLs, or authentication mechanisms. Mark unavailable information as `TODO`.

6. Use concise, non-sensitive examples. Never include credentials, tokens, or production data.

7. If `service-catalogue-docs/` already exists, inspect and update only the two target files. Preserve unrelated contents.

8. Do not create ZIP files, validation schemas, utilities, CI pipelines, or additional files.

9. Avoid duplicate content
