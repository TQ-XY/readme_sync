---
api:
  file: giftCards_webhooks.json
  operationId: giftcards_registerprofile
hidden: false
---
To integrate your gift cards solution with Deliverect Gift Cards, you will need to provide a **registration URL**. This URL will be invoked when a merchant initiates the setup of gift card services in Deliverect.

During this setup, the merchant will be prompted to enter an API key, which must be pre-issued by the gift cards platform. Subsequently, Deliverect will call the provided **registration URL** to retrieve all necessary additional details to complete the integration process.

### Payload Details

| Parameter | Type   | Description                                                                                                                                             |
| :-------- | :----- | :------------------------------------------------------------------------------------------------------------------------------------------------------ |
| account   | string | The merchant's account Id in Deliverect                                                                                                                 |
| apiKey    | string | A unique identifier, typically a string of characters, used to authenticate and authorize a user, application, or project when interacting with an API. |

```json Payload Example
{
    "account": "6401c934c43f86ebfedaeb9c",
    "apiKey": "123***890"
}
```

### Response Details

| Attribute               | Type   | Description                                                             |
| :---------------------- | :----- | :---------------------------------------------------------------------- |
| redeemGiftCardURL       | string | This webhook is called by our system to redeem values from a gift card. |
| revertRedeemGiftCardURL | string | This webhook is called to revert a redeem operation.                    |
| getGiftCardBalanceURL   | string | This webhook is called to retrieve the balance of a gift card.          |

```json Response Example
{
    "redeemGiftCardURL": "https://yourserver.com/redeem",
    "revertRedeemGiftCardURL": "https://yourserver.com/reverse",
    "getGiftCardBalanceURL": "https://yourserver.com/balance",
}
```