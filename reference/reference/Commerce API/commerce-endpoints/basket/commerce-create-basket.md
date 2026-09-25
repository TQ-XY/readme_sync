---
api:
  file: commerce.json
  operationId: post_commerce-accountid-baskets
hidden: false
link:
  new_tab: false
---
## Purpose

Creates a Basket for a specified store to validate content, if successfully validated, an `id` is returned that will be used when proceeding to [Checkout Basket](ref:checkout)

<HTMLBlock>{`
<div class="callout-banner callout-banner--neutral">
  <span class="callout-icon"><i class="fa-regular fa-square-info"></i></span>
  <p>
    <strong>Basket Ids Expiry</strong><br>
    Basket IDs become invalid once they are used in a completed checkout. If they are not used, they will remain valid for up to 45 days.
  </p>
</div>
`}</HTMLBlock>

## Fulfilment types

| Type        | Definition                                                                    |
| :---------- | :---------------------------------------------------------------------------- |
| `delivery`  | For delivery orders (including those handled by 3rd party dispatch platforms) |
| `pickup`    | Will be collected i.e. for takeaway (can apply for Kiosk orders)              |
| `curbside`  | Will be as per pickup, but specific handoff to customer in vehicle            |
| `eatIn`     | Customer will be ordering on-premise e.g. QR Code ordering                    |
| `driveThru` | Customers will be submitting an order in a drive-thru format                  |

## Basket Items

A basket can be first created without items and updated later via [Update Basket - Item(s)](ref:update-basket-items) Below are examples showing the minimum requirements for an initial basket to be created per fulfilment type:

```json Delivery
{
    "channelLinkId": "67********************2c",
    "fulfillment": {
        "type": "delivery"
    }
}
```
```json Pickup
{
    "channelLinkId": "67********************2c",
    "fulfillment": {
        "type": "pickup",
        "pickupNotes": "Yellow Honda"
    }
}
```
```json Curbside
{
    "channelLinkId": "67********************2c",
    "fulfillment": {
        "type": "curbside",
        "pickupNotes": "Yellow Honda"
    }
}
```
```json Eat-In
{
    "channelLinkId": "67********************2c",
    "fulfillment": {
        "type": "eatIn",
        "spot": "table-5"
    }
}
```

## Basket Validation

The combination of `storeId` and a valid `menuId` will provide the required reference to validate basket items in the following criteria;

- Items are available and valid for the "`fulfillment.type`" specified.
- Item selections comply with menu rules, e.g, minimum and maximum values
- Requested times fall within store operating hours
- Fulfilment type specified is offered by the store

## Pre-defined charges

Extra charges can be applied automatically if configured in Deliverect.

| Charge         | Definition                                          |
| :------------- | :-------------------------------------------------- |
| Delivery Fee   | Cost of delivery payable by the customer            |
| Service Charge | Any additional charges levied e.g. transaction fees |
| Bag Fee        | Unique charge for provision of packaging for orders |

## Tax Calculation

In certain 'Tax Exclusive' regions e.g. US/Canada, the complete calculate tax totals can be serviced via the integrated POS. This will be factored into `"payment.total"` and a specific breakdown of tax code will be returned within `"taxes": []`&#x20;

<HTMLBlock>{`
<div class="callout-banner callout-banner--neutral">
  <span class="callout-icon"><i class="fa-regular fa-square-info"></i></span>
  <p>
    <strong>Enquire for Specific POS Support</strong><br>
Tax calculation is supported by most major POS integrations, but availability depends on the capabilities of each POS. Enquire with your Deliverect contact to confirm support for your specific POS.
  </p>
</div>
`}</HTMLBlock>

```json Tax Calculation Example
"payment": {
  "tips": [],
  "donationTotal": 0,
  "discountsTotal": 0,
  "chargesTotal": 0,
  "taxTotal": 43,
  "tipTotal": 0,
  "subTotal": 618,
  "total": 661
},
"taxes": [
  {
    "name": "GST",
    "amount": 43
  }
]
```

## Group Basket

#### **To support group ordering, a l**ist of customers participating in a group order can be submitted, see the guide below for further information on the group ordering format.

<HTMLBlock>{`
<a href="https://developers.deliverect.com/v3.0-ordering-experience/docs/how-to-create-a-group-order" target="_blank" class="doc-button">▶ Group ordering</a>
`}</HTMLBlock>