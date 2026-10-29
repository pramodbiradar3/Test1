# Enterprise Service Catalogue

## 1. Overview

The Enterprise Service Catalogue provides a centralized, repository-based inventory of approved enterprise services and their API contracts.

It is intended to help developers and AI coding assistants, including GitHub Copilot Agent Mode in IntelliJ IDEA, discover existing APIs before implementing new integrations.

The catalogue supports REST and GraphQL services and provides:

- A central registry of available services, datasets, capabilities, and contract locations.
- Service-specific API contracts describing available operations, parameters, and responses.
- Environment-specific base URLs for development, SIT, UAT, and production.
- Sample requests and responses to guide implementation.
- Copilot instructions for discovering and consuming documented APIs consistently.

## 2. Repository structure

```text
service-catalogue/
├── README.md
├── catalogue.yaml
├── .github/
│   └── copilot-instructions.md
└── services/
    ├── brahma/
    │   ├── service-contract.yaml
    │   └── README.md
    └── alekha/
        ├── service-contract.yaml
        └── README.md
```

## 3. Catalogue components

### `catalogue.yaml`

The central registry of services. Each entry identifies a service, its protocol, datasets, capabilities, supported environments, contract location, and documentation location.

### `.github/copilot-instructions.md`

Provides repository-specific guidance for GitHub Copilot. It instructs Copilot to consult the registry and service contracts before writing integration code and not to invent undocumented endpoints, operations, or fields.

### `services/<service-name>/service-contract.yaml`

Contains the service's API contract, environment configuration, authentication expectations, supported operations, and request/response examples.

REST services use OpenAPI. GraphQL services use a catalogue-specific YAML representation of documented GraphQL operations.

### `services/<service-name>/README.md`

Contains service-specific usage guidance, capabilities, environment details, and important integration considerations.

## 4. Currently catalogued services

| Service | Protocol | Available datasets |
|---|---|---|
| Brahma | REST | Case |
| Alekha | GraphQL | Case, Task, Client, Events |

The service-specific documentation and contracts are the authoritative references for the operations and fields documented in this repository.

## 5. Environment configuration

Each service contract documents its base URL for the following environments:

- **DEV:** Development
- **SIT:** System Integration Testing
- **UAT:** User Acceptance Testing
- **PROD:** Production

The example URLs in this repository are placeholders. Replace them with the actual approved service URLs before using the contracts in an application.

Environment selection should be explicit in application configuration. Avoid hardcoding environment-specific URLs throughout application code.

## 6. Guidelines for API consumers

1. Read `catalogue.yaml` to discover the appropriate service.
2. Read the service-specific README for integration guidance.
3. Consult `service-contract.yaml` for the documented API operations, fields, parameters, and response formats.
4. Use the documented authentication mechanism and approved environment configuration.
5. Follow the documented capability and access restrictions.
6. Handle errors and unexpected responses appropriately.
7. Do not create duplicate service integrations when an appropriate catalogued API already exists.

For Copilot-assisted development, follow `.github/copilot-instructions.md` in addition to these guidelines.

## 7. Adding a new service

To add a service:

1. Create a directory under `services/` using the service's agreed identifier.
2. Add `service-contract.yaml` with the appropriate REST or GraphQL contract representation.
3. Add a service-specific `README.md`.
4. Register the service in `catalogue.yaml`.
5. Document its supported environments, datasets, capabilities, authentication requirements, operations, and sample requests and responses.
6. Ensure the contract reflects the actual service API and has been reviewed by the service owner.
7. Update the Copilot instructions only if the catalogue's general discovery or consumption rules change.

## 8. Updating an existing service

When a service changes, update its contract and service-specific README. Keep the registry aligned with the supported capabilities and datasets.

Document breaking changes, deprecated operations, changed fields, and environment URL changes where applicable. Coordinate changes with the service owner.

## 9. Security and governance

The catalogue documents API discovery and intended usage; it does not itself enforce authorization or access control.

- Never store credentials, bearer tokens, passwords, private keys, or other secrets in this repository.
- Use approved identity and token-management mechanisms.
- Use non-production example data in documentation.
- Follow service-owner authorization requirements and organizational security policies.
- Do not assume that an operation is authorized merely because it appears in the catalogue.
- Production access must follow the applicable organizational approval process.

Copilot instructions are guidance for AI-assisted development, not a security boundary. Actual access restrictions must be enforced by the service, identity provider, and runtime controls.

## 10. Source of truth

Use the following order when implementing an integration:

1. The actual service schema and authoritative service-owner documentation.
2. The service's approved contract in this repository.
3. The service-specific README.
4. The central catalogue metadata.

If the contract and the actual API disagree, confirm the correct behavior with the service owner before implementing the integration.
