---
api:
  file: dispatch_webhooks.json
  operationId: post_dispatch-updatejob
hidden: false
link:
  new_tab: false
---
## Purpose

Webhook called when an existing delivery job changes. This can be because the pickup time needs to change, items to add, dropoff locations are added or removed, etc.

<HTMLBlock>{`
<div class="callout-banner callout-banner--neutral">
  <span class="callout-icon"><i class="fa-regular fa-square-info"></i></span>
  <p>

    The Update Delivery Job URL needs to be standardised, i.e.
    <strong>the same URL should be used for every customer installation</strong>.
  </p>
</div>
`}</HTMLBlock>

### Request Example

```json Update Delivery Job
{
    "_id": "5c8fbfd3c6489f00010e50d1",
    "externalJobId": "ABC123",
    "deliveryLocations": [
        {
            "deliveryId": "ABC567",
            "orderId": "5f47a223280a29046404e2af",
            "channelOrderDisplayId": "MT4YVTPL",
            "deliveryTime": "2019-02-20T16:45:00.000000Z",
            "packageSize": "small",
            "orderDescription": "hot food",
            "company": "BrainQuantums",
            "name": "V. Bertels",
            "street": "Refugehof",
            "streetNumber": "49",
            "postalCode": "9001 AB",
            "city": "Leusden",
            "phone": "+32123456789",
            "latitude": "52.370216",
            "longitude": "4.895168",
            "deliveryRemarks": "please knock 3x, baby is sleeping",
            "payment": {
                "orderIsAlreadyPaid": false,
                "amount": 1500,
                "paymentType": 2,
                "paysWith": 2000
            }
        },
        {
            "orderId": "5f47a484d08f00f30f04e7eb",
            "channelOrderDisplayId": "82DE5",
            "deliveryTime": "2019-02-20T16:45:00.000000Z",
            "packageSize": "large",
            "orderDescription": "hot food",
            "name": "C. Landman",
            "street": "Prinsengracht",
            "streetNumber": "198",
            "postalCode": "9101 CG",
            "city": "Leusden",
            "phone": "+3212987654",
            "latitude": "52.370216",
            "longitude": "4.895168",
            "deliveryRemarks": "",
            "payment": {
                "orderIsAlreadyPaid": true,
                "amount": 1000,
                "paymentType": 3
            }
        }
    ]
}
```

### Example Response

```json Example Response
{
  "jobId": "5f47a0af620ae2fad0a8f62c",
  "externalJobId": "ABC123",
  "canDeliver": true,
  "pickupTimeETA": "2019-02-20T16:20:42.000000Z",
  "courier": {
    "courierId": "D1234",
    "firstName": "Delivery",
    "lastName": "Rider",
    "phoneNumber": "0032494112233",
    "transportType": "bike"
  },
  "deliveryLocations": [
    {
      "deliveryId": "ABC567",
      "orderId": "5f47a223280a29046404e2af",
      "channelOrderDisplayId": "MT4YVTPL",
      "deliveryTimeETA": "2019-02-20T16:48:00.000000Z",
      "packageSize": "small",
      "latitude": "52.370216",
      "longitude": "4.895168",
      "deliveryRemarks": ""
    },
    {
      "deliveryId": "ABC890",
      "orderId": "5f47a484d08f00f30f04e7eb",
      "channelOrderDisplayId": "82DE5",
      "deliveryTimeETA": "2019-02-20T16:53:00.000000Z",
      "packageSize": "large",
      "latitude": "52.370216",
      "longitude": "4.895168",
      "deliveryRemarks": ""
    }
  ],
  "distance": 4500,
  "duration": 319,
  "price": {
    "price": 750,
    "taxRate": 10000
  }
}
```