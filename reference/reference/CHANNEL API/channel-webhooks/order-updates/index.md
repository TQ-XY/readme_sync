---
title: Order Updates
deprecated: false
hidden: false
metadata:
  robots: index
---
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
        [Payment Update](ref:payment-update-webhook)
      </td>

      <td>
        <POST_LABEL />
      </td>

      <td>
        A webhook is sent to indicate that a preparation time update for an order has been applied.
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
        [Courier Update](ref:courier-update-webhook)
      </td>

      <td>
        <POST_LABEL />
      </td>

      <td>
        Courier-related updates are sent to provide new information about the courier journey whenever a change applies.
      </td>
    </tr>
  </tbody>
</Table>

## Retail Updates

Below webhooks are available to channels working with retail clients who manage the order picking process;

<HTMLBlock>{`
<div class="callout-banner callout-banner--note">
  <span class="callout-icon"><i class="fa-duotone fa-solid fa-lightbulb"></i></span>
  <p>
    <strong>Retail Webhooks</strong><br>
    Picking related webhook events available via our
    <a href="https://developers.deliverect.com/v2.0-retail/reference/retail-channel-webhooks" target="_blank" style="color: #1b5e20; font-weight: 600; text-decoration: underline;">Retail API</a>
  </p>
</div>
`}</HTMLBlock>

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
        **Picking Status Update**<Anchor target="_blank" href="https://developers.deliverect.com/v2.0-retail/reference/picking-status-update"> 🔗</Anchor>
      </td>

      <td>
        <POST_LABEL />
      </td>

      <td>
        When a store process order picking status updates, this webhook can be set to receive these events
      </td>
    </tr>

    <tr>
      <td>
        **Amendments**<Anchor target="_blank" href="https://developers.deliverect.com/v2.0-retail/reference/picking-amendments"> 🔗</Anchor>
      </td>

      <td>
        <POST_LABEL />
      </td>

      <td>
        When a store processes amendments for one or more items within an order, this webhook will deliver the amendment details
      </td>
    </tr>

    <tr>
      <td>
        **Substitutes**<Anchor target="_blank" href="https://developers.deliverect.com/v2.0-retail/reference/picking-substitutes"> 🔗</Anchor>
      </td>

      <td>
        <GET_LABEL />
      </td>

      <td>
        This is a GET webhook provided by the channel, which returns valid substitute item PLUs for any requested substitution
      </td>
    </tr>
  </tbody>
</Table>
