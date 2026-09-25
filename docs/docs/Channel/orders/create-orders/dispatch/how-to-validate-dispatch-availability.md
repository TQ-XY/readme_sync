---
title: How to validate dispatch availability
deprecated: false
hidden: false
metadata:
  robots: index
---
## Introduction

Use the Dispatch Availability endpoint to verify whether a dispatch partner can perform a delivery before you submit an order. This guide provides information on activating dispatch, validating dispatch partner availability, and effectively using the obtained `validationId` to submit orders.

## Activate and Configuring Dispatch

Before utilizing the **Dispatch Availability** endpoint, it's essential to ensure that dispatch is activated and correctly configured for your channel integration. We can set up a mock dispatch configuration for testing in our staging environment.

If you plan to implement this endpoint, contact our API team at [integrations-support@deliverect.com](mailto:integrations-support@deliverect.com) to configure this for your staging account.

## Validate dispatch partner availability

1. Send a POST request to the validation endpoint.
2. Include the required request information:
   - <Glossary>channelLinkId</Glossary>
   - Delivery location details, including delivery time, package size, customer information, and coordinates, if available.

```json Validate Dispatch Availability

{
  "channelLinkId": "62********************7c",
  "deliveryLocations": {
    "deliveryTime": "2023-05-17T10:00:00Z",
    "packageSize": "unknown",
    "name": "customer name",
    "source": "customer address",
    "street": "customer street and number",
    "postalCode": "postal code",
    "phone": "+111111111",
    "coordinates": {
      "coordinates": [
        -113,
        53
      ]
    }
  }
}
```

## Handle the validation request

A successful validation response includes:

- An `available` flag set to `true`, which means a dispatch partner is available for the specified delivery.
- A `validationId` to set within the order creation process (valid for 10 minutes)

```json Success response
{
  "validationId": "62********************7c",
  "available": true,
  "expiresAt": "YYYYY-MM-DDTHH:mm:ss.SSSSSSZ",
  "deliveryTimeETA": "YYYYY-MM-DDTHH:mm:ss.SSSSSSZ",
  "pickupTimeEta": "YYYYY-MM-DDTHH:mm:ss.SSSSSSZ",
  "price": 0
}
```

## Use the `validationId` for order creation

When you submit an order through our [Create Order API,](https://developers.deliverect.com/v3.0-ordering-experience/reference/create-channel-order) include the `validationId` in the request payload.

<HTMLBlock>{`
<div class="callout-banner callout-banner--important">
  <span class="callout-icon"><i class="fa-regular fa-triangle-exclamation"></i></span>
  <p><strong>Location Updates</strong><br>
On order creation, if a <code>validationId</code> is supplied it will be ignored, as the pre-validated address submitted in the <a href="https://developers.deliverect.com/v3.0-ordering-experience/reference/post_fulfillment-validate">Dispatch Availability</a> request will be used</p>
</div>
`}</HTMLBlock>
