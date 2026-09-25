---
api:
  file: loyalty-api.json
  operationId: loyalty-partner-sso-redirect
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
## Purpose

This endpoint facilitates a seamless transition for customers coming from a Loyalty Partner's mobile application to the Online Ordering Channel. It validates the partner's session, authenticates the user within the internal ecosystem, and performs a final redirect to the target store.

### Path Parameters

| Parameter       | Type   | Required | Description                                                                                                                                                              |
| --------------- | ------ | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `channelLinkId` | String | Yes      | The unique identifier for the specific channel configuration (e.g., a specific Mobile App integration). Used to retrieve default store URLs and merchant configurations. |

### Query Parameters

| Parameter   | Type         | Required | Description                                                                                                                                                                                        |
| ----------- | ------------ | -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `code`      | String       | Yes      | The authentication code provided by the Loyalty Partner to verify the user's session.                                                                                                              |
| `returnUrl` | String (URL) | No       | An optional destination URL within the store. If provided, the user is redirected here upon success. If missing, the system redirects to the default Store URL configured for the `channelLinkId`. |

<HTMLBlock>{`
<div class="callout-banner callout-banner--important">
  <span class="callout-icon"><i class="fa-duotone fa-solid fa-triangle-exclamation"></i></span>
  <p>
   <code>returnUrl</code> parameter must be URL encoded
  </p>
</div>
`}</HTMLBlock>

## Response & Redirect Logic

On a successful authentication, the API will not return a JSON body. Instead, it will return an HTTP 302 status code.

**Redirect Priority:**

1. Redirect to the `returnUrl` provided in the query string.

2. **Fallback:** Redirect to the `Store URL` retrieved from the `channelLinkId` configuration.

<br />

### Error Scenarios

| Scenario                   | Status Code                | Description                                             |
| -------------------------- | -------------------------- | ------------------------------------------------------- |
| **Missing Channel Config** | `404 Not Found`            | The `channelLinkId` provided in the URL does not exist. |
| **Invalid URL parameters** | `422 Unprocessable Entity` | The provided URL parameters are invalid.                |

## Implementation

- **Security:** The `code` parameter should be treated as a one-time-use credential (OTP).

- **Graceful Failure Redirect:** In the event that customer authentication fails (e.g., invalid code or no matching account), the customer will still be redirected to the online ordering store. They will not be logged in, allowing them to continue their ordering experience as guests or log in manually using their existing credentials.

## Example Request

**Request:**
`GET http://staging.api.deliverect.com/loyalty/685d1e2dfe7bf9b714454796/sso?code=abc123&returnUrl=https://store.com/menu`

**Success Response:**
`HTTP/1.1 302 Found`
`Location: https://store.com/menu?auth_token=xyz789...`