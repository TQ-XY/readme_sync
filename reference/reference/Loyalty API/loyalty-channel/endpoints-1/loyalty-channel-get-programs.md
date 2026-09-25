---
api:
  file: loyalty-api.json
  operationId: post_loyalty-channellinkid-programs-retrieve
hidden: false
link:
  new_tab: false
metadata:
  robots: index
---
## Purpose

This endpoint allows channels to retrieve a list of loyalty programs available to a customer. It supports two different use cases, each requiring a different level of detail in the request payload.

### Request Schema and Structure

| Field                                              | Type               | Required | Description                                                                                                                                                                                                                                                                                        |
| :------------------------------------------------- | :----------------- | :------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `sessionId`                                        | `string`           | Yes      | A unique session identifier, reused across the Get Programs, Validate Programs, and Create Order calls.                                                                                                                                                                                            |
| `order`                                            | `object`           | Yes      | The order payload.                                                                                                                                                                                                                                                                                 |
| `order.customer`                                   | `object`           | Yes      | The customer's details.                                                                                                                                                                                                                                                                            |
| `order.customer.name`                              | `string`           | No       | The customer's full name.                                                                                                                                                                                                                                                                          |
| `order.customer.email`                             | `string`           | No       | The customer's email address.                                                                                                                                                                                                                                                                      |
| `order.customer.phoneNumber`                       | `string`           | No       | The customer's phone number (E.164 standard).                                                                                                                                                                                                                                                      |
| `order.customer.`<br />`loyaltyProviderCustomerId` | `string`           | Yes      | The customer's unique ID from the loyalty provider.                                                                                                                                                                                                                                                |
| `order.orderType`                                  | `integer`          | Yes      | The type of order.<ul><li>1 – Pickup</li><li>2 – Delivery</li><li>3 – Eat In</li><li>4 – Curbside</li><li>5 – Drive Thru</li></ul>Any other value — including an omitted field — resolves to Unknown, which this endpoint rejects with a 422 invalid_order_type error (see Error Responses below). |
| `order.items`                                      | `array of objects` | No       | The order’s line items. Empty for a customer-only call; populated with the full basket when sending items — see the Order Model below for the item schema.                                                                                                                                         |

### Order Model

For more information on the order schema, see the link below;

<HTMLBlock>{`
<a href="https://developers.deliverect.com/page/glossary-channel-orders" target="_blank" class="doc-button">▶ Order Model</a>
`}</HTMLBlock>

### Response Schema and Structure

| Field             | Type                | Required | Description                                                                                                                                                                                                                                         |
| :---------------- | :------------------ | :------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `programId`       | `string`            | Yes      | The unique identifier of the loyalty program.                                                                                                                                                                                                       |
| `title`           | `string`            | Yes      | The title or display name of the program.                                                                                                                                                                                                           |
| `type`            | `string` (enum)     | Yes      | The type of the loyalty program.<ul><li>discount_amount</li><li>discount_percentage</li><li>free_item</li><li>buy_one_get_one_free</li><li>item_discount_amount</li><li>item_discount_percentage</li><li>item_fixed_price</li><li>unknown</li></ul> |
| `applicable`      | `boolean`           | No       | Indicates if the customer meets the basic requirements for this program. Default is true. This is a best-effort estimate from the loyalty partner — call [Validate Programs](ref:loyalty-channel-validate-programs) for an authoritative check.     |
| `description`     | `string`            | No       | A description of the loyalty program.                                                                                                                                                                                                               |
| `cost`            | `number`            | No       | The cost of the program in the loyalty provider’s points (not currency), e.g., the number of points to redeem.                                                                                                                                      |
| `media`           | `object`            | No       | Media assets associated with the program, such as an image or icon.                                                                                                                                                                                 |
| `media.mediaType` | `string`            | Yes      | Values may be: `image` / `video`                                                                                                                                                                                                                    |
| `media.url`       | `string`            | Yes      | The url of the resource                                                                                                                                                                                                                             |
| `expiresAt`       | `string` (ISO 8601) | No       | The expiration date and time of the program.                                                                                                                                                                                                        |
| `discount`        | `number`            | No       | The specific discount value, in the smallest unit of the order’s currency (e.g., cents).                                                                                                                                                            |
| `itemPLU`         | `string`            | No       | The PLU of the item to which the program applies.                                                                                                                                                                                                   |
| `quantity`        | `number`            | No       | The quantity of items affected by the program.                                                                                                                                                                                                      |
| `minOrderValue`   | `number`            | No       | The minimum order value required for this program to be applicable, in the smallest unit of the order’s currency (e.g., cents).                                                                                                                     |

### Usage

- Customer only — the minimum required call: send order.customer with order.items empty. This lists every program the customer can access, but since no basket is sent to the loyalty partner, applicability can’t be evaluated accurately.
- Customer + basket (recommended) — send the full order payload (items, payment, discounts). This is forwarded to the loyalty partner so they can determine which programs actually apply to that basket.<br /><br />

The request and response shapes are otherwise identical between the two — only how much of order you populate changes.

Applicability here is a best-effort estimate from the loyalty partner and isn’t guaranteed — it can depend on factors this endpoint doesn’t have full visibility into. Before charging or redeeming a program, call [Validate Programs](https://developers.deliverect.com/v3.0-ordering-experience/reference/loyalty-channel-validate-programs) for an authoritative applicability check.

**URL Parameters:**

- `channelLinkId` (string): The unique identifier for the channel.

**Example Request:**

```json
{
  "sessionId": "mysessionId123",
  "order": {
    "customer": {
      "name": "{{loyaltyCustomerFirstName}} {{loyaltyCustomerLastName}}",
      "email": "{{loyaltyCustomerEmail}}",
      "phoneNumber": "{{loyaltyCustomerPhone}}",
      "loyaltyProviderCustomerId": "{{loyaltyCustomerProviderId}}"
    },
    "orderType": 2,
    "items": [
      {
        "plu": "P-TE-zxb3-2",
        "name": "Burger",
        "price": 10000,
        "quantity": 1,
        "subItems": [],
        "productType": 1
      }
    ],
    "payment": {
      "amount": 10000
    },
    "discounts": []
  }
}
```

**Response Payload:**<br />The response returns a list of all programs, with the `applicable` field indicating whether they can be applied to the basket.

**Example Response:**

```json
[
  {
    "programId": "1",
    "title": "$2 OFF",
    "type": "discount_amount",
    "applicable": true,
    "description": "",
    "cost": 10,
    "media": {
      "url": "...",
      "mediaType": "image"
    },
    "expiresAt": null,
    "discount": 200,
    "itemPLU": null,
    "quantity": null,
    "minOrderValue": 1000
  },
  {
    "programId": "2",
    "title": "Free Dessert",
    "type": "free_item",
    "applicable": false,
    "description": "Requires a minimum order value of $150.00",
    "cost": 50,
    "media": {
      "url": "...",
      "mediaType": "image"
    },
    "expiresAt": null,
    "discount": null,
    "itemPLU": null,
    "quantity": null,
    "minOrderValue": 15000
  }
]
```

In this example, the basket totals 10000 ($100.00, from order.payment.amount), which is below the 15000 ($150.00) `minOrderValue` for the “Free Dessert” program — so it comes back with applicable: false, while “$2 OFF” remains applicable.

If the customer has no accessible programs, the endpoint returns an empty array.

```json
[]
```