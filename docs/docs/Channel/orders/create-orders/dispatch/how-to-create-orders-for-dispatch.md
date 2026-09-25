---
title: How to create orders for Dispatch
deprecated: false
hidden: false
metadata:
  robots: index
---
## Overview

For platforms who don't directly handle delivery or aren't currently offering this order type, Deliverect allows for an order to be routed to an integrated 'Dispatch' service.&#x20;

## Formats

There are three ordering formats where dispatch services can be integrated;

| Format              | Description                                                                                                                                                                                                                                                                                                                       |
| ------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Commerce            | Deliverect's <Anchor target="_blank" href="https://developers.deliverect.com/v3.0/reference/commerce-api-overview">Commerce Suite</Anchor> orchestrates all aspects of the digital ordering flow, delivery jobs can be assigned to any fulfillment type '`delivery`' and where `"courier": "restaurant"` is specified in Checkout |
| Channel             | This consists of an <Anchor target="_blank" href="https://developers.deliverect.com/v3.0-ordering-experience/reference/create-channel-order">order creation endpoint</Anchor> where `"courier": "restaurant"` is specified                                                                                                        |
| Standalone Dispatch | This utilizes the same endpoint as above, but for a format where POS order injection isn't a requirement and validation on product <Glossary>PLUs</Glossary> is relaxed                                                                                                                                                           |

<HTMLBlock>{`
<div class="callout-banner callout-banner--important">
  <span class="callout-icon"><i class="fa-regular fa-triangle-exclamation"></i></span>
  <p>

   Specifying any other string than <strong>\`"restaurant"\`</strong> will signal that your channel will be fully handling delivery
  </p>
</div>
`}</HTMLBlock>

## Dispatch Flow

See a complete flow diagram of the dispatch process via the link below;

<HTMLBlock>{`
<a href="https://developers.deliverect.com/page/dispatch-sequence-diagram" target="_blank" class="doc-button">▶ Dispatch Flow</a>
`}</HTMLBlock>

### Pre-requisites

A pre-requisite for delivery orders to be routed to one of our dispatch partners, a customer needs to select one or more services to connect with. See our full list of Dispatch partners <Anchor target="_blank" href="https://www.deliverect.com/en/integrations/fulfilment">here</Anchor>

## Create Order for Dispatch

```json Commerce - Checkout
{
  "basket": {
    "id": "62********************3x"
  },
  "order": {
    "channelOrderId": "TEST****629",
    "channelOrderDisplayId": "T**629",
    "validationId": null,
    "courier": "restaurant",
    "by": "Mobile App"
  },
  "note": "ORDER LEVEL NOTE",
  "payments": [
    {
      "type": "dpay",
      "externalId": "68****************44",
      "isPrepaid": true,
      "amount": 900
    }
  ]
}
```
```json Channel - Create Order
{
    "items": [
        {
            "plu": "BRG-0398",
            "name": "Burger",
            "price": 1500,
            "quantity": 1,
            "subItems": [],
            "productType": 1
        }
    ],
    "courier": "restaurant",
    "orderType": 2,
    "deliveryAddress": {
        "street": "Brown Street",
        "streetNumber": "900",
        "postalCode": "1120",
        "city": "New York",
        "extraAddressInfo": "Use Buzzer"
    },
    "deliveryCost": 0,
    "deliveryIsAsap": true,
    "deliveryTime": "yyyy-MM-ddTHH:mm:ssZ",
    "tip": 0,
    "channelOrderId": "501-bffe-f0e97",
    "channelOrderDisplayId": "f0e97"
}
```
```json Standalone Dispatch - Create Order
{
    "items": [
        {
            "plu": "1234",
            "name": "Burger",
            "price": 1500,
            "quantity": 1,
            "subItems": [],
            "productType": 1
        }
    ],
    "courier": "restaurant",
    "orderType": 2,
    "deliveryAddress": {
        "street": "Brown Street",
        "streetNumber": "900",
        "postalCode": "1120",
        "city": "New York",
        "extraAddressInfo": "Use Buzzer"
    },
    "deliveryCost": 0,
    "deliveryIsAsap": true,
    "deliveryTime": "yyyy-MM-ddTHH:mm:ssZ",
    "tip": 0,
    "channelOrderId": "501-bffe-f0e97",
    "channelOrderDisplayId": "f0e97"
}
```

## Pre-validating Dispatch Availability

To enhance the ordering flow and customer experience it is possible to check that an integrated Dispatch service is available before processing an order. The endpoint below can be used to validate Dispatch availability before submitting your order.

<HTMLBlock>{`
<a href="https://developers.deliverect.com/v3.0-ordering-experience/reference/post_fulfillment-validate" target="_blank" class="doc-button">▶ Dispatch Availability</a>
`}</HTMLBlock>

## Receiving Courier Updates

Once an order is submitted, a webhook can be delivered when various courier-related events occur. These cover the following scenarios;

<HTMLBlock>{`
<div class="step-list step-list--dots">
  <div class="step-list-item">
    <div class="step-list-marker step-list-marker--dot"></div>
    <div class="step-list-content">
      <p class="step-list-desc">The status change for the order</p>
    </div>
  </div>
  <div class="step-list-item">
    <div class="step-list-marker step-list-marker--dot"></div>
    <div class="step-list-content">
      <p class="step-list-desc">Co-ordinates updated</p>
    </div>
  </div>
  <div class="step-list-item">
    <div class="step-list-marker step-list-marker--dot"></div>
    <div class="step-list-content">
      <p class="step-list-desc">The <code>deliveryTimeETA</code> changes by greater than 60 seconds</p>
    </div>
  </div>
  <div class="step-list-item">
    <div class="step-list-marker step-list-marker--dot"></div>
    <div class="step-list-content">
      <p class="step-list-desc">Courier name changes</p>
    </div>
  </div>
</div>
`}</HTMLBlock>

See more about receiving courier updates below;

<HTMLBlock>{`
<a href="https://developers.deliverect.com/v3.0-ordering-experience/reference/courier-update-webhook" target="_blank" class="doc-button">▶ Courier Update Webhook</a>
`}</HTMLBlock>

### Package sizes & Transport types

It is optional to also specify the package sizes and transport types which will be sent using the format below.

```json
"deliveryInfo": {
        "packageSize": "large",
        "transportType": "car"
 }
```

| Package Size Name | String Value | Dimensions                   | Description                                                                         |
| :---------------- | :----------- | :--------------------------- | :---------------------------------------------------------------------------------- |
| SMALL             | small        | 22 x 42 x 45 cm              | Standard delivery with a Courier on a bicycle or scooter.                           |
| LARGE             | large        | 30 x 124 x 80 cm             | Delivery which will require to be delivered via car                                 |
| EXTRA LARGE       | extraLarge   | Larger than 30 x 124 x 80 cm | For large catering orders with many different trays to be delivered requiring a van |

| Transport Type Name | String Value |
| :------------------ | :----------- |
| BICYCLE             | bicycle      |
| CARGOBIKE           | cargobike    |
| MOTORBIKE           | motorbike    |
| MOTORBIKE XL        | motorbikexl  |
| CAR                 | car          |
