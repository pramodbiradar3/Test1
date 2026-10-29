# Alekha Service

## Overview

Alekha is a GraphQL service exposing enterprise datasets.

## Contract

- Contract: `services/alekha/service-contract.yaml`
- Protocol: GraphQL over HTTP
- Dataset: Case, Task, Client, Events
- Capabilities:
  - `case.read`
  - `task.read`
  - `client.read`
  - `events.read`

## Environments

The service contract documents DEV, SIT, UAT, and PROD GraphQL endpoints.
Replace the example URLs with the approved Alekha endpoints.

## Available operations

The illustrative contract documents these queries:

- GetCase
- GetTasks
- GetClient
- GetEvents

These operation names, fields, arguments, and response structures are
examples until verified against the actual Alekha GraphQL schema.

## Authentication

The example contract uses bearer-token authentication. Verify the
actual authentication mechanism with the service owner.

## Integration guidelines

- Use the documented GraphQL endpoint.
- Reuse documented query operations and field selections.
- Do not invent fields, relationships, arguments, or mutations.
- Request only the fields required by the use case.
- Handle GraphQL errors returned in the `errors` array.
- Use the correct environment for the task.
- Do not store credentials or tokens in this repository.
