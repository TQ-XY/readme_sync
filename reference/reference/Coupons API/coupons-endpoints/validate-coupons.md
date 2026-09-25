---
api:
  file: coupon.json
  operationId: post_coupons-accountid-channel-channellinkid-coupons-validate
hidden: false
link:
  new_tab: false
metadata:
  robots: index
---
# Purpose

Validate one or more coupon codes for an order in a single request.

## Format

To validate coupon eligibility and discount amounts, these are computed against the order content provided in the request, any changed content can be re-validated to confirm eligibility.

Each coupon code is validated **independently**, so any invalid or ineligible codes will not fail the whole request<br /><br />There are two scenarios where validating coupons is reccomended;

- **When a customer enters a coupon code** - check for eligibility and confirm the discount to apply to the order.
- **Whenever an order changes** - with items added, removed, quantities updated, coupons need revalidated with the updated content.

## Path Parameters

| Path parameter  | Type   | Description                                                                                                                             |
| --------------- | ------ | --------------------------------------------------------------------------------------------------------------------------------------- |
| `accountId`     | string | The Deliverect account id.                                                                                                              |
| `channelLinkId` | string | The channel link id the order belongs to. The account, location and channel used for validation are all derived from this channel link. |

### Revalidating after the order changes

Whenever the customer's order mutates, re-validate by sending **all** the codes relevant to the order in `codes` — both any code the customer just entered and any code(s) already applied to the order from a previous validation — in a single call against the current order state. Then, for each result:

- `applicable: false` → the code is no longer eligible for the current order (e.g. a PLU-scoped discount whose matching item was removed, or a minimum-spend coupon that no longer qualifies after items were removed). Un-apply it from the order and surface `validationErrors` to the customer.
- `applicable: true` → re-apply the returned `discounts` as-is, replacing whatever was previously applied for that code. **Don't reuse a previously computed amount**: a `percent_off` discount's effective amount depends on the order total and an `item`-scoped discount's depend on which basket items are currently present — both can change even when the code itself remains valid.

Reconcile the order's totals using the fresh discount amounts from the latest call, not the amounts from any earlier validation. This keeps the customer from checking out with a stale discount amount, or one that no longer applies at all, after the order has changed since it was last validated.

###

## Request body

| Field       | Type                   | Required | Description                                                                             |
| ----------- | ---------------------- | -------- | --------------------------------------------------------------------------------------- |
| `sessionId` | string                 | Yes      | Client/session identifier for the checkout session the coupons are being validated for. |
| `order`     | [Order](#order-object) | Yes      | The order the coupons are being validated against.                                      |
| `codes`     | array of string        | Yes      | The coupon codes to validate. At least one is required. Codes cannot be empty or blank. |

### Order object

| Field        | Type                          | Required | Description                                                         |
| ------------ | ----------------------------- | -------- | ------------------------------------------------------------------- |
| `orderType`  | string                        | Yes      | The order's fulfillment type. One of `delivery`, `pickup`, `eatIn`. |
| `items`      | array of [Item](#item-object) | Yes      | The items on the order/basket.                                      |
| `placedTime` | string (ISO 8601 date-time)   | No       | When the order was/will be placed.                                  |

### Item object

| Field   | Type    | Required | Description                                                                                                            |
| ------- | ------- | -------- | ---------------------------------------------------------------------------------------------------------------------- |
| `id`    | string  | Yes      | The item's own id on the basket. Used to resolve item-scoped discounts back to the specific basket line they apply to. |
| `plu`   | string  | Yes      | The item's PLU.                                                                                                        |
| `price` | integer | Yes      | The item's price, in the smallest currency unit (e.g. `$2.00` → `200`).                                                |

### Example request

```json
{
  "sessionId": "session-123",
  "order": {
    "orderType": "delivery",
    "items": [
      {
        "id": "64f1a2b3c4d5e6f7a8b9c0d3",
        "plu": "SKU-001",
        "price": 1500
      },
      {
        "id": "64f1a2b3c4d5e6f7a8b9c0d4",
        "plu": "SKU-002",
        "price": 800
      }
    ]
  },
  "codes": [
    "SUMMER25",
    "INVALIDCODE"
  ]
}
```

## Response

Returns a list with one result entry per requested code.

| Field              | Type                                                | Description                                                                                                       |
| ------------------ | --------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------- |
| `code`             | string                                              | The coupon code this result is for.                                                                               |
| `applicable`       | boolean                                             | Whether the code is valid and applicable to this order. `false` if the code doesn't exist or fails any condition. |
| `discounts`        | array of [Discounts](#discount-object)              | The discount(s) this coupon would apply, if `applicable` is `true`. Empty otherwise.                              |
| `description`      | string                                              | The coupon's description, if applicable.                                                                          |
| `validationErrors` | array of [ValidationError](#validationerror-object) | Present when `applicable` is `false`; explains why the code could not be applied.                                 |

### Discount object

| Field        | Type   | Description                                                    |
| ------------ | ------ | -------------------------------------------------------------- |
| `offer`      | object | The discount amount/type. See [Offer types](#offer-types).     |
| `scope`      | object | What the discount applies to. See [Scope types](#scope-types). |
| `provider`   | string | Always `"coupon"`.                                             |
| `externalId` | string | The coupon's code.                                             |
| `name`       | string | The coupon's name.                                             |

#### Offer types

Discriminated by `offer.type`:

| `type`        | Fields                                   | Description                                                                   |
| ------------- | ---------------------------------------- | ----------------------------------------------------------------------------- |
| `flat_off`    | `value` (integer)                        | A fixed amount off, in the smallest currency unit.                            |
| `percent_off` | `value` (integer), `maxAmount` (integer) | A percentage off, in basis points (e.g. `2500` = 25%), capped at `maxAmount`. |

#### Scope types

Discriminated by `scope.type`:

| `type`  | Fields                      | Description                                                                                                                                                           |
| ------- | --------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `order` | —                           | The discount applies to the whole order.                                                                                                                              |
| `item`  | `itemIds` (array of string) | The discount applies only to the specific basket item(s) matching this coupon's configured PLU(s), identified by the `id`s you passed in the request's `order.items`. |

### ValidationError object

| Field     | Type   | Description                                   |
| --------- | ------ | --------------------------------------------- |
| `code`    | string | Machine-readable error code. See table below. |
| `message` | string | Human-readable explanation.                   |

| `code`                              | Meaning                                                                           |
| ----------------------------------- | --------------------------------------------------------------------------------- |
| `coupon_not_found`                  | No coupon exists for this code on the account.                                    |
| `max_uses_per_coupon_exceeded`      | The coupon has reached its maximum number of uses.                                |
| `coupon_not_available_for_location` | The coupon isn't configured for the order's location.                             |
| `not_eligible_fulfillment_type`     | The coupon doesn't support the order's fulfillment type (delivery/pickup/eat-in). |
| `coupon_not_valid_for_channel`      | The coupon isn't configured for the order's channel.                              |
| `coupon_not_valid_for_channel_link` | The coupon isn't configured for this specific channel link.                       |
| `coupon_not_enabled`                | The coupon exists but is currently disabled.                                      |

### Example response

```json
[
  {
    "code": "SUMMER25",
    "applicable": true,
    "discounts": [
      {
        "offer": {
          "type": "percent_off",
          "value": 2500,
          "maxAmount": 3000
        },
        "scope": {
          "type": "order"
        },
        "provider": "coupon",
        "externalId": "SUMMER25",
        "name": "Summer 25% off"
      }
    ],
    "description": "25% off your order, up to $30",
    "validationErrors": []
  },
  {
    "code": "INVALIDCODE",
    "applicable": false,
    "discounts": [],
    "description": "",
    "validationErrors": [
      {
        "code": "coupon_not_found",
        "message": "coupon not found"
      }
    ]
  }
]
```

## Notes

- This endpoint does not redeem the coupon — it only validates and returns the
  applicable discount(s). Redemption happens separately at checkout.
