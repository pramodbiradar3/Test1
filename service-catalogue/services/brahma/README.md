# Brahma Service

## Overview

Brahma is a REST service for retrieving Case entity information.

## Contract

- Contract: `services/brahma/service-contract.yaml`
- Protocol: REST
- Format: OpenAPI 3.1
- Dataset: Case
- Capability: `case.read`

## Environments

The service contract documents DEV, QA, PREPROD, and PROD base URLs.
Replace the example URLs with the approved Brahma endpoints.

## API usage

The illustrative contract defines a read operation for retrieving a case
by its case ID.

Before implementing an integration, verify the endpoint, fields, response
schema, and authentication requirements against the actual Brahma API.

## Authentication

The example contract uses bearer-token authentication. Confirm the actual
authentication mechanism with the service owner.

Do not store tokens or credentials in this repository.

## Integration guidelines

- Use the documented HTTP method and endpoint.
- Supply the required case identifier.
- Handle documented success and error responses.
- Do not assume undocumented fields or operations exist.
- Avoid logging sensitive case information.
