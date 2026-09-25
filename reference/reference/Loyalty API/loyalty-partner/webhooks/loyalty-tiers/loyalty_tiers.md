---
api:
  file: loyalty_webhooks.json
  operationId: loyalty_tiers
hidden: false
---
## Purpose

This webhook will request the available loyalty tiers for the configured merchant.

<HTMLBlock>{`
<div class="callout-banner callout-banner--neutral">
  <span class="callout-icon"><i class="fa-regular fa-square-info"></i></span>
  <p>
     To determine the progression path, results must be sorted from the lowest ranking tier to the most exclusive tier.
  </p>
</div>
`}</HTMLBlock>

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