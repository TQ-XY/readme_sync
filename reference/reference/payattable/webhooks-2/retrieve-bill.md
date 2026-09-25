---
api:
  file: payattable-webhooks.json
  operationId: get_billid
hidden: true
link:
  new_tab: false
metadata:
  robots: index
---
<HTMLBlock>{`
<div style="background: #F00; font-weight: bold; color: #FFF; padding: 10px">Please do not yet share this information to anyone else.<br />The below spec might still be prone to changes.</div>
`}</HTMLBlock>

{{YourSyncBillsWebhookURL}}?billId={string}ℴId={string}\&tableId={string}\&modifiedSince={datetime}\&createdSince={datetime}∈cludeClosed={boolean}

<br />

Although we expect bill updates using the [POST Bill Update](ref:post-bill-update) webhook, there might be occasions where we did not receive an update (e.g. because there was a temporary hickup in network communication). We might also want to ensure we have the latest state of a bill when doing sensitive processes like payment.

The call will be made with at least one of below parameters (but can be called with multiple parameters combined):

| Parameter       | Description                                                                                                                                                                                                                            | Type               |
| :-------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :----------------- |
| `billId`        | Your ID of the bill. It is the ID which was communicated back as `receiptId` to us upon [sending an order](ref:post-orders-webhook), as described in the [Update Order Status expected return](ref:update-order-status).               | string             |
| `orderId`       | The Deliverect Order ID (in case the bill was created via Deliverect). This ID will be used in case we did (not yet) get back a `receiptId`, it was communicated to you during the [POST Orders webhook call](ref:post-orders-webhook) | string             |
| `tableId`       | The ID of the table against which the order/bill was created. The ID will be the one communicated by the POS on webhook [GET Tables](ref:get-tables).                                                                                  | string             |
| `modifiedSince` | Returned bills should be modified since the provided timestamp (format YYYY-MM-ddTHH:mm:ss.SSSZ).                                                                                                                                      | string($date-time) |
| `createdSince`  | Returned bills should have been created since the provided timestamp (format YYYY-MM-ddTHH:mm:ss.SSSZ).                                                                                                                                | string($date-time) |
| `includeClosed` | If set to true, we also expect the closed bills. If set to false, only the non-closed bills should be returned. If no parameter is provided, you can assume we do not want the closed bills.                                           | boolean            |

<Callout icon="📘" theme="info">
  ### UTC Time

  Note that all time values in our API are in UTC time.
</Callout>

In several scenarios there might be only one result (e.g. when calling with `billId` or `orderId`), but you can always return us the result in an array, containing only one entry. If no matches can be found on your side, you can return an empty array.

```json Get bill from the POS by bill id
curl --location --request GET '{{YourSyncBillsWebhookURL}}?billId=R29532LF'
```
```json Get bill from the POS by table id
curl --location --request GET '{{YourSyncBillsWebhookURL}}?tableId=T1'
```
```text Get bill from the POS by deliverect order id
curl --location --request GET '{{YourSyncBillsWebhookURL}}?orderId=62********************2e'
```
```Text Get all bills modified since
curl --location --request GET '{{YourSyncBillsWebhookURL}}?modifiedSince=2022-05-04T09:11:51.166000Z&includeClosed=true'
```

Below an example response. An explanation to the fields can be found on the [Get Bills by ID](ref:bill-by-id), as they are a one-on-one match. The only exception is the status field which we will expect from your return as well (which can be OPEN (20), CLOSED (90) or DELETED (100)).<br />

```json Example Response
{
  "bills": [{
    "id": "R29532LF",
    "status": 20,
    "table": {
      "id": "T1",
      "name": "Table 1"
    },
    "posSpecificData": {
      "id": "POSID123456",
    },
    "createdAt": "2022-05-04T09:11:51.166000Z",
    "lastUpdated": "2022-05-04T09:13:17.166000Z",
    "closedAt": "1970-00-00T00:00:00.000000Z",  
    "decimalDigits": 2,
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
    "totalDue": 400,
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
        "paymentType": "Cash",
        "totalAmount": 400
      }
    ]
  }]
}
```

<br />