---
api:
  file: loyalty_webhooks.json
  operationId: loyalty_customer
hidden: false
---
## Purpose

This endpoint will be called when a new customer needs created within the loyalty provider's platform.

### Payload

| Customer Attributes | Type   | Required                         | Description                                                                         |
| :------------------ | :----- | :------------------------------- | :---------------------------------------------------------------------------------- |
| `firstName`         | string | No                               | First name of the customer.                                                         |
| `lastName`          | string | No                               | Last name of the customer.                                                          |
| `email`             | string | Yes if used as unique identifier | The customer's email.                                                               |
| `phoneNumber`       | string | Yes if used as unique identifier | The customer's phone email. Must be sent in E.164 international standard.           |
| `dateOfBirth`       | string | No                               | The provided date must be in ISO 8601 format. Example: 2025-05-22T22:55:59+12:00.   |
| `accountId`         | string | Yes                              | The merchant's account ID in Deliverect                                             |
| `loyaltyProfileId`  | string | Yes                              | The Id of the profile where the response configuration was stored                   |
| `locationId`        | string | No                               | The location ID related to the merchant's account in Deliverect                     |
| `channelLinkId`     | string | No                               | The channel link ID related to the location of the merchant's account in Deliverect |

<br />

### Response

<HTMLBlock>{`
<div class="callout-banner callout-banner--neutral">
  <span class="callout-icon"><i class="fa-regular fa-square-info"></i></span>
  <p>

    If the customer already exists on your platform, the endpoint should return a <code>409</code> status code
  </p>
</div>
`}</HTMLBlock>

| Customer Attributes | Type    | Required                         | Description                                                                                                                                |
| :------------------ | :------ | :------------------------------- | :----------------------------------------------------------------------------------------------------------------------------------------- |
| `firstName`         | string  | No                               | First name of the customer.                                                                                                                |
| `lastName`          | string  | No                               | Last name of the customer.                                                                                                                 |
| `email`             | string  | Yes if used as unique identifier | The customer's email.                                                                                                                      |
| `phoneNumber`       | string  | Yes if used as unique identifier | The customer's phone email. Must be sent in E.164 international standard.                                                                  |
| `dateOfBirth`       | string  | No                               | The provided date must be in ISO 8601 UTC format. Example: 2025-05-22T22:55:59+00:00.                                                      |
| `acceptedTCAt`      | string  | No                               | The date and time when the customer accepted the terms and conditions. Must be in ISO 8601 UTC format. Example: 2025-05-22T22:55:59+00:00. |
| `balance`           | integer | No                               | The point balance of the customer.                                                                                                         |
| `tier`              | Object  | No                               | See tier object description bellow.                                                                                                        |

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