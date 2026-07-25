---
name: Read Ripe brand website content
description: >-
  Retrieve published pages and media from a Ripe Insurance brand website through the
  Umbraco Content Delivery API — list, filter, sort, page, and fetch single items by GUID
  or URL path, requesting only the properties you need. This is Ripe's only public API and
  it returns website content, not insurance data.
api: openapi/ripe-insurance-umbraco-content-delivery-openapi.json
base_url: https://www.ripeinsurance.co.uk/umbraco/delivery/api/v2
operations:
  - GetContent2.0
  - GetContentItemById2.0
  - GetContentItemByPath2.0
  - GetContentItems2.0
method: generated
generated: '2026-07-25'
---

# Read Ripe brand website content

## What this API is, and is not

Ripe Insurance publishes **no insurance API**. There is no quote, bind, issue, policy,
billing or FNOL endpoint on any Ripe brand, and no developer portal to obtain one. The
surface below is the **Umbraco CMS Content Delivery API** that ships with the .NET content
management system running the brand websites. It returns pages and media. Treat anything
you retrieve as marketing content, not as a policy, price or cover confirmation.

Ripe does not document or promote this API, and `robots.txt` on every brand host carries
`Disallow: /umbraco/`. Read politely: cache aggressively, keep concurrency to one, and do
not crawl the whole tree.

## Authentication

None. Every operation is served anonymously — verified 2026-07-25 against
`/umbraco/delivery/api/v2/content`, which returned HTTP 200 with `total: 345`.

An optional `Api-Key` **header** is declared on every operation (an Umbraco configuration
feature), but Ripe publishes no way to obtain a key, so omit it. A separate OpenID Connect
server exists for website customer login (`/.well-known/openid-configuration`); it is for
consumers, not integrators, and is only relevant if you hit a `401` on member-protected
content — which you cannot resolve. See `authentication/ripe-insurance-authentication.yml`.

## Hosts

| Brand | Host | Operations |
|---|---|---|
| Ripe Insurance | `https://www.ripeinsurance.co.uk` | 8 (v2 only) |
| Cycleplan | `https://www.cycleplan.co.uk` | 16 (v1 + v2) |
| Golf Care | `https://www.golfcare.co.uk` | 16 (v1 + v2) |
| Insure4Sport | `https://www.insure4sport.co.uk` | 16 (v1 + v2) |
| Insure4Boats | `https://www.insure4boats.co.uk` | none (404) |

Always call **v2**. On `www.ripeinsurance.co.uk` the v1 paths return `400` — they were
withdrawn with no notice and no `Sunset` header.

## Steps

### 1. List content — `GetContent2.0`

`GET /umbraco/delivery/api/v2/content`

Query parameters (all optional):

- `fetch` — scope the set relative to a node: `children:{id}`, `children:{path}`,
  `descendants:{id}`, `ancestors:{id}`, or omit for everything.
- `filter` — repeatable expressions: `contentType:alias`, `name:nodeName`,
  `createDate<2024-01-01`, `updateDate>:2023-01-01`.
- `sort` — repeatable, per the examples published in the spec: `createDate:asc|desc`,
  `updateDate:asc|desc`, `name:asc|desc`, `sortOrder:asc|desc`.
- `skip` / `take` — offset paging. Read `total` from the response and page until you have
  consumed it.
- `fields` — **use this**. `properties[alias1,alias2]` returns only the properties you
  named instead of every property on every page.
- `expand` — `properties[$all]` or `properties[alias1[properties[nested1]]]` to walk into
  nested content.

Headers: `Accept-Language` (language variants), `Accept-Segment` (segment variants),
`Start-Item` (a root GUID or URL segment, to scope the query to one site root).

Response: `PagedIApiContentResponseModel` — `{ total, items[] }`, each item carrying `id`
(GUID), `contentType`, `name`, `createDate`, `updateDate`, `route`, `cultures` and an
untyped `properties` map.

### 2. Fetch one item — `GetContentItemByPath2.0` or `GetContentItemById2.0`

`GET /umbraco/delivery/api/v2/content/item/{path}` when you have the URL segment (this is
the natural join from a page URL you already have), or
`GET /umbraco/delivery/api/v2/content/item/{id}` when you hold the GUID from a previous
listing. Same `fields`/`expand` parameters apply.

### 3. Batch fetch — `GetContentItems2.0`

`GET /umbraco/delivery/api/v2/content/items?id={guid}&id={guid}` — pass the `id` query
parameter repeatedly. Prefer one batch call over N single fetches.

## Rules

- **Do not retry on `4xx`.** Every operation is a `GET` and therefore safe to retry on
  `5xx` or a network fault with exponential backoff. There is no idempotency key because
  there are no writes — see `conventions/ripe-insurance-conventions.yml`.
- **`400`** means a malformed `fetch`/`filter`/`sort` expression or a v1 path on a v2-only
  host. It returns an RFC 7807-shaped `ProblemDetails` body served as `application/json`
  (not `application/problem+json`); `type` is nullable and never populated, so classify on
  the HTTP status, not the body.
- **`401` / `403`** mean member-protected content. These have **no response body** and you
  cannot resolve them — no developer credential exists. Skip the item and move on.
- **`404`** means no such id or path, or the item is outside your `Start-Item` scope.
  Note that a protected item can also present as `404` depending on configuration.
- **No rate-limit headers are published.** Nothing tells you when you are going too fast;
  self-throttle.
- `properties` is an open map with no schema. Never assume a property alias exists —
  check before reading, and expect the shape to change silently when Ripe upgrades the CMS.

## Prefer llms.txt for product questions

If the task is "what does Cycleplan cover" rather than "give me this page object", read the
brand `llms.txt` instead — it is a curated, annotated link map Ripe actually maintains for
agents:

- `https://www.cycleplan.co.uk/llms.txt`
- `https://www.golfcare.co.uk/llms.txt`
- `https://www.insure4sport.co.uk/llms.txt`

(`https://www.ripeinsurance.co.uk/llms.txt` returns 200 with zero bytes — it is published
empty.) Verbatim copies are in `llms/` in this repository.
