# Ripe Insurance (ripe-insurance)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

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
