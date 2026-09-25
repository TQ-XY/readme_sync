---
api:
  file: fulfilment.json
  operationId: refunds
hidden: true
---
## Purpose

This endpoint can be called to communicate a refund.

## HMAC - Headers

| Key              | Value                                                                                                                             |
| :--------------- | :-------------------------------------------------------------------------------------------------------------------------------- |
| Content-type     | application/json                                                                                                                  |
| X-HMAC-Signature | With every call made to this endpoint, the HMAC signature should uses the SHA256 cryptographic hash function with base64 encoding |
| X-HMAC-Partner   | This is a pre-shared by Deliverect value to identify the partner                                                                  |

## Refund Types

This indicates whether the refund is for the full basket value or for a partial amount on the order.

| Type | Integer value |
| :--- | :------------ |
| Full | `1`           |
| Item | `2`           |
| Flat | `3`           |

<HTMLBlock>{`
<div class="callout-banner callout-banner--neutral">
  <span class="callout-icon"><i class="fa-regular fa-square-info"></i></span>
  <p>
   If sending a refund event for just delivery fees, use "Item" Type <code>2</code>
  </p>
</div>
`}</HTMLBlock>

<br />

## Refund Owner

This indicates who is ultimately responsible to fund the cost of the refund.

| Owner            | Integer Value |
| :--------------- | :------------ |
| Restaurant       | 1             |
| Delivery Service | 2             |
| Shared           | 3             |

## Refund reason

| Reason                | Description                                                            |
| :-------------------- | :--------------------------------------------------------------------- |
| ORDER_MISSING_ITEMS   | Items are missing on the order.                                        |
| ORDER_ITEM_ERROR      | Error with some of the items on the order.                             |
| ORDER_FOOD_QUALITY    | The food quality was compromised.                                      |
| OTHER                 | If using this reason, please provide "extraInfo" to detail the problem |
| ORDER_LATE_DELIVERY   | The order arrived late.                                                |
| ORDER_NEVER_DELIVERED | The order was not delivered.                                           |
| WRONG_ORDER_DELIVERED | A wrong order was delivered.                                           |
| DRIVER_DAMAGE         | Driver has damaged the order                                           |
| ORDER_DAMAGED         | Order was damaged                                                      |

```json Example Item Request
{
    "externalJobId": "67d89438a697346d7752a71a",
    "deliveryRefundDetails": {
        "type": 2,
        "owner": 1,
        "totalRestaurantAmount": 200,
        "totalDspAmount":0,
        "reason": "INCORRECT_ORDER_TO_CUSTOMER",
        "extraInfo": "Contained mayo and asked for no mayo"
    },
    "deliveryRefundItemDetails": [ 
        {
            "itemName": "Big Burger",
            "itemPLU": "abc-123",
            "quantity": 1,
            "reason": "INCORRECT_ORDER_TO_CUSTOMER",
            "amount": 200,
            "percentage": 25,
            "owner": 1
        }
    ],
    "deliveryRefundFeeDetails": [ 
    {
        "amount": 200,
        "owner": 2
    }
]
}

```
```json Example Flat Request
{
  "externalJobId": "67d89438a697346d7**2a71a",
  "deliveryRefundDetails": {
    "type": 3,
    "owner": 1,
    "totalRestaurantAmount": 0,
    "totalDspAmount": 0,
    "reason": "string",
    "extraInfo": "string"
  },
  "deliveryRefundFeeDetails": [
    {
      "amount": 0,
      "owner": 1
    }
  ]
}
```
