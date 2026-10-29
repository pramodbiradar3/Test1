---
description: Generate read-only API documentation and contract for the current service
---

# Generate Read-Only Service Documentation

Analyze the current service repository and generate exactly two files:

- `service-catalogue-docs/README.md`
- `service-catalogue-docs/service-contract.yaml`

## 1. Analyze the repository

Inspect only relevant API controllers, GraphQL schemas, existing API specifications, DTOs, service implementations, security/configuration files, and focused tests.

Skip build output, generated code, dependencies, and unrelated files. Reuse existing documentation and specifications. Stop exploring once sufficient evidence is available.

Do not assume that every entity, database table, Java class, or internal method is a public API.

## 2. Include only read-only APIs

Select APIs by their actual behavior, not their HTTP method.

- Include operations that retrieve, search, list, filter, or query existing data without changing business or system state.
- Include read-only operations implemented using GET, POST, or other HTTP methods.
- Exclude operations that create, update, delete, submit, approve, cancel, trigger workflows, or otherwise modify state.
- For GraphQL, include only read-only queries. Exclude all mutations.
- Inspect implementation and authoritative documentation when needed to establish behavior.
- Exclude operations whose read-only behavior cannot be established confidently. Report them as unresolved in the final response.
- Do not assume GET is always read-only or POST always modifies data.

Examples:
- `GET /cases/{id}`: include if it only retrieves data.
- `POST /cases/search`: include if it only searches data.
- `POST /cases`: exclude if it creates a case.
- `PUT /cases/{id}`: exclude if it updates a case.
- GraphQL query: include if read-only.
- GraphQL mutation: exclude.

This is a documentation filter, not a change to runtime authorization or service behavior.

## 3. Output files

Create or update only:

- `service-catalogue-docs/README.md`
- `service-catalogue-docs/service-contract.yaml`

Create `service-catalogue-docs/` if it does not exist.

Do not overwrite or modify the service's existing README, source code, configuration, or other files.

If the output directory already exists, update only these two target files and preserve unrelated contents.

## 4. README.md

Include concise documentation covering:

- Service name and purpose
- Protocol
- Available datasets and capabilities, when identifiable
- Environment base URLs, when known
- Authentication requirements
- Included read-only operations
- Brief usage and security guidance
- Any unresolved information relevant to consumers

List only the read-only operations included in the contract.

## 5. service-contract.yaml

### REST services

Generate a valid OpenAPI Specification 3.1.0 document beginning with `openapi: 3.1.0`.

Include only verified read-only operations. Document their:

- Service metadata and environment-specific servers
- Paths and HTTP methods
- Operation IDs and summaries
- Path, query, and header parameters
- Request bodies, where applicable
- Response schemas and representative examples
- Relevant HTTP status codes and error responses
- Authentication and security requirements

Use standard OpenAPI locations for parameter, request-body, and response examples.

### GraphQL services

Use a concise, consistent YAML structure containing:

- `contractVersion`
- `service`
- `environments`
- `authentication`
- `policies`
- `datasets`
- `operations`

Include only verified read-only queries. Exclude mutations.

For each operation, document:

- `operationId`
- `name`
- `type: query`
- `dataset`
- `capability`, when identifiable
- `access: read`
- `description`
- `arguments`
- Complete GraphQL document under `graphql`
- `sampleRequest`
- `sampleResponse`

Each sample request must include the HTTP method, path, required headers, operation name, complete GraphQL query, and variables.

Each sample response must include the HTTP status code and representative response body, including GraphQL `data` and relevant error examples where appropriate.

## 6. Environments and accuracy

Use these environment names consistently:

- `dev`
- `qa`
- `uat`
- `prod`

Use actual environment URLs only when established from repository configuration or authoritative documentation. Otherwise, use clearly identified `TODO` placeholders; never invent URLs.

Use the actual implementation and authoritative API specifications as the source of truth. Do
