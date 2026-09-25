---
api:
  file: fulfilment.json
  operationId: post_fulfillment-updatejob
hidden: true
---
## Purpose

This endpoint updates a delivery job linked to an order, provided the associated DSP supports updates.

### Request  Parameters

<HTMLBlock>{`
<div class="callout-banner callout-banner--neutral">
  <span class="callout-icon"><i class="fa-regular fa-square-info"></i></span>
  <p>

 Only the fields intended for modification must be included. The <code>\`deliveryJobId\`</code> field must always be provided.
  </p>
</div>
`}</HTMLBlock>

| Field               | Type   | Definition                                                                                                                                   |
| :------------------ | :----- | :------------------------------------------------------------------------------------------------------------------------------------------- |
| deliveryJobId       | string | Id of the deliveryJob                                                                                                                        |
| deliveryAddress     | object | Object including street, city, postalCode, source, coordinates.                                                                              |
| dropoffInstructions | string | The initial deliveryAddress.extraAddressInfo can be changed using dropoffInstructions                                                        |
| deliveryTime        | string | Timestamp is in UTC yyyy-MM-ddTHH:mm:ssZ all time values in our API are in UTC time as per [ISO8601](https://en.wikipedia.org/wiki/ISO_8601) |
| pickupTime          | string | Timestamp is in UTC yyyy-MM-ddTHH:mm:ssZ all time values in our API are in UTC time as per[ ISO8601](https://en.wikipedia.org/wiki/ISO_8601) |
| driverTip           | int    | Tip intended for the driver.  It should be sent as an integer with 2 decimal digits e.g. 1 euro would be sent as 100.                        |

<HTMLBlock>{`
<div class="callout-banner callout-banner--neutral">
  <span class="callout-icon"><i class="fa-regular fa-square-info"></i></span>
  <p>

Validation is performed only when the DSP supports updates; otherwise, the endpoint returns <code>501 Not Implemented</code>
  </p>
</div>
`}</HTMLBlock>

```json Example Request
{
    "deliveryJobId": "67**********************30",
    "deliveryAddress": {
      "street": "Praceta Aldeia do Meio, 2740 Porto Salvo, Portugal",
      "city": "Porto Salvo",
      "postalCode": "2740",
      "source": "Praceta Aldeia do Meio, 2740 Porto Salvo, Portugal, 2740, Porto Salvo, Portugal"
    },
    "dropoffInstructions": "apartment 17; Lisboa",
    "deliveryTime": "YYYY-MM-DDTHH:mm:ss.SSSSSSZ",
    "pickupTime": "YYYY-MM-DDTHH:mm:ss.SSSSSSZ",
    "driverTip": 0
  }'
```

### Eligibility Rules

| Field                     | Rule                                                               |
| :------------------------ | :----------------------------------------------------------------- |
| deliveryTime / pickupTime | Update allowed when a status ≤ 83                                  |
| deliveryAddress           | Update allowed when a status ≤ 83                                  |
| dropoffInstructions       | Update allowed when status ≤ 89                                    |
| driverTip                 | Update allowed within 48h of delivery, and amount cannot decrease. |

```json Example Sucess Response
{
    "deliveryJobId": "6993924cc83efc95cc331f93",
    "updated": true
}
```
```json Example Failure Response
{
    "errors": {
        "driverTip": "Driver tip cannot be reduced."
    }
}
```