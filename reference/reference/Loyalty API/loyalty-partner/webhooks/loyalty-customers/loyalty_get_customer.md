---
api:
  file: loyalty_webhooks.json
  operationId: loyalty_get_customer
hidden: false
---
## Purpose

This webhook URL will be called to retrieve customer details in response, the customers will be identified by one of three unique identifiers within the query parameters; `email` , `phoneNumber` or `providerId`&#x20;

### Query Parameters

<HTMLBlock>{`
<div class="callout-banner callout-banner--neutral">
  <span class="callout-icon"><i class="fa-regular fa-square-info"></i></span>
  <p>
     All request parameters will be URL encoded.
  </p>
</div>
`}</HTMLBlock>

| Parameter                                               | Description                                                                                                                                                                                                    |
| :------------------------------------------------------ | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `email`                                                 | This parameter will always be sent if your integration uses the email as a unique identifier<br /><br />e.g.`https://yourwebhook.com/customer?email=john.doe%40email.com`                                      |
| `phoneNumber `                                          | This parameter will always be sent if your integration uses the phone number as a unique identifier. (E.164 international <br /><br />e.g.`https://yourwebhook.com/customer?phoneNumber=%2B32111111111`format) |
| `providerId` <span style="color:red">\* required</span> | The customer's unique identifier within the loyalty provider's system.<br /><br />e.g. `https://yourwebhook.com/customer?providerId=abc123`                                                                    |
| `accountId`                                             | The merchant's account ID in Deliverect                                                                                                                                                                        |
| `loyaltyProfileId`                                      | The Id of the profile where the response configuration was stored                                                                                                                                              |
| `locationId`                                            | The location ID related to the merchant's account in Deliverect                                                                                                                                                |
| `channelLinkId`                                         | The channel link ID related to the location of the merchant's account in Deliverect                                                                                                                            |

### Response

<Table align={["left","left","left","left"]}>
  <thead>
    <tr>
      <th>
        Customer Attributes
      </th>

      <th>
        Type
      </th>

      <th>
        Required
      </th>

      <th>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        `providerId`
      </td>

      <td>
        string
      </td>

      <td>
        Yes
      </td>

      <td>
        ID of the loyalty provider to identify the customer
      </td>
    </tr>

    <tr>
      <td>
        `firstName`
      </td>

      <td>
        string
      </td>

      <td>
        No
      </td>

      <td>
        First name of the customer.
      </td>
    </tr>

    <tr>
      <td>
        `lastName`
      </td>

      <td>
        string
      </td>

      <td>
        No
      </td>

      <td>
        Last name of the customer.
      </td>
    </tr>

    <tr>
      <td>
        `email`
      </td>

      <td>
        string
      </td>

      <td>
        Yes if used as unique identifier
      </td>

      <td>
        The customer's email.
      </td>
    </tr>

    <tr>
      <td>
        `phoneNumber`
      </td>

      <td>
        string
      </td>

      <td>
        Yes if used as unique identifier
      </td>

      <td>
        The customer's phone email. Must be sent in E.164 international standard.
      </td>
    </tr>

    <tr>
      <td>
        `dateOfBirth`
      </td>

      <td>
        string
      </td>

      <td>
        No
      </td>

      <td>
        The provided date must be in ISO 8601 UTC format. Example: 2025-05-22T22:55:59+00:00.
      </td>
    </tr>

    <tr>
      <td>
        `status`
      </td>

      <td>
        string
      </td>

      <td>
        Yes
      </td>

      <td>
        See statuses below.
      </td>
    </tr>

    <tr>
      <td>
        `acceptedTCAt`
      </td>

      <td>
        string
      </td>

      <td>
        Yes
      </td>

      <td>
        The date and time when the customer accepted the terms and conditions. Must be in ISO 8601 UTC format. Example: `1970-01-01T00:00:00+00:00`.
      </td>
    </tr>

    <tr>
      <td>
        `"lifetimePointsBalance"`
      </td>

      <td>
        integer
      </td>

      <td>
        No
      </td>

      <td>
        Number of loyalty points a customer has earned over the lifetime of their account.

        Note: it does not indicate current balance, which will be provided via ["GET loyalty Customer Wallet".](https://developers.deliverect.com/reference/loyalty-partner-get-customer-wallet)
      </td>
    </tr>

    <tr>
      <td>
        `tier`
      </td>

      <td>
        Object
      </td>

      <td>
        No
      </td>

      <td>
        See tier object description bellow.
      </td>
    </tr>
  </tbody>
</Table>

| Tier Attributes | Type   | Required | Description                          |
| :-------------- | :----- | :------- | :----------------------------------- |
| `name`          | string | Yes      | The name of the Tier                 |
| `description`   | string | No       | A description for the Tier           |
| `media`         | Object | No       | See media object description bellow. |

<Table align={["left","left","left","left"]}>
  <thead>
    <tr>
      <th>
        Media attributes
      </th>

      <th>
        Type
      </th>

      <th>
        Required
      </th>

      <th>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        `url`
      </td>

      <td>
        string
      </td>

      <td>
        Yes
      </td>

      <td>
        A video or image URL that can be displayed along the tier information.
      </td>
    </tr>

    <tr>
      <td>
        `type`
      </td>

      <td>
        string
      </td>

      <td>
        Yes
      </td>

      <td>
        Valid options:

        - `image`
        - `video`
      </td>
    </tr>
  </tbody>
</Table>

| Status Values         | Type   | Description                                                         |
| :-------------------- | :----- | :------------------------------------------------------------------ |
| `unknown`             | string | Customer status cannot be determined.                               |
| `activation_pending`  | string | Customer created an account but did not verify/complete.            |
| `active`              | string | Customer created an account and verified their access.              |
| `blocked_by_provider` | string | Customer blacklisted from partner. Unable to interact with loyalty. |

<HTMLBlock>{`
<div class="callout-banner callout-banner--neutral">
  <span class="callout-icon"><i class="fa-regular fa-square-info"></i></span>
  <p>

    If the customer doesn't exist on your platform, the endpoint should return an HTTP <code>404</code> Not found response
  </p>
</div>
`}</HTMLBlock>