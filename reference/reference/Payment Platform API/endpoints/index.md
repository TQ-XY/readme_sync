---
title: Endpoints
deprecated: false
hidden: false
icon: fad fa-plug
metadata:
  robots: index
---
<BaseURLsTable />

## Payment Platform Endpoints

Use the following endpoints to manage the payment lifecycle for a store.

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        ENDPOINT
      </th>

      <th>
        TYPE
      </th>

      <th>
        FUNCTION
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        [Payment Events](ref:payment-events)
      </td>

      <td>
        <POST_LABEL />
      </td>

      <td>
        Payment platforms should call this endpoint to confirm the status of a payment request
      </td>
    </tr>
  </tbody>
</Table>
