---
api:
  file: payPlatform_webhooks.json
  operationId: payplatform_payments_profile_register
hidden: false
---
## Purpose

As part of onboarding a new payment platform, a webhook event will be sent to transfer the relevant account information and in response receive the necessary webhook URLs for each integration function

### Request Parameters

| Attribute        | Definition                                                                                                             |
| ---------------- | ---------------------------------------------------------------------------------------------------------------------- |
| gatewayProfileId | The unique identifier set in Deliverect for the payment platform                                                       |
| accountId        | The unique customer <Glossary>accountId</Glossary>                                                                     |
| apiKey           | A unique identifier of the customer account known to the payment platform                                              |
| webhookUrl       | The endpoint to where [payment events](https://developers.deliverect.com/v3.0/reference/payment-events) are to be sent |

<br />

### Response Parameters

| Attribute                   | Definition                                                                 |
| --------------------------- | -------------------------------------------------------------------------- |
| requestPaymentURL           | The endpoint where payment request events should be sent                   |
| refundPaymentURL            | The endpoint where payment refund events should be sent                    |
| unregisterGatewayProfileURL | The endpoint used to unregister a payment platform from a customer account |