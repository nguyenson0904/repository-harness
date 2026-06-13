# Architecture

Template này chưa chọn application stack.

Dùng tài liệu này như boundary guide mặc định cho implementation tương lai.
Khi stack hoặc architecture thật được chọn, ghi quyết định cụ thể vào
`docs/decisions/`.

## Discovery Before Shape

Trước khi đề xuất implementation shape, xác định:

- product surfaces: browser, mobile, desktop, CLI, API, worker, service,
- runtime stack: language, framework, database, queues, providers, hosting,
- core domains: khái niệm sản phẩm có tên và contract ổn định,
- boundary inputs: user input, API requests, webhooks, jobs, files,
  credentials, provider payloads, environment config,
- validation ladder: checks nhỏ nhất chứng minh stack đã chọn.

## Default Layering

```text
domain
  <- application
      <- infrastructure
          <- interface
              <- app surfaces
```

Chỉ tạo folder thật khi stack và story cần.

## Dependency Rule

Layer trong không được phụ thuộc layer ngoài.

| Layer | Có thể phụ thuộc | Không được phụ thuộc |
| --- | --- | --- |
| domain | pure utilities | framework, database, UI, provider, process/env |
| application | domain | framework, UI, provider, concrete database clients |
| infrastructure | domain, application | interface controllers hoặc UI |
| interface | backend layers | UI state hoặc platform shell assumptions |
| app surfaces | API contracts và app-facing clients | domain internals trực tiếp |

## Parse-First Boundary Rule

Dữ liệu unknown phải được parse ở boundary trước khi đi vào inner code.

Boundary gồm:

- HTTP request bodies, params, query strings,
- session payloads và identity claims,
- environment variables,
- database rows trả về từ external clients,
- platform shell payloads,
- deep links, tokens, signed URLs,
- provider webhooks, events, async payloads.

Target flow:

```text
unknown input
  -> parser
  -> typed DTO hoặc command
  -> application use case
  -> domain object/value object
```

## Command/Query Boundary

Nếu product có cả reads và writes:

- commands mutate state và sở hữu audit side effects,
- queries read state và format cho consumers,
- shared domain rules nằm trong domain/application, không nằm trong controllers.

## Observability

Khi project có server, ưu tiên một JSON log line chuẩn cho mỗi request:

- timestamp,
- level,
- request_id,
- user_id khi biết,
- action,
- duration_ms,
- status_code,
- message.

Audit logs là product records. Application logs là operational records. Không
dùng một loại để thay thế loại kia.
