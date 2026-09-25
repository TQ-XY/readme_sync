---
api:
  file: giftCards_webhooks.json
  operationId: giftcards_registerprofile-1
hidden: false
link:
  new_tab: false
metadata:
  robots: index
---
This webhook is called to retrieve the balance of a gift card.

### Payload Details

| Field                    | Type   | Required |
| :----------------------- | :----- | :------- |
| giftCardNumber           | string | Yes      |
| giftCardVerificationCode | string | Yes      |
| locationId               | string | Yes      |

### Payload Example

```json Payload Example
{
    "giftCardNumber": "125476349806",
    "giftCardVerificationCode": "1234",
    "locationId": ObjectId
}
```

### Response Example

```json Response Example
{
    "giftCardNumber": "125476349806",
    "amount": 123,
}
```