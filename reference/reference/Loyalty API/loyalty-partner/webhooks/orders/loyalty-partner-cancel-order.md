---
api:
  file: loyalty_webhooks.json
  operationId: loyalty_cancelorder
hidden: false
---
## Purpose

When an order is cancelled. Deliverect sends an event to the configured endpoint, including the key order identifier `"orderId"` along with a cancellation reason where provided. This enables the Loyalty platform  to perform relevant follow-up actions, such as reversing awarded loyalty points or reinstating redeemed points.

### Payload

```json Cancelled Order Example
{
    "orderId": "63********************a7",
    "loyaltyProfileId": "63********************a7",
    "accountId": "6403c0b9ea6956b6f6970c5b",
    "locationId": "61********************b4",
    "channelLinkId": "61********************c3",
    "channelOrderDisplayId": "TESTORDER1",
    "isCancelled": true,
    "cancellationReason": "Customer cancelled.",
    "customer": {
        "email": "email@email.com",
        "phoneNumber": "+32111111111",
        "loyaltyProviderCustomerId": "123",
        "name": "John Doe"
    }
}
```

| Attribute name          | Type    | Description                                                       |
| :---------------------- | :------ | :---------------------------------------------------------------- |
| `orderId`               | string  | Identifier of the order                                           |
| `accountId`             | string  | The merchant's account Id in Deliverect                           |
| `loyaltyProfileId`      | string  | The Id of the profile where the response configuration was stored |
| `locationId`            | string  | The merchant's location Id in Deliverect                          |
| `channelLinkId`         | string  | The merchant's online store Id                                    |
| `channelOrderDisplayId` | string  | Identifier of the order in a human readable format                |
| `isCancelled`           | boolean | Indicates if order is canceled.                                   |
| `cancellationReason`    | string  | Reason of a cancellation.                                         |
| `customer`              | object  | Contains customer details                                         |
| `customer.email`        | string  | Customer's email                                                  |
| `customer.phoneNumber`  | string  | Customer's phone number                                           |
| `customer.name`         | string  | Customer's name (first name + last name).                         |

<br />