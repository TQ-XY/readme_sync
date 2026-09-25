---
title: How to Update an Order
deprecated: false
hidden: true
metadata:
  robots: index
---
## Why update an order during delivery?

Dispatch partners (third-party delivery providers) manage the delivery and the courier. Deliverect uses your updates to keep the user and ordering channel (the platform where the order was placed) informed about delivery progress and timing changes.

## Supported updates

You can send updates for the following delivery details:

- `status`: delivery status.
- `deliveryTimeETA`: estimated delivery time.
- `pickupTimeETA`: estimated pickup time.
- `courier`: courier name, phone number, latitude, and longitude.
- `transportType`: courier transport type.

## Submit an order update

Send updates with the [**Update Delivery** endpoint](https://developers.deliverect.com/v1.0/reference/post_fulfillment-generic-events).