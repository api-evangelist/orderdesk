# Order Desk (orderdesk)

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
