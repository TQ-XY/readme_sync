---
api:
  file: deletecustomer.json
  operationId: post_fulfillment-deleteuserdata-outcome
hidden: true
---
## Purpose

The DSP system must notify Deliverect of the final result of the deletion request.

## HMAC - Headers

| Key              | Value                                                                                                                          |
| :--------------- | :----------------------------------------------------------------------------------------------------------------------------- |
| Content-type     | application/json                                                                                                               |
| X-HMAC-Signature | With every call made to this endpoint, the HMAC signature should uses the SHA256 cryptographic hash function with hex encoding |
| X-HMAC-Partner   | This is a pre-shared by Deliverect value to identify the partne                                                                |

<br />

## Request Body

| Field           | Type   | Required | Description                                                        |
| :-------------- | :----- | :------- | :----------------------------------------------------------------- |
| requestId       | string | Yes      | Unique identifier of the deletion request                          |
| requestOutcome  | string | Yes      | Result status : `Completed`, `Failed`, `Incomplete`, or `Pending`. |
| rejectionReason | string | No       | Optional reason if failed or incomplete                            |