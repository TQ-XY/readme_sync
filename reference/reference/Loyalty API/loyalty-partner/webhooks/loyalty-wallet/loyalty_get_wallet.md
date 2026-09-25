---
api:
  file: loyalty_webhooks.json
  operationId: loyalty_get_wallet
hidden: false
---
## Purpose

Retrieve a customer's loyalty wallet by returning either their cash or points balance along with any expiration details.

## Format

A Loyalty platform can specify the unique identifier used in their system to identify customers. Deliverect will send that identifier as a request parameter on the provided endpoint. For example, if the unique customer identifier is email, the request url will be sent as: `http://yourwebhook.com/customer/wallet?email=john.doe%40email.com`

### Request Parameters

| Parameter          | Description                                                                                                                  | Example URL                                                                  | Format |
| ------------------ | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------- | ------ |
| `accountId`        | The merchant's account ID in Deliverect                                                                                      |                                                                              | String |
| `locationId`       | The merchant's location ID in Deliverect                                                                                     |                                                                              | String |
| `channelLinkId`    | The  unique Id of the ordering channel                                                                                       |                                                                              | String |
| `loyaltyProfileId` | Unique Id of the Loyalty platform                                                                                            |                                                                              | String |
| `email`            | Customer's email address sent if your integration uses the email as a unique identifier                                      | `http://yourwebhook.com/customer/wallet?email=john.doe%40email.com`          | String |
| `phoneNumber`      | Customer's phone number in E.164 international format sent if your integration uses the phone number as a unique identifier. | `http://yourwebhook.com/customer/wallet?phoneNumber=%2B32111111111`          | String |
| `providerId`       | Unique customer identifier known to the loyalty provider                                                                     | `http://yourwebhook.com/customer/wallet?providerId=%partner-customer-id-123` | String |

<br />

<HTMLBlock>{`
<div class="callout-banner callout-banner--neutral">
  <span class="callout-icon"><i class="fa-regular fa-square-info"></i></span>
  <p>
    All request parameters are URL encoded.
  </p>
</div>
`}</HTMLBlock>

### Response Body

The loyalty provider must return the customer’s available balance, including loyalty points and optionally, wallet cash. This enables Deliverect Direct channels and Kiosk, as well as external partners, to display the customer’s current funds so they can decide how to use their rewards.

```json Get Customer Wallet
{
  "points": {
    "balance": 150,
    "expirations": [
      {
        "amount": 500,
        "date": "YYYY-MM-DD"
      }
    ]
  },
  "cash": {
    "balanceAmount": 1000,
    "expirations": [
      {
        "amount": 150,
        "date": "YYYY-MM-DD"
      }
    ]
  }
}
```

###

If the customer does not exist in your platform, return a `404` status code.

Return at least one wallet object: `cash` or `points`.

### Response

| Customer Wallet Attributes | Type   | Required | Description                          |
| :------------------------- | :----- | :------- | :----------------------------------- |
| `cash`                     | Object | Yes      | See cash object description below.   |
| `points`                   | Object | Yes      | See points object description below. |

<br />

| Cash Attributes | Type          | Required                     | Description                                                                                                                                        |
| :-------------- | :------------ | :--------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------- |
| `balanceAmount` | integer       | No (defaults to zero)        | Cash balance that the customer uses to redeem programs.  It should be sent as an integer with 2 decimal digits e.g. 1 dollar would be sent as 100. |
| `expirations`   | list\[Object] | No (defaults to empty array) | See expirations object description below.                                                                                                          |

<br />

| Cash Expirations Attributes | Type    | Required                                             | Description                                             |
| :-------------------------- | :------ | :--------------------------------------------------- | :------------------------------------------------------ |
| `amount`                    | integer | Yes if your integration uses cash to redeem programs | Amount of cash balance to expire according to the date. |
| `date`                      | date    | Yes if your integration uses cash to redeem programs | Expiration date of the amount to be expired.            |

<br />

| Points Attributes | Type          | Required                     | Description                                             |
| :---------------- | :------------ | :--------------------------- | :------------------------------------------------------ |
| `balance`         | float         | No (defaults to zero)        | Cash balance that the customer uses to redeem programs. |
| `expirations`     | list\[Object] | No (defaults to empty array) | See expirations object description below.               |

| Points Expirations Attributes | Type  | Required                                               | Description                                               |
| :---------------------------- | :---- | :----------------------------------------------------- | :-------------------------------------------------------- |
| `amount`                      | float | Yes if your integration uses points to redeem programs | Amount of points balance to expire according to the date. |
| `date`                        | date  | Yes if your integration uses points to redeem programs | Expiration date of the amount to be expired.              |