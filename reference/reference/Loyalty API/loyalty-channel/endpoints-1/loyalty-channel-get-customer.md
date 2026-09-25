---
api:
  file: loyalty-api.json
  operationId: loyalty-channel-get-customer
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
## Purpose

This endpoint returns customer information by email and phone number from the loyalty provider system.

<HTMLBlock>{`
<div class="callout-banner callout-banner--neutral">
  <span class="callout-icon"><i class="fa-regular fa-square-info"></i></span>
  <p>
    If a location or channel link ID isn't known, the <code class="strong">accountId</code> can be used instead: <code>/loyalty/account/{accountId}/configuration</code>
  </p>
</div>
`}</HTMLBlock>