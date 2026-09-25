---
api:
  file: channel.json
  operationId: post_channelname-order-channellinkid
hidden: false
link:
  new_tab: false
---
## Purpose

A channel integration can use this endpoint to place a new order or process a cancellation of an existing order.

## Payments

Details on processing discounts, payments, taxes or other charges in the guide below;

<HTMLBlock>{`
<a href="https://developers.deliverect.com/v3.0-ordering-experience/docs/payments" target="_blank" class="doc-button">▶ Payments, Discounts, Taxes etc.</a>
`}</HTMLBlock>

## Create Orders for Dispatch / Last Mile Fulfillment

For platforms who don't directly handle delivery or aren't currently offering this order type, Deliverect allows for an order to be routed to an integrated 'Dispatch' service.

### Standalone Dispatch Integration

Our Dispatch functionality can also be integrated as a “Standalone” solution, enabling full courier assignment and delivery, whilst bypassing requirements for POS order injection i.e. product validation. This format supports several use cases such as;

- First-party ordering platforms which already integrates to a customer POS via an existing direct integration
- Phone orders entered directly into a POS requiring delivery

For details on handling dispatch orders, see guide below;

<HTMLBlock>{`
<a href="https://developers.deliverect.com/v3.0-ordering-experience/docs/how-to-create-orders-for-dispatch" target="_blank" class="doc-button">▶ Create Orders for Dispatch</a>
`}</HTMLBlock>

## Channel Cancelations

Your channel integration can process a cancellation using the same endpoint used create a new order

Sending a secondary order with the same `channelOrderId` and `"status": 100` (Cancel) will initiate a POS cancellation request which typically involves 'voiding' the order.

Once the cancellation is processed by the POS, a status `CANCELED` (110) will be returned to confirm this has been handled.

<HTMLBlock>{`
<div class="callout-banner callout-banner--important">
  <span class="callout-icon"><i class="fa-regular fa-triangle-exclamation"></i></span>
  <p>
    <strong>Cancelling Already Accepted Orders</strong><br>
   <strong>NB:</strong> There is no validation in Deliverect to prevent cancellation requests based on the current order status.
  </p>
</div>
`}</HTMLBlock>

<HTMLBlock>{`
<div class="callout-banner callout-banner--important">
  <span class="callout-icon"><i class="fa-regular fa-triangle-exclamation"></i></span>
  <p>
    <strong>Order Response</strong><br>
   All orders sent in a valid format with the correct scope applied will receive a <code>201</code>.
    This does not indicate that the POS has successfully processed the order. You should reference the events sent to your
    <a href="https://developers.deliverect.com/v3.0-ordering-experience/reference/channel_order_status" style="color: #b71c1c; font-weight: 600; text-decoration: underline;">

      Order Status Update
    </a>
    webhook to confirm whether the order was successfully processed.
  </p>
</div>
`}</HTMLBlock>