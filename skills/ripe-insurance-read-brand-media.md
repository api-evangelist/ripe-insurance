---
name: Read Ripe brand media assets
description: >-
  Retrieve media items — images, documents, policy PDFs published as media — from a Ripe
  Insurance brand website through the Umbraco Content Delivery API, including their crops,
  focal points and dimensions.
api: openapi/ripe-insurance-umbraco-content-delivery-openapi.json
base_url: https://www.ripeinsurance.co.uk/umbraco/delivery/api/v2
operations:
  - GetMedia2.0
  - GetMediaItemById2.0
  - GetMediaItemByPath2.0
  - GetMediaItems2.0
method: generated
generated: '2026-07-25'
---

# Read Ripe brand media assets

The media half of the Umbraco Content Delivery API. Same host, same anonymous access, same
caveats as `ripe-insurance-read-brand-content.md` — read that first. `robots.txt` carries
`Disallow: /umbraco/`; be conservative.

## Steps

### 1. List media — `GetMedia2.0`

`GET /umbraco/delivery/api/v2/media`

Supports `fetch`, `filter`, `sort`, `skip`, `take`, `fields` and `expand` exactly as the
content operations do. Returns `PagedIApiMediaWithCropsResponseModel` — `{ total, items[] }`.

### 2. Fetch one media item

- `GET /umbraco/delivery/api/v2/media/item/{path}` — `GetMediaItemByPath2.0`
- `GET /umbraco/delivery/api/v2/media/item/{id}` — `GetMediaItemById2.0`

### 3. Batch fetch — `GetMediaItems2.0`

`GET /umbraco/delivery/api/v2/media/items?id={guid}&id={guid}`

## The media object

`ApiMediaWithCropsResponseModel` (named `IApiMediaWithCropsResponseModel` on the Cycleplan,
Golf Care and Insure4Sport hosts, which run an older CMS build):

| Field | Notes |
|---|---|
| `id` | GUID, read-only |
| `name` | read-only |
| `mediaType` | the Umbraco media type alias |
| `url` | **required** — the fetchable asset URL |
| `extension`, `width`, `height`, `bytes` | nullable |
| `focalPoint` | `{ left, top }`, normalised doubles — use it when you crop |
| `crops[]` | `{ alias, width, height, coordinates: { x1, y1, x2, y2 } }` |
| `path` | media-tree path |
| `properties` | open map, no schema |
| `createDate`, `updateDate` | timestamps |

## Rules

- Read `url` for the asset itself; the API returns metadata, not bytes.
- Honour `focalPoint` and the named `crops[]` rather than centre-cropping — the crops are
  the ones Ripe's editors actually configured.
- `width`, `height`, `bytes` and `extension` are all nullable. Do not assume an image.
- Errors: `404` for an unknown id or path (no response body declared). `GetMedia2.0` also
  declares `400` with a `ProblemDetails` body for malformed query expressions. See
  `errors/ripe-insurance-problem-types.yml`.
- Every operation is a `GET`. Safe to retry on `5xx`; do not retry a `4xx`.
- Media assets are brand marketing material. Check
  `https://www.ripeinsurance.co.uk/terms-of-use/` before reusing anything.
