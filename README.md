# Ripe Insurance (ripe-insurance)

Ripe Insurance Services Limited, trading as Ripe and part of Ripe Thinking Limited, is a Stockport-based United Kingdom digital Managing General Agent and specialist insurance intermediary authorised and regulated by the Financial Conduct Authority (FRN 313411). Founded in 1997 and majority-backed by Aquiline Capital Partners, Ripe underwrites and distributes niche personal and small-commercial lines direct to consumers through its own brands — Cycleplan, Golf Care, Insure4Boats, Insure4Sport and Ripe Caravans — covering caravans and motorhomes, park homes and holiday homes, photography and music equipment, valuables, shooting, golf, cycling, boats, over 400 sports, personal trainers, hair and beauty businesses, clubs and leisure organisations, and small business. It reports more than 400,000 policyholders.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/ripe-insurance/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/ripe-insurance/refs/heads/main/apis.yml)

## Tags

- Insurance
- United Kingdom
- Insurtech
- Managing General Agent
- Specialist Insurance
- Personal Lines
- Small Business Insurance
- Underwriting
- Direct to Consumer
- Broker

## Timestamps

- **Created:** 2026-07-25
- **Modified:** 2026-07-25

## API Posture

Ripe publishes **no developer portal and no insurance API**. This is the honest finding, and it is the expected one for a UK direct-to-consumer digital MGA in a market with no open-insurance mandate.

- `developer.`, `developers.`, `docs.` and `api.` subdomains do not resolve. `/developers`, `/developer`, `/partners` and `/integrations` all return 404.
- The only integration path is commercial: the corporate [Partner with Us](https://www.ripethinking.co.uk/partner-with-us/) page is a business-development enquiry form with no specification, sandbox, or onboarding. Recorded as **gated**.
- **None** of quote, bind, issue, or FNOL is exposed as an API. Quoting and binding happen inside first-party consumer web funnels and, since 28 April 2026, the Cycleplan ChatGPT app — a real-time conversational quote that clicks through to payment, built in-house, with no published API, MCP server, or spec.
- **ACORD posture: no ACORD reference found.** Zero hits for ACORD, AL3, ACORD XML, NGDS, IVANS, Vertafore or Applied Epic across the consumer and corporate sites. Consistent with a D2C MGA that owns its distribution end to end and never touches agency-download rails.
- No webhooks, no AsyncAPI, no public Postman collection, no GraphQL, no gRPC.

## APIs

### Ripe Insurance Umbraco Content Delivery API

The read-only Umbraco CMS Content Delivery API served anonymously from the Ripe Insurance marketing and quote site. This is platform infrastructure that ships with Umbraco, **not an insurance product API** — eight GET operations over website content and media, with no quote, bind, issue, policy, billing, or FNOL capability. Confirmed live and parsing as OpenAPI 3.0.4 on 2026-07-25, with an equivalent surface on cycleplan.co.uk, golfcare.co.uk and insure4sport.co.uk. Ripe neither documents nor promotes it, and `robots.txt` carries `Disallow: /umbraco/`. It is recorded because it is real and publicly reachable, not because it constitutes an insurance API.

- **Human URL:** [https://www.ripeinsurance.co.uk/umbraco/swagger/index.html](https://www.ripeinsurance.co.uk/umbraco/swagger/index.html)
- **Base URL:** `https://www.ripeinsurance.co.uk/umbraco/delivery/api/v2`

#### Tags

- Content
- Media
- CMS
- Umbraco

#### Properties

- [OpenAPI](openapi/ripe-insurance-umbraco-content-delivery-openapi.json) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [API Reference](https://www.ripeinsurance.co.uk/umbraco/swagger/index.html)
- [Documentation](https://docs.umbraco.com/umbraco-cms/reference/content-delivery-api)

## Authentication

The only OAuth surface is Umbraco member authentication (OpenIddict) fronting the website customer login, discoverable at [`/.well-known/openid-configuration`](https://www.ripeinsurance.co.uk/.well-known/openid-configuration): `authorization_code`, `refresh_token` and `client_credentials` grants, `openid` and `offline_access` scopes, PKCE S256, RS256 id tokens. It is not a partner or developer authorization server, and no public client registration is offered. The harvested Content Delivery API requires no authentication at all.

## Links

- [Website](https://www.ripeinsurance.co.uk/)
- [Corporate site — Ripe Thinking](https://www.ripethinking.co.uk/)
- [Partner with Us](https://www.ripethinking.co.uk/partner-with-us/)
- [Technology](https://www.ripethinking.co.uk/technology/)
- [How to claim](https://www.ripeinsurance.co.uk/how-to-claim/)
- [News](https://www.ripethinking.co.uk/news/)
- [LinkedIn](https://uk.linkedin.com/company/ripe-insurance)

## Review

See [review.yml](review.yml) for the full reviewer finding, every probed URL with its HTTP status, spec provenance, ACORD scan, and auth model.
