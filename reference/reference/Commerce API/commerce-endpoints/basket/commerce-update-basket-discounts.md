---
api:
  file: commerce.json
  operationId: commerce-channel-api-baskets-update-basket-discounts
hidden: false
link:
  new_tab: false
next:
  pages:
    - slug: loyalty-channel-get-programs
      title: Get Loyalty Programs
      type: endpoint
    - slug: get-coupons
      title: Get Coupons
      type: endpoint
    - slug: validate-basket
      title: Validate Basket
      type: endpoint
---
## Overview

Apply discounts to perform a recalculation of basket totals based on the specified discount `type` and `value`. Baskets can also be updated with additional items when discount types like `item_bogof` or `item_free`are specified. The response returns an updated `discountsTotal` along with itemised `discountTotal` for item level discounts to ensure detailed reporting.

### Commerce Discount Types

The following table describes the supported discount types and the equivalent value to map to when retrieving info via loyalty API via [Get Loyalty Programs](ref:loyalty-channel-get-programs)

| Commerce Discount Type | Loyalty Program Type       | Description                                                                                                                            |
| ---------------------- | -------------------------- | :------------------------------------------------------------------------------------------------------------------------------------- |
| `order_percent_off`    | `discount_percentage`      | Percentage discount applied to the subtotal of the order.                                                                              |
| `order_flat_off`       | `discount_amount`          | Fixed amount discount applied to the subtotal of the order                                                                             |
| `item_bogof`           | `buy_one_get_one_free`     | Buy one get one free promotion on specific items.                                                                                      |
| `item_free`            | `free_item`                | A specific item is provided free of charge.                                                                                            |
| `item_percent_off`     | `item_discount_percentage` | Percentage discount applied to a specific item.                                                                                        |
| `item_flat_off`        | `item_discount_amount`     | Fixed amount discount applied to a specific item.                                                                                      |
| `wallet_cash`          | \-                         | Discount funded by a user's digital wallet balance.                                                                                    |
| `compensation_card`    | `compensation_card`        | Discount applied via a compensation card                                                                                               |
| \-                     | `item_fixed_price`         | Item is sold at a fixed price. The channel must calculate the discount amount and add it to the commerce basket as an `item_flat_off.` |

### Available Providers

| Provider     | Description                                                                                              |
| :----------- | :------------------------------------------------------------------------------------------------------- |
| `restaurant` | Used when the discount is provided by the restaurant                                                     |
| `coupon`     | Used when the discount is applied via a coupon code returned via our [Coupons API](ref:coupons-overview) |
| `loyalty`    | Used when a discount is applied which is retrieved via our [Loyalty Channel API](ref:loyalty-channel)    |

### Loyalty provider

<HTMLBlock>{`
<div class="callout-banner callout-banner--neutral">
  <span class="callout-icon"><i class="fa-regular fa-square-info"></i></span>
  <p>

    Where using
    <a href="https://developers.deliverect.com/v3.0-ordering-experience/reference/loyalty-channel-get-programs">GET /programs</a>,
    the <code>programId</code> returned is the unique identifier of a specific program
    and should be specified as the <code>externalId</code> in the PATCH body.
  </p>
</div>
`}</HTMLBlock>

```json item_flat_off
[
  {
    "type": "item_flat_off",
    "provider": "loyalty",
    "externalId": "discount-item-flat-123",
    "name": "Item flat off: $5",
    "menuId": "668f7ff64dc853**c96**877",
    "value": 5000,
    "itemIds": [
      "6900f2f01306779be71e7b8e"
    ]
  }
]
```
```json order_percent_off
[
  {
    "type": "order_percent_off",
    "provider": "restaurant",
    "value": 1000,
    "name": "CONGRATS10% OFF"
  }
]
```
```json order_flat_off
[
  {
    "type": "order_flat_off",
    "provider": "coupon",
    "amount": 100,
    "name": "CONGRATS! HERE IS 1 EUR OFF"
  }
]
```
```json order_percent_off
[
  {
    "type": "order_percent_off",
    "provider": "restaurant",
    "value": 1000,
    "name": "CONGRATS10% OFF"
  }
]
```
```json item_free
[
  {
    "provider": "restaurant",
    "name": "Free coke",
    "type": "item_free",
    "plu": "DLX-3",
    "menuId": "69d4c198e1c58591f461cb4a",
    "externalId": "discount-123"
  }
]
```
```json item_bogof
[
  {
    "provider": "restaurant",
    "name": "",
    "type": "item_bogof",
    "plu": "DLX-3",
    "menuId": "69d4c198e1c58591f461cb4a",
    "externalId": "discount-bogo"
  }
]
```
```json item_percent_of
[
  {
    "type": "item_percent_off",
    "provider": "restaurant",
    "externalId": "discount-123",
    "name": "Item percent off: 25%",
    "menuId": "69d4c198e1c58591f461cb4a",
    "value": 2500,
    "itemIds": [
      "6900f2f01306779be71e7b8e"
    ]
  }
]
```
```json wallet_cash
[
  {
    "type": "wallet_cash",
    "value": 1000,
    "provider": "loyalty",
    "externalId": null
  }
]
```
```json compensation_card
[
  {
    "type": "compensation_card",
    "provider": "restaurant",
    "externalId": "cardnumber-123",
    "value": 5000,
    "name": "Compensation card for $5"
  }
]
```