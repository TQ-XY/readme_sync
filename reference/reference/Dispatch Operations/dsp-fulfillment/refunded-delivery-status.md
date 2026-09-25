---
api:
  file: fulfilment.json
  operationId: refunds-1
hidden: true
---
## Purpose

This endpoint is used to get refund data after processing it.

## HMAC - Headers

| Key              | Value                                                                                                                             |
| :--------------- | :-------------------------------------------------------------------------------------------------------------------------------- |
| Content-type     | application/json                                                                                                                  |
| X-HMAC-Signature | With every call made to this endpoint, the HMAC signature should uses the SHA256 cryptographic hash function with base64 encoding |
| X-HMAC-Partner   | This is a pre-shared by Deliverect value to identify the partner                                                                  |

## Request

At least one the following fields is required

| Field                 | Type   | Notes                                            |
| :-------------------- | :----- | :----------------------------------------------- |
| deliveryExternalJobId | string | The job ID of the delivery platform (preferred). |
| deliveryJobId         | string | Deliverect job ID.                               |

```json Example Request
{
  "deliveryExternalJobId": "your-external-job-id-123"
}

```

<HTMLBlock>{`
<div class="callout-banner callout-banner--neutral">
  <span class="callout-icon"><i class="fa-regular fa-square-info"></i></span>
  <p>
    If both values are provided, <code>deliveryExternalJobId</code> will be used used
  </p>
</div>
`}</HTMLBlock>

### Response Parameters

| Field              | Type    | Description                                                                                             |
| :----------------- | :------ | :------------------------------------------------------------------------------------------------------ |
| deliveryJobId      | string  | Deliverect delivery job ID.                                                                             |
| deliveryExternalId | string  | The job ID of the delivery platform (preferred).                                                        |
| status             | string  | Refund status Possible values: `COMPLETED`, `FAILED`, `INCOMPLETE`, `PENDING`                           |
| amount             | integer | Refund amount sent as an integer with 2 decimal digits,  for example, 1 euro would be sent as 100.      |
| completedAt        | string  | Timestamp is in UTC yyyy-MM-ddTHH:mm:ssZ  time as per [ISO8601](https://en.wikipedia.org/wiki/ISO_8601) |

```json Success Response example
{
  "deliveryJobId": "507f1f77bcf86cd799439011",
  "deliveryExternalId": "your-external-job-id-123",
  "status": "COMPLETED",
  "amount": 599,
  "completedAt": "2026-01-28T14:30:00.000Z"
}

```
```json No refund /Job Found
{}
```

<HTMLBlock>{`
<div class="callout-banner callout-banner--neutral">
  <span class="callout-icon"><i class="fa-regular fa-square-info"></i></span>
  <p>
   If no refund or job is found, the response will be an empty object <code>{}</code>
  </p>
</div>
`}</HTMLBlock>

| Status     | Description                                                                   |
| :--------- | :---------------------------------------------------------------------------- |
| COMPLETED  | The refund was completed by the order source responsible as per the decision. |
| FAILED     | The refund was not actioned at the decision of the order source responsible.  |
| INCOMPLETE | The response time timed out and no update was received                        |
| PENDING    | Final outcome not yet received from the order source                          |