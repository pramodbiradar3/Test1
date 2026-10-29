# Service Catalogue

## Overview

The Service Catalogue is a centralized repository of enterprise service contracts. It enables developers and AI coding assistants, including GitHub Copilot, to discover available services, understand their capabilities, and integrate with approved APIs using documented contracts.

The catalogue supports services using different API protocols, including REST and GraphQL.

## Repository Structure

```text
service-catalogue/
├── README.md
├── catalogue.yaml
├── .github/
│   └── copilot-instructions.md
└── services/
    └── <service-id>/
        ├── service-contract.yaml
        └── README.md
```

## Catalogue Components

### `catalogue.yaml`

The central registry of available services. It provides each service's identifier, name, description, protocol, contract location, documentation location, datasets, and supported capabilities.

### `services/<service-id>/service-contract.yaml`

Contains the machine-readable contract for an individual service, including:

- Service metadata and API protocol
- Environment-specific base URLs
- Available endpoints or GraphQL operations
- Request parameters and arguments
- Request and response schemas
- Sample requests and responses
- Authentication requirements
- Approved capabilities and usage restrictions

The contract format depends on the service protocol. REST services can use OpenAPI, while GraphQL services can document their operations and schema information in YAML.

### `services/<service-id>/README.md`

Contains service-specific documentation, including business context, dataset descriptions, relationships, usage guidance, limitations, and ownership information.

### `.github/copilot-instructions.md`

Provides repository-level instructions to help GitHub Copilot discover the appropriate service, follow its contract, select the correct environment, and generate integrations consistent with the documented capabilities.

## How to Use the Catalogue

1. Consult `catalogue.yaml` to discover the relevant service.
2. Read the service-specific README to understand its business context.
3. Review `service-contract.yaml` to identify the appropriate operation.
4. Select the environment appropriate to the development or deployment task.
5. Use the documented parameters, request examples, response schemas, and authentication requirements.
6. Follow the service's authorization and data-access policies.

## Environment Conventions

Services may define the following environments:

| Environment | Purpose |
|---|---|
| `dev` | Development and initial integration |
| `sit` | System integration testing |
| `uat` | User acceptance testing |
| `prod` | Production |

Use only the configured environment URLs. Never invent a base URL or assume that endpoints and permissions are identical across environments.

## Contract and Documentation Guidelines

- Maintain one service directory per registered service.
- Keep each service's contract and README in its own directory.
- Document operations, required parameters, expected responses, and representative examples.
- Use non-production sample data.
- Keep service metadata and the central registry consistent.
- Document only verified capabilities and supported operations.
- Avoid storing credentials, access tokens, or other secrets in the repository.

## Security and Governance

The catalogue documents service capabilities and intended usage. It does not itself enforce API permissions.

Actual authentication, authorization, data filtering, and read-only restrictions must be enforced by the service or its API gateway.

Use approved operations only. If a required capability or operation is missing from the catalogue, confirm the requirement with the service owner before implementing it.

## Adding or Updating a Service

1. Create or update the service directory under `services/`.
2. Add or update `service-contract.yaml`.
3. Add or update the service-specific `README.md`.
4. Register the service or update its metadata in `catalogue.yaml`.
5. Review environment URLs, examples, security requirements, and documented capabilities.
6. Submit the changes for review according to the repository's contribution process.

## Important Notes

- Example URLs and payloads must be verified before production use.
- The service contract is the reference for documented API behavior.
- Changes to API capabilities should be reflected in both the service contract and central registry.
- The catalogue should not contain production secrets or sensitive real-world response samples.
