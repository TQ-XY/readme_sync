---
api:
  file: giftCards_webhooks.json
  operationId: giftcards_redeem
hidden: false
link:
  new_tab: false
---
This webhook is called by our system to redeem values from a gift card.

### When the webhook is Triggered

* When an order containing a gift card payment is injected.

### Payload Details

| Field                    | Type   | Required | Description                             |
| :----------------------- | :----- | :------- | :-------------------------------------- |
| giftCardNumber           | string | Yes      | The unique identifier of the gift card. |
| giftCardVerificationCode | string | No       | The verification code of the gift card. |
| amount                   | int    | Yes      | The amount to be redeemed.              |

```json Payload Example
{
    "giftCardNumber": "125476349806",
    "giftCardVerificationCode": "1234",
    "amount": 100
}
```

<br />

<br />