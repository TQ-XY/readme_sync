---
title: How to Checkout a Basket
deprecated: false
hidden: false
metadata:
  robots: index
---
## Overview

After a basket is created, the checkout process creates an order in Deliverect, which is then sent to the customer’s POS system. The checkout flow can vary depending on the payment method used.

# Payment Methods

| Method                | Description                                                                        |
| :-------------------- | :--------------------------------------------------------------------------------- |
| Third party           | External payment provider                                                          |
| Deliverect pay - Dpay | Payment provider connected via Deliverect. The redirection happens via Deliverect. |
| Gift Card             | Gift Card provider connected via Deliverect.                                       |
| Multiple              | Combination of various methods                                                     |

## Deliverect Pay - Dpay

Deliverect customers can configure payment methods via Deliverect.  In order to checkout via DPay, the customer must have configured an **Online** payment method. Consult[ this  guide here ](https://help.deliverect.com/en/articles/7979307-deliverect-pay-configure-a-payment-gateway) on how to set up a payment gateway.&#x20;

The payment request will provide a redirection link to the payment provider to complete the transaction.

<HTMLBlock>{`
<div class="callout-banner callout-banner--neutral">
  <span class="callout-icon"><i class="fa-regular fa-square-info"></i></span>
  <p>

    Deliverect customers can configure payment methods via Deliverect. In order to checkout via DPay, the customer must have configured an <strong>Online</strong> payment method. Consult <a href="https://help.deliverect.com/en/articles/7979307-deliverect-pay-configure-a-payment-gateway" target="_blank" rel="noopener noreferrer">this guide here</a> on how to request a payment before proceeding to basket checkout.
  </p>
</div>
`}</HTMLBlock>

## Third Party

If payments are handled by an external provider and processed independently (outside Deliverect), the checkout method must be configured as `third_party`.

### Unpaid orders

Commerce partners may need to submit unpaid orders which is a common for pickup order type. To do this, use the `third_party` payment type and set `isPrepaid` to `false`.  If this method is selected, orders are injected into the POS as unpaid. Payment cannot be updated later via Deliverect; the order must be marked as paid in the POS.

```json Unpaid orders
"payments": [
      {
        "type": "third_party",
        "externalId": "{{$guid}}",
        "isPrepaid": false,
        "amount": 800,
        "metadata": {}
      }
    ]
```

## Order Identifiers

It is possible to supply the platform’s order identifiers during checkout via the order object.

- **channelOrderId**: the full unique ID from the ordering channel. It must not be reused within 48 hours after pickup (across all accounts).
- **channelOrderDisplayId**: a human-readable order reference, typically printed on the POS receipt and used by couriers to identify orders.

```json OrderIds
"order": {
  "channelOrderId": "",
  "channelOrderDisplayId": ""
}
```

# Checkout Status

Across payment methods, a well-formed basket checkout receives an HTTP 200 OK response. Completion occurs asynchronously; use the confirmation delivered to your [checkout update webhook URL](https://developers.deliverect.com/v3.0-ordering-experience/reference/post_checkout-update)
to confirm success.

<HTMLBlock>{`
<div class="callout-banner callout-banner--neutral">
  <span class="callout-icon"><i class="fa-regular fa-square-info"></i></span>
  <p>

    Only consider a checkout successful after the basket checkout webhook URL receives <code>"status": "completed"</code>.
  </p>
</div>
`}</HTMLBlock>
