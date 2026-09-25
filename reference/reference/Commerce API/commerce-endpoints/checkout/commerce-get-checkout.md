---
api:
  file: commerce.json
  operationId: get_commerce{accountId}checkouts{checkoutId}-1
hidden: false
---
### Purpose

Returns a checkout session by ID. This can be used to poll the status of a checkout session providing order placement details.

### Checkout Status

A successful checkout will show `status` as `open` and once processed into the POS will update to `completed` or to `failed` if an unexpected error occurs.

As an alternative method to retrieving the `status` listening to the [Checkout Update](ref:commerce-api-checkout-update) webhook will deliver the final checkout status in real time as soon as it is updated