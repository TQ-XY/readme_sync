---
api:
  file: loyalty_webhooks.json
  operationId: loyalty_token
hidden: false
---
## Purpose

During the merchant registration process, you should have provided the following essential OAuth details:

- Base OAuth URL
- Client ID
- Client Secret

At this stage of the OAuth workflow, Deliverect anticipates receiving an authorisation code via an HTTP redirect initiated by your third-party application [SSO redirect](https://developers.deliverect.com/v3.0/reference/loyalty-partner-sso-redirect). Upon successful reception of this code, Deliverect will then call your loyalty provider's authentication endpoint, located at `{baseOauthUrl}/token`, to exchange the authorisation code for an access token.

Following the OAuth workflow, then Deliverect will proceed to obtain the customer details by providing the received access token in the headers when calling the [Get customer](https://developers.deliverect.com/v3.0/reference/loyalty_get_customer) endpoint.

### Payload

| Attributes      | Type   | Required | Description                                                                                                                                                                                                                                |
| :-------------- | :----- | :------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `grant_type`    | string | Yes      | Refers to the method or flow that the Deliverect application uses to obtain an access token from an authorization server. Currently, Deliverect only supports Client Credentials Grant. This field is always sent as `authorization_code`. |
| `client_id`     | string | Yes      | The client ID configured by the merchant during the registration process                                                                                                                                                                   |
| `client_secret` | string | Yes      | The client secret configured by the merchant during the registration process                                                                                                                                                               |
| `code`          | string | Yes      | The authorisation code received during the SSO redirect                                                                                                                                                                                    |

<br />

### Response

| Attributes     | Type   | Required | Description                                                                                                |
| :------------- | :----- | :------- | :--------------------------------------------------------------------------------------------------------- |
| `token_type`   | string | Yes      | The token type issued by the authorisation server. Deliverect currently supports only `Bearer`token types. |
| `scope`        | string | Yes      | Not required by the Loyalty API server. This field can be set to an empty string.                          |
| `created_at`   | string | Yes      | Unix timestamp on when the token was created.                                                              |
| `access_token` | string | Yes      | The credential that represents the authorisation granted by the loyalty provider.                          |

<br />