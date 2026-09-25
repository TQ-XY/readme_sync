---
api:
  file: channel_webhooks.json
  operationId: channel_prep_time
hidden: false
---
## Purpose

A POS can update the preparation time for any incoming order. This is to ensure an optimal order flow in the kitchen and for delivery orders, allow for a more time-efficient procedure for couriers.

## Format

The webhook event will communicate a new `"pickupTime"` as in the example below and channel partners should ensure this is communicated to couriers as well as end-consumers.

```json
{
    "channelOrderId": "X7CESD",
    "orderId": "5e****abc11dec0001****9b",
    "location": "5e****abc11dec0001****0b",
    "status": 20,
    "pickupTime": "2021-04-20T16:20:00Z"
}
```