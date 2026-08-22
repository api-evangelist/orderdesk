# Order Desk (orderdesk)

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
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Order Desk is an ecommerce order management and fulfillment routing platform that centralizes orders from shopping carts and marketplaces, then automates routing to print-on-demand, dropshipping, warehouse, and shipping providers via a rule builder and 300-plus integrations. Its public REST API (base `https://app.orderdesk.me/api/v2`) exposes Orders, Order Items, Shipments, Inventory Items, and Store settings so developers can create and update orders, manage line items, record shipments and tracking, and sync inventory programmatically.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/orderdesk/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/orderdesk/refs/heads/main/apis.yml)

## Access Model

Order Desk publishes a documented, public REST API at [apidocs.orderdesk.com](https://apidocs.orderdesk.com/) (the older `apidocs.orderdesk.me` host now redirects here). The API is available to any Order Desk store on a paid or trial plan - there is no separate developer signup or API-only tier.

- **Base URL:** `https://app.orderdesk.me/api/v2`
- **Authentication:** two request headers on every call:
  - `ORDERDESK-STORE-ID` - the numeric ID of your store
  - `ORDERDESK-API-KEY` - the store's API key
  - Credentials are found in the Order Desk dashboard under Store Settings → API. Each store has its own store ID and key, so the API is scoped to a single store per credential pair.
- **Format:** JSON request and response bodies. List responses wrap results in a `status` field plus the resource array and pagination metadata (`total_records`, `records_returned`, `offset`, `limit`).
- **Pagination:** `limit` (default 50, max 500) and `offset` query parameters on list endpoints.
- **Rate limiting:** a leaky-bucket limiter - a 20-request bucket that refills at 3 requests/second (~100 requests per rolling 30-second window). Remaining quota is reported in the `X-Tokens-Remaining` header; exceeding it returns HTTP 429 with an `X-Retry-After` header. See [rate-limits/orderdesk-rate-limits.yml](rate-limits/orderdesk-rate-limits.yml).

There is no documented public WebSocket or streaming API; the surface is request/response REST over HTTPS. Order Desk does offer outbound webhooks and inbound integrations elsewhere in the product, but those are configured in the dashboard rather than through this REST API.

## Tags

- Ecommerce
- Order Management
- Fulfillment
- Dropshipping
- Inventory
- Shipping

## Timestamps

- **Created:** 2026-07-11
- **Modified:** 2026-07-11

## APIs

### Order Desk Orders API

Create, retrieve, search, update, and delete orders in an Order Desk store. Filter orders by folder, status, source, date, and customer, add order history notes, and move orders between folders to drive fulfillment workflows.

- **Human URL:** [https://apidocs.orderdesk.com/](https://apidocs.orderdesk.com/)
- **Base URL:** `https://app.orderdesk.me/api/v2`

#### Tags

- Orders
- Order Management
- Ecommerce

#### Properties

- [Documentation](https://apidocs.orderdesk.com/)
- [API Reference](https://apidocs.orderdesk.com/)
- [OpenAPI](openapi/orderdesk-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/orderdesk.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/orderdesk.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Order Desk Order Items API

Manage the individual line items within an order - list, get, add, update, and remove items, adjust quantities, prices, variations, and per-item metadata without rewriting the whole order.

- **Human URL:** [https://apidocs.orderdesk.com/](https://apidocs.orderdesk.com/)
- **Base URL:** `https://app.orderdesk.me/api/v2`

#### Tags

- Order Items
- Line Items
- Orders

#### Properties

- [API Reference](https://apidocs.orderdesk.com/)
- [OpenAPI](openapi/orderdesk-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/orderdesk.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/orderdesk.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Order Desk Shipments API

Record and manage shipments against an order - create shipments with carrier and tracking details, list, get, update, and delete them, and batch-add many shipments at once to reconcile fulfillment from external providers.

- **Human URL:** [https://apidocs.orderdesk.com/](https://apidocs.orderdesk.com/)
- **Base URL:** `https://app.orderdesk.me/api/v2`

#### Tags

- Shipments
- Tracking
- Fulfillment

#### Properties

- [API Reference](https://apidocs.orderdesk.com/)
- [OpenAPI](openapi/orderdesk-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/orderdesk.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/orderdesk.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Order Desk Inventory Items API

Maintain the store's inventory catalog - list, get, create, update, and delete inventory items by code, adjust stock counts, prices, and metadata, and batch-update many items in a single request to keep stock in sync.

- **Human URL:** [https://apidocs.orderdesk.com/](https://apidocs.orderdesk.com/)
- **Base URL:** `https://app.orderdesk.me/api/v2`

#### Tags

- Inventory
- Stock
- Catalog

#### Properties

- [API Reference](https://apidocs.orderdesk.com/)
- [OpenAPI](openapi/orderdesk-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/orderdesk.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/orderdesk.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Order Desk Store API

Read store settings and structure - retrieve the store's folder list and configuration, and test API connectivity and credentials before running order, item, shipment, or inventory operations.

- **Human URL:** [https://apidocs.orderdesk.com/](https://apidocs.orderdesk.com/)
- **Base URL:** `https://app.orderdesk.me/api/v2`

#### Tags

- Store Settings
- Folders
- Configuration

#### Properties

- [API Reference](https://apidocs.orderdesk.com/)
- [OpenAPI](openapi/orderdesk-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/orderdesk.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/orderdesk.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

## Common Properties

- [LinkedIn](https://www.linkedin.com/company/order-desk)
- [Website](https://www.orderdesk.com)
- [Documentation](https://apidocs.orderdesk.com/)
- [Plans](plans/orderdesk-plans-pricing.yml)
- [Rate Limits](rate-limits/orderdesk-rate-limits.yml)
- [Fin Ops](finops/orderdesk-finops.yml)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
