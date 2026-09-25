---
title: Webhooks
deprecated: false
hidden: false
icon: fad fa-webhook
metadata:
  robots: index
---
<br />

<HMACAuthentication />

<br />

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        WEBHOOK
      </th>

      <th>
        TYPE
      </th>

      <th>
        FUNCTION
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        [Channel Registration](ref:channel_register)
      </td>

      <td>
        <POST_LABEL />
      </td>

      <td>
        Any channel integrator will provide a standardised registration URL to facilitate customer onboarding/offboarding.
      </td>
    </tr>

    <tr>
      <td>
        [Checkout Update](ref:post_checkout-update)
      </td>

      <td>
        <POST_LABEL />
      </td>

      <td>
        Triggered after a customer completes checkout. Sends the final basket and checkout status to your endpoint.
      </td>
    </tr>

    <tr>
      <td>
        [Menu Update](ref:channel_menu_update)
      </td>

      <td>
        <POST_LABEL />
      </td>

      <td>
        Customers will publish their menu to a provided webhook URL. This delivers JSON containing all the necessary attributes to display their menu as intended.
      </td>
    </tr>

    <tr>
      <td>
        [Snooze / Unsnooze Products](ref:channel_snooze)
      </td>

      <td>
        <POST_LABEL />
      </td>

      <td>
        When items are out of stock or temporarily unavailable, a snooze event is sent to instruct channels to make items unavailable. When items become available again, an unsnooze event is sent.
      </td>
    </tr>

    <tr>
      <td>
        [Busy mode](ref:busy-mode)
      </td>

      <td>
        <POST_LABEL />
      </td>

      <td>
        When a store is paused, a webhook event is sent to ensure no further orders can be received. When re-opened, an event is sent to set the store back online.
      </td>
    </tr>

    <tr>
      <td>
        [Courier Update](ref:courier-update-webhook)
      </td>

      <td>
        <POST_LABEL />
      </td>

      <td>
        Courier-related updates are sent to provide new information about the courier journey whenever a change applies.
      </td>
    </tr>

    <tr>
      <td>
        [Order Status Update](ref:channel_order_status)
      </td>

      <td>
        <POST_LABEL />
      </td>

      <td>
        Whenever a POS updates the status of an order, a webhook event is sent with the updated order details.
      </td>
    </tr>

    <tr>
      <td>
        [Preparation Time Update](ref:channel_prep_time)
      </td>

      <td>
        <POST_LABEL />
      </td>

      <td>
        A webhook is sent to indicate that a preparation time update for an order has been applied.
      </td>
    </tr>
  </tbody>
</Table>

<br />

<br />
