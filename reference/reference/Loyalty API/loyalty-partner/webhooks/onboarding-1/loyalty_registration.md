---
api:
  file: loyalty_webhooks.json
  operationId: loyalty_registration
hidden: false
---
## Purpose

To  integrate your loyalty solution with Deliverect Loyalty, you will need to provide a **registration URL**. This URL will be invoked when a merchant initiates the setup of loyalty services in Deliverect.

During this setup, the merchant will be prompted to enter an API key, which must be pre-issued by the loyalty platform. Subsequently, Deliverect will call the provided **registration URL** to retrieve all necessary additional details to complete the integration process.

### Payload Details

| Parameter          | Type   | Description                                                                                                                                             |
| :----------------- | :----- | :------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `accountId`        | string | The merchant's account Id in Deliverect                                                                                                                 |
| `loyaltyProfileId` | string | The Id of the profile where the response configuration was stored                                                                                       |
| `apiKey`           | string | A unique identifier, typically a string of characters, used to authenticate and authorize a user, application, or project when interacting with an API. |

<br />

```json Payload Example
{
    "account": "6401c934c43f86ebfedaeb9c",
    "accountId": "6401c934c43f86ebfedaeb9c",
    "loyaltyProfileId": "67acb1893b57bab8866dfa4c",
    "apiKey": "123***890"
}
```

<br />

### Response Details

| Attribute                    | Type   | Required | Description                                                                                                                                                           |
| :--------------------------- | :----- | :------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `customerURL`                | string | **Yes**  | This webhook is used to create a new user or retrieve user details.                                                                                                   |
| `customerWalletURL`          | string | **Yes**  | This webhook is used to retrieve the customer's wallet details, such as available points and cash balance.                                                            |
| `loyaltyProgramsURL`         | string | **Yes**  | This webhook is called by our system to retrieve all loyalty programs a customer is eligible for.                                                                     |
| `orderURL`                   | string | **Yes**  | Whenever a customer places an order, the order details will be sent to this endpoint in order to award points to the customer and consume applied programs.           |
| `validateWalletURL`          | string | No       | This webhook is initiated by our system to validate a customer's request to use cash or points from their loyalty wallet as a discount on a current order.            |
| `loyaltyValidateProgramsURL` | string | No       | This webhook is called to validate a customer's selected loyalty programs against their current order.                                                                |
| `tiersURL`                   | string | No       | Used to list all the available tier's and the progression path.                                                                                                       |
| `oauthUrl`                   | string | No       | Base URL for OAuth workflows.                                                                                                                                         |
| `oauthClientId`              | string | No       | A unique identifier assigned to an application that is requesting access to a user's resources through the OAuth protocol.                                            |
| `oauthClientSecret`          | string | No       | As a confidential string of characters that acts like a password for an application (the "client") when it needs to authenticate itself with an authorisation server. |

<br />

```json Response Example
{
    "customerURL": "https://yourserver.com/customer",
    "customerWalletURL": "https://yourserver.com/customerWallet",
    "validateWalletURL": "https://yourserver.com/validateWallet",
    "loyaltyProgramsURL": "https://yourserver.com/programs",
    "loyaltyValidateProgramsURL": "https://yourserver.com/validatePrograms",
    "orderURL": "https://yourserver.com/orders",
    "tiersURL": "https://yourserver.com/tiers",
    "oauthUrl": "https://yourserver.com/oauth",
    "oauthClientId": "myClientId",
    "oauthClientSecret": "zxcv1323"
}

```

### Single Sign On (SSO)

For loyalty providers who which to provide SSO authentication, the following details will need to be provided in the response in order to enable SSO:

- `oauthUrl`
- `oauthClientId`
- `oauthClientSecret`