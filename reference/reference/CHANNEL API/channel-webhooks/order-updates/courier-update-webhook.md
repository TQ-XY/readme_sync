---
api:
  file: channel_webhooks.json
  operationId: channel_courier_update
hidden: false
---
## Purpose

This webhook delivers real-time updates on each delivery job, based on information provided by the integrated Dispatch partner.

## Format

Webhook events are triggered based on the following conditions. Early in the delivery process, events may be infrequent but become more regular after an order is assigned. The same status enum may be sent with updated details:

- Courier co-ordinates change
- `pickupTimeETA` or `deliveryTimeETA` changes by more than 60 seconds
- Delivery status changes (e.g., DELIVERY_CREATED → EN_ROUTE_TO_PICKUP)
- A courier is reassigned

<HTMLBlock>{`
<div class="callout-banner callout-banner--neutral">
  <span class="callout-icon"><i class="fa-regular fa-square-info"></i></span>
  <p>
    <strong>Requires Integrated Dispatch</strong><br>
    A Dispatch provider needs to be integrated with a customer location for courier status updates to be received.
  </p>
</div>
`}</HTMLBlock>

## Definitions

The various attributes delivered with Courier status updates are listed in the link below;

<HTMLBlock>{`
<a href="https://developers.deliverect.com/page/courier-status-update-model" target="_blank" class="doc-button">▶ Courier Status Model</a>
`}</HTMLBlock>

## Courier Statuses

For a full list of all courier `status` values, see the link below;

<HTMLBlock>{`
<a href="https://developers.deliverect.com/page/order-status#courier-statuses" target="_blank" class="doc-button">▶ Courier Statuses</a>
`}</HTMLBlock>

### Example Courier Status Updates

```json Sample Courier Update
{
    "orderId": "651142e93c54c5405****6a3",
    "channelOrderId": "T8****28",
    "status": 87,
    "deliveryTime": "YYYY-MM-DDT08:36:46.SSSSSSZ",
    "courierName": "DRIVER NAME",
    "coordinates": {
        "coordinates": [
            -4.294259666220875,
            55.78873945318564
        ]
    },
    "courierId": "9B******HK",
    "dispatchPartner": "COURIERAPP",
    "trackingURL": "trackingURL"
}
```
```json Sample Courier Update (multiple couriers)
{
    "orderId": "651142e93c54c5405****6a3",
    "channelOrderId": "T8****29",
    "status": 87,
    "deliveryTime": "YYYY-MM-DDT08:36:46.SSSSSSZ",
    "courierName": "DRIVER NAME",
    "coordinates": {
        "coordinates": [
            -4.294259666220875,
            55.78873945318564
        ]
    },
    "courierId": "9B******HL",
    "dispatchPartner": "UBERDAAS",
    "multipleDrivers": true
}
```

<HTMLBlock>{`
<div class="callout-banner callout-banner--neutral">
  <span class="callout-icon"><i class="fa-regular fa-square-info"></i></span>
  <p>
    <strong>Tracking URL Availability</strong><br>
     A tracking URL is returned only when supported by the Dispatch provider.
  </p>
</div>
`}</HTMLBlock>

## Response format

```json 200
OK
```