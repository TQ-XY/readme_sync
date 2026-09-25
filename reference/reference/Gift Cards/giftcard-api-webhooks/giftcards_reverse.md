---
api:
  file: giftCards_webhooks.json
  operationId: giftcards_reverse
hidden: false
---
## Purpose

This webhook is called by our system to reverse the redemption of a gift card i.e. when an order containing a gift card payment is cancelled.

### Payload Details

| Field                    | Type   | Required | Description                             |
| :----------------------- | :----- | :------- | :-------------------------------------- |
| giftCardNumber           | string | Yes      | The unique identifier of the gift card. |
| giftCardVerificationCode | string | No       | The verification code of the gift card. |
| amount                   | int    | Yes      | The amount to be reversed.              |

```json Payload Example
{
    "giftCardNumber": "125476349806",
    "giftCardVerificationCode": "1234",
    "amount": 100
}
```

<br />

<br />