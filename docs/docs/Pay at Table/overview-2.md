---
title: Overview
deprecated: false
hidden: true
icon: fad fa-book-open-lines
metadata:
  robots: index
---
Use the Deliverect Dine-In Payment API endpoints to support payment fulfillment for dine-in orders.

These endpoints are being prepared to support **Deliverect Dine-In Payment**. They are not complete documentation for the [Deliverect API](https://developers.deliverect.com/reference/get-started).

Dine-In Payment lets API partners fulfill payment for an order. The order can be created through Deliverect or directly in the POS, depending on the capabilities of each underlying POS.

## Prerequisites

1. Set up a Payment Channel Link by following [Activating Channels](https://developers.deliverect.com/docs/how-do-i-activate-my-channel).
2. Use [POST Channel Status](https://developers.deliverect.com/reference/post-channel-status) to receive the `channelLink` ID and location ID.
3. Authenticate requests using the same rules described in [Public API Documentation](https://developers.deliverect.com/reference/machine-2-machine-access-token).

<Callout icon="far fa-triangle-exclamation" theme="warning">
  This API is a work in progress. Breaking changes might still occur, and not all POS integrations already support these endpoints. Contact the API team for details about supported POS integrations.
</Callout>

## API scope

These endpoints are not related to the [getReceipt endpoint](https://developers.deliverect.com/reference/get-receipt-from-pos), which was scheduled for deprecation in early 2022.

## Tags

- `orders`: Operations related to orders
- `receipts`: Operations related to receipts
- `tables`: Operations related to tables

## Paths

Send a payment for a Deliverect order:

```http
POST /channellinks/{clId}/orders/{channelOrderId}/payments
```
