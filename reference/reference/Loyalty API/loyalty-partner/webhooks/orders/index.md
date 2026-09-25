---
title: Loyalty Orders
deprecated: false
hidden: false
icon: fad fa-receipt
metadata:
  robots: index
---
## Webhooks

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        Webhook
      </th>

      <th>
        Method
      </th>

      <th>
        Purpose
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        [Loyalty Order Notification](ref:loyalty-partner-order)
      </td>

      <td>
        <POST_LABEL />
      </td>

      <td>
        Triggered when an order is made. Deliverect sends the order details to the configured endpoint, enabling the loyalty provider to perform relevant loyalty operations, such as awarding points and deducting redeemed points.
      </td>
    </tr>

    <tr>
      <td>
        [Cancel Loyalty Order](ref:loyalty-partner-cancel-order)
      </td>

      <td>
        <POST_LABEL />
      </td>

      <td>
        When an order is cancelled. Deliverect sends an event to the configured endpoint, including the key order identifier `"orderId"` along with a cancellation reason where provided. This enables the Loyalty platform  to perform relevant follow-up actions, such as reversing awarded loyalty points or reinstating redeemed points.
      </td>
    </tr>
  </tbody>
</Table>
