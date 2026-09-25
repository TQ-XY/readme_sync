---
api:
  file: deleteCustomer_webhooks.json
  operationId: deletecustomer_delete
hidden: true
---
## Purpose

This webhook delivers customer deletion requests which identify the customer by their unique `customerId` allowing an asynchronous response to confirm the deletion request status via <Anchor target="_blank" href="https://developers.deliverect.com/v3.0/update/reference/deletion-customer-data-endpoint">Customer Deletion Status</Anchor>

### Request body

| Field           | Type     | Required | Description                                                                                                                                |
| :-------------- | :------- | :------- | :----------------------------------------------------------------------------------------------------------------------------------------- |
| **customerId**  | string   | Yes      | Unique identifier of the customer                                                                                                          |
| **accountId**   | string   | Yes      | Deliverect account identifier                                                                                                              |
| **responseSLA** | integer  | Yes      | Expected response timeframe in days                                                                                                        |
| **requestDate** | datetime | Yes      | Timestamp of request creation                                                                                                              |
| **requestId**   | string   | Yes      | Unique Id for the deletion request.<br />The requestId is required for proper tracking and must be returned unchanged in the outcome call. |