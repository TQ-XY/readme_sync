---
api:
  file: payPlatform_webhooks.json
  operationId: payplatform_payments_request
hidden: false
---
## Purpose

Where a payment request is submitted, this webhook event will contain all the relevant details which needs responded to with a `status` of either; `authorized`, `pending` or `refused`&#x20;

### Request Parameters

| Attribute | Definition |
| --- | --- |
| `gatewayProfileId` | Identifier for the gateway profile that should process the payment. |
| `amount` | Payment amount in the smallest currency unit, such as cents. |
| `currency` | ISO 4217 currency code for the payment amount, such as `EUR`. |
| `reference` | Your unique reference for the payment, such as an order number. |
| payer.`name` | Payer's display name. |
| payer.`email` | Payer's email address. |
| payer.`reference` | Your external identifier for the payer. |
| `returnUrl` | URL to send the payer to after they complete or exit the payment flow. |
| `logoUrl` | Public URL of a logo to display in the payment flow. |

### Response Parameters

| Attribute | Definition |
| --- | --- |
| update.`gatewayId` | Identifier assigned to the payment by the gateway. This can be `null` when the payment is refused. |
| update.`status` | Payment decision: `authorized`, `pending`, or `refused`. |
| update.`method` | Payment method reported by the gateway, such as `visa`. |
| action.`type` | Required next action for the payer, such as `redirect`; absent when no further action is needed. |
| action.`url` | Destination URL for the required action, such as the gateway's payment-completion page. |