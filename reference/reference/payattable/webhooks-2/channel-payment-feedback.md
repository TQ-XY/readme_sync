---
api:
  file: payattable-webhooks.json
  operationId: get_payment-feedback
hidden: true
link:
  new_tab: false
metadata:
  robots: index
---
<HTMLBlock>{`
<div style="background: #F00; font-weight: bold; color: #FFF; padding: 10px">Please do not yet share this information to anyone else.<br>The below spec might still be prone to changes.</div>
`}</HTMLBlock>

This webhook is called when we have processed the payment request mentioned in [POST Payment to Bill](ref:post-payment-to-bill) or [POST Payment to Order](ref:post-payment-to-order).

## What we will send you

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        Field name
      </th>

      <th>
        Type
      </th>

      <th>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        statusCode
      </td>

      <td>
        integer
      </td>

      <td>
        HTTP status code
      </td>
    </tr>

    <tr>
      <td>
        paymentRequestId
      </td>

      <td>
        string
      </td>

      <td>
        A unique ID which was communicated upon sending us the payment via [POST Payment to Bill](ref:post-payment-to-bill) or [POST Payment to Order](ref:post-payment-to-order).
      </td>
    </tr>

    <tr>
      <td>
        fullPayment
      </td>

      <td>
        boolean
      </td>

      <td>
        True in case a full payment was done, false if the order/bill was only partially fullfilled.
      </td>
    </tr>

    <tr>
      <td>
        message
      </td>

      <td>
        string
      </td>

      <td>
        A human readable feedback. Contains what went wrong, trying to assist you in understanding what can be done to avoid the error.
      </td>
    </tr>
  </tbody>
</Table>

Successful processing:

```json
{
  "statusCode": 200,
  "paymentRequestId": "626fbe281430a4bd3d1f839e",
  "fullPayment": true,
  "message": "Payment successful"
}
```

Failure:

```json
{
  "statusCode": 400,
  "paymentRequestId": "626fbd821430a4bd3d1f8394",
  "message": "The POS is currently unreachable"
}
```