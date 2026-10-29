---
description: Generate service README.md and service-contract.yaml
---

# Generate Service Documentation

Analyze the current service repository and generate exactly two files:
- `README.md`
- `service-contract.yaml`

## Instructions

1. Inspect only relevant API controllers, GraphQL schemas, existing API specifications, DTOs, exception handlers, security configuration, application configuration, and focused tests. Do not scan build output, generated code, dependencies, or unrelated files.

2. Reuse existing documentation and specifications. Stop exploring once sufficient evidence is available.

3. Generate `README.md` containing:
   - Service purpose and protocol
   - Datasets and capabilities
   - Environment URLs, if known
   - Authentication
   - Available operations
   - Brief usage guidance and security considerations

4. Generate `service-contract.yaml`:
   - **REST:** Valid OpenAPI 3.1.0 document, including servers, paths, parameters, request/response schemas, status codes, security, and examples.
   - **GraphQL:** YAML containing service metadata, environments, authentication, datasets, capabilities, and documented operations. Each operation must include its complete GraphQL document, arguments, `sampleRequest`, and `sampleResponse`.

5. Use actual implementation and authoritative specifications as the source of truth. Do not invent endpoints, fields, arguments, URLs, or authentication mechanisms. Mark unavailable information as `TODO`.

6. Use non-sensitive examples. Never include credentials, tokens, or production data.

7. Preserve useful existing content. Create or update only `README.md` and `service-contract.yaml`. Do not modify source code, other documentation, dependencies, CI pipelines, or any other files.

8. Do not generate ZIP files, validation schemas, utilities, or additional files.

9. Keep both files concise. Avoid duplicate documentation, unnecessary repository summaries, and lengthy explanations.

## Final response

Briefly report the two files created or updated and any unresolved `TODO` items. Do not claim unverified details are confirmed.
