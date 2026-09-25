---
api:
  file: channel_webhooks.json
  operationId: channel_payment_update
hidden: false
---
## Purpose

Listen to this webhook to receive updates on a payment processed through Deliverect Pay. It can be used to know if a payment was authorized or refused, and consequently submit the order.

## Definitions

| Parameter | Meaning                                                  |
| :-------- | :------------------------------------------------------- |
| paymentId | The unique payment ID from Deliverect Pay                |
| status    | The status from the list of value supported for updates. |

## Available status for courier update

| Status     | Description                                                                                                  |
| :--------- | :----------------------------------------------------------------------------------------------------------- |
| authorized | Payment was successfully authorized                                                                          |
| refused    | Payment was refused due to issues with the shopper's payment methods (not enough balance, wrong cvc, etc...) |
| failed     | Payment failed to be processed due to a technical issue                                                      |
| pending    | Payment is being processed                                                                                   |

```json Example Request
{
    "paymentId": "651142e93c54c5405****6a3",
    "status": "authorized"
}
```

## Response format