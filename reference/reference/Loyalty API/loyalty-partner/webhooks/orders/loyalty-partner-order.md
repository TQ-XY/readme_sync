---
api:
  file: loyalty_webhooks.json
  operationId: loyalty_order
hidden: false
---
## Purpose

This webhook event is triggered when an order is made. Deliverect sends the order details to the configured endpoint, enabling the loyalty provider to perform relevant loyalty operations, such as awarding points and deducting redeemed points.

### Order Schema

For a full list of all order attributes and their definition, see the link below;

<HTMLBlock>{`
<a href="https://developers.deliverect.com/page/loyalty-order-schema" target="_blank" class="doc-button">▶ Loyalty Order Model</a>
`}</HTMLBlock>