# Architecture

No application stack is selected by this template.

Use this document as the default boundary guide for future implementation. Add
project-specific decisions under `docs/decisions/` when the real stack or
architecture becomes known.

## Discovery Before Shape

Before proposing implementation shape, identify:

- product surfaces: browser, mobile, desktop, CLI, API, worker, service,
- runtime stack: language, framework, database, queues, providers, hosting,
- core domains: stable product concepts and names,
- boundary inputs: user input, API requests, webhooks, jobs, files,
  credentials, provider payloads, environment config,
- validation ladder: smallest checks that prove the selected stack.

## Default Layering

```text
domain
  <- application
      <- infrastructure
          <- interface
              <- app surfaces
```

Create real folders only when the selected stack and story need them.

## Dependency Rule

Inner layers must not depend on outer layers.

| Layer | May depend on | Must not depend on |
| --- | --- | --- |
| domain | pure utilities | framework, database, UI, provider, process/env |
| application | domain | framework, UI, provider, concrete database clients |
| infrastructure | domain, application | interface controllers or UI |
| interface | backend layers | UI state or platform shell assumptions |
| app surfaces | API contracts and app-facing clients | domain internals directly |

## Parse-First Boundary Rule

Unknown data must be parsed at boundaries before it enters inner code.

Boundaries include:

- HTTP request bodies, params, and query strings,
- session payloads and identity claims,
- environment variables,
- database rows returned from external clients,
- platform shell payloads,
- deep links, tokens, and signed URLs,
- provider webhooks, events, and async payloads.

Target flow:

```text
unknown input
  -> parser
  -> typed DTO or command
  -> application use case
  -> domain object/value object
```

## Command/Query Boundary

If the product has both reads and writes:

- commands mutate state and own audit side effects,
- queries read state and format for consumers,
- shared domain rules live in domain/application, not controllers.

## Observability

When the project has a server, prefer one canonical JSON log line per request:

- timestamp,
- level,
- request_id,
- user_id when known,
- action,
- duration_ms,
- status_code,
- message.

Audit logs are product records. Application logs are operational records. Do
not use one as a substitute for the other.
