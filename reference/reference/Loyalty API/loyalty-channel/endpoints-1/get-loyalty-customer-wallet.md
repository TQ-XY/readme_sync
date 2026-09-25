---
api:
  file: loyalty-api.json
  operationId: get-loyalty-customer-wallet
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
## Purpose

Retrieve the loyalty points and cash amounts for a customer.

<HTMLBlock>{`
<div class="callout-banner callout-banner--neutral">
  <span class="callout-icon"><i class="fa-regular fa-square-info"></i></span>
  <p>
    If a location or channel link ID isn't known, the <code class="strong">accountId</code> can be used instead: <code>/loyalty/account/{accountId}/configuration</code>
  </p>
</div>
`}</HTMLBlock>

## Response

Returns `200` when a customer was found or `404` when the customer does not exist.