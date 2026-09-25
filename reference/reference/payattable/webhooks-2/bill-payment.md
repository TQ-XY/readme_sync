---
api:
  file: payattable-webhooks.json
  operationId: get_new-endpoint
hidden: true
link:
  new_tab: false
metadata:
  robots: index
---
<HTMLBlock>{`
<div style="background: #F00; font-weight: bold; color: #FFF; padding: 10px">Please do not yet share this information to anyone else.<br />The below spec might still be prone to changes.</div>
`}</HTMLBlock>

When we receive a **payment notification** from a channel partner, we will send this notification to the POS who is assumed to accept this payment, apply it to the bill and close the bill.

Closing the bill would be determined where the total paid amount (excluding the tips) and the payment(s) already done and processed via the POS + the payment being set matches the oustanding balance.

All information related to the payment notification can be found in the **body** of the POST request we'll be doing. The fields passed through are similar to the ones documented on **[POST Payment to Bill](ref:post-payment-to-bill)**, with the exception of the below:

* instead of the channelLink, we will provide the **locationId**
* the **callbackUrl will not be included** as we expect sync communication between Deliverect and the POS in this scenario (the callback url refers to our partner, whereas the POS will communicate with the Deliverect API and not directly with the partner that sent the payment notification)
* the **billId** or the **orderId** will be part of the body payload. The orderId will be mentioned in case Deliverect also created the order and will refer to the `_id` field you received in the [POST Orders webhook call](ref:post-orders-webhook).
* the **paymentRequestId** is what we use to communicate asynchronously to our payment partner whether your POS successfully processed the payment. We send it to you just for logging purposes.

The provided totalAmount might be lower than the due amount on the POS. This indicates we are dealing with a **partial payment** (e.g. customer might be preferring to pay partially by app and partially by cash/voucher in-restaurant).<br />

```json Example payload
{
  "location": "61********************a4",
  "billId": "123",
  "orderId": "62********************1f",
  "paymentRequestId": "456",
  "decimalDigits": 2,
  "paidAmount": 1400,
  "tipAmount": 200,
  "message": "Transfer of €12.00 for your Moon Burger requested",
  "reference": "22.02.14-001-450",
  "paidAt": "2022-02-14T12:01:32.128Z"
}
```

If the payment does not get accepted, please return us the appropriate HTTP response (4xx in case we did something wrong, 5xx if the problem is on your side). If the payment gets accepted, we expect an **HTTP 200 response**.

The following data will be included in your**response body**:

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        Field name
      </th>
      <th>
        Description
      </th>
      <th>
        Type
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        `message`
      </td>
      <td>
        Human readable message. In case something went wrong, an explanation what happened. You can share additional technical messages in additional fields. Optional field in case of success.
      </td>
      <td>
        string
      </td>
    </tr>
    <tr>
      <td>
        `closed`
      </td>
      <td>
        True in case the ticket was closed as a result of our payment call. False if it remains open (partial payment).
      </td>
      <td>
        boolean
      </td>
    </tr>
    <tr>
      <td>
        `bill`
      </td>
      <td>
        To avoid a roundtrip to your API, we expect the full bill as mentioned on endpoint [GET Bill by ID](ref:bill-by-id) to be part of the return message of payment. It will enable us to conclude the due amount in case the receipt was not closed.  

        Note we expect a single object, not an array, as a payment deals with one bill.
      </td>
      <td>
        json object
      </td>
    </tr>
  </tbody>
</Table>

**Example** responses

```json Successful closure
{
  "message": "Payment successfully processed",
  "closed": true,
  "bill": {
    "billId": "R29532LF",
    "tableId": "T1",
    "createdAt": "2022-05-04T09:11:51.166000Z",
    "closedAt": "2022-05-09T14:12:23.478000Z",  
    "decimalDigits": 2,
    "subTotal": 700,
    "discountTotal": 100,
    "discounts": [{
    	"name": "Our company birthday discount",
    	"total": 100
    }],
    "surchargesTotal": 200,
    "surcharges": [{
    	"name": "Take-away",
    	"total": 200
    }],
    "taxTotal": 48,
    "taxes": [{
    	"name": "6% VAT",
    	"total": 48
    }],
    "total": 800,
    "totalDue": 0,
    "items": [
      {
        "plu": "PLU-01",
        "name": "My first product",
        "quantity": 1,
        "price": 300,
        "subItems": []
      },
      {
        "plu": "PLU-02",
        "name": "My second product",
        "quantity": 1,
        "price": 400,
        "subItems": [
          {
            "plu": "PLU-03",
            "name": "My modifier",
            "quantity": 1,
            "price": 0,
            "subItems": []
          }
        ]
      }
    ],
    "payments": [
      {
        "name": "Cash",
        "total": 400
      },
      {
        "name": "Deliverect",
        "total": 400
      }
    ]
  }
}
```
```json Partial payment
{
  "statusCode": 200,
  "message": "Payment successfully processed. $15.00 remains to be paid.",
  "closed": false,
  "bill": {
    "billId": "R29533LF",
    "tableId": "",
    "created": "2022-05-09T09:26:55.134000Z",
    "closed": "1970-00-00T00:00:00.000000Z",  
    "decimalDigits": 2,
    "subTotal": 2000,
    "discountTotal": 0,
    "discounts": [],
    "surchargesTotal": 0,
    "surcharges": [],
    "taxTotal": 120,
    "taxes": [{
    	"name": "6% VAT",
    	"total": 120
    }],
    "total": 2000,
    "totalDue": 1500,
    "items": [
      {
        "plu": "PLU-001",
        "name": "Dessert 1",
        "quantity": 1,
        "price": 1000,
        "subItems": []
      },
      {
        "plu": "PLU-002",
        "name": "Coffee 1",
        "quantity": 1,
        "price": 800,
        "subItems": [
          {
            "plu": "PLU-003",
            "name": "Sugar 1",
            "quantity": 1,
            "price": 200,
            "subItems": []
          }
        ]
      }
    ],
    "payments": [
      {
        "name": "Deliverect",
        "total": 500
      }
    ]
  }
}
```
```json Failure 1
{
  "statusCode": 500,
  "message": "Bill being processed on POS, cannot apply updates at this moment",
  "closed": false,
}
```
```json Failure 2
{
  "statusCode": 500,
  "message": "Bill already paid and closed. Provided payment rejected.",
  "closed": true,
}
```
```json Failure 3
{
  "statusCode": 400,
  "message": "Bill could not be found."
}
```