---
api:
  file: channel_webhooks.json
  operationId: >-
    channel_oauth_authorize?client_id=integration_id&state=state_id&redirect_uri=redirect_uri&response_type=response_type&metadata=metadata
hidden: true
---
## Authentication

|                 |                                                    | Type   |
| :-------------- | :------------------------------------------------- | :----- |
| `client_id`     | Deliverect application client id                   | string |
| `client_secret` | Deliverect application client secret.              | string |
| `code`          | The authentication code returned the previous step | string |
| `grant_type`    |                                                    |        |

1. The user is redirected to partner frontend with an authorize url.
2. Users will approve requested scopes.
3. Confirm the location and other metadata
4. Channel redirects to the `redirect_uri` with a challenge code, Deliverect frontend forwards the code to Deliverect API.
5. Deliverect API now sends a request to the Channel API for an `access_token` with this code.
6. Deliverect API persists the `access_token` and confirms on our frontend that the store/venue is now authorized.
7. The venue ID is typically encoded into the `access_token`
8. Our onboarding wizard is able to load the store(s) related to this access_token. The user will be shown an overview of these store(s) (based on GET /venues data) and chooses which (Deliverect) menu they want to have live.
9. On confirmation of the store and menu, Deliverect API is able to patch the Deliverect store ID and webhook URL onto the Wolt venue and then publish a menu.

## When we call your endpoint

For information on HMAC Authentication [see the link here](https://developers.deliverect.com/reference/hmac-authentication)