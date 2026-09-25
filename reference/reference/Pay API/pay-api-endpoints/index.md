---
title: Endpoints
excerpt: ''
deprecated: false
hidden: false
icon: fad fa-plug
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
<BaseURLsTable />

## Pay API Endpoints

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
        [Get Payment Gateways](ref:pay-api-get-payment-gateways)
      </td>

      <td>
        <GET_LABEL />
      </td>

      <td>
        Retrieves all payment gateways configured for a store.
      </td>
    </tr>

    <tr>
      <td>
        [Request Payment](ref:request-payment)
      </td>

      <td>
        <POST_LABEL />
      </td>

      <td>
        Request for payment intent.
      </td>
    </tr>

    <tr>
      <td>
        [Refund Payment](ref:pay-api-refund-payment)
      </td>

      <td>
        <POST_LABEL />
      </td>

      <td>
        Request to refund a payment.
      </td>
    </tr>

    <tr>
      <td>
        [Payment Update ](ref:pay-api-payment-update)
      </td>

      <td>
        <POST_LABEL />
      </td>

      <td>
        Endpoint receiving payment update events.
      </td>
    </tr>
  </tbody>
</Table>
