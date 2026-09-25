---
api:
  file: payApi_webhooks.json
  operationId: payapi_payment_update
hidden: false
---
## Purpose

Use the payment update webhook to receive the result of an asynchronous payment request. The event reports a payment `status` of `authorized` or `refused` and includes the payment ID and gateway metadata.

<HTMLBlock>{`
<div class="callout-banner callout-banner--important">
  <span class="callout-icon"><i class="fa-duotone fa-solid fa-triangle-exclamation"></i></span>
  <p>
    <strong>Payment Authorization</strong><br>
    Before proceeding to finalise checkout, you must confirm that <code>"status": "authorized"</code> is received for the payment.
  </p>
</div>
`}</HTMLBlock>

```json Authorized
{
  "paymentId": "68ee0b062744b20a958dae54",
  "status": "authorized",
  "metadata": {
    "gatewayProfileLinkId": "68eaa1df8c4c3ca7c569dc5c",
    "methodRaw": "visa"
  }
}
```
```json Refused
{
  "paymentId": "68ee0b062744b20a958dae54",
  "status": "refused",
  "metadata": {
    "gatewayProfileLinkId": "68eaa1df8c4c3ca7c569dc5c",
    "methodRaw": "visa"
  }
}
```