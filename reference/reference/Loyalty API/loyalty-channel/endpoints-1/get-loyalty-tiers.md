---
api:
  file: loyalty-api.json
  operationId: get-loyalty-tiers
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
## Purpose

Returns the loyalty tiers configured in the loyalty platform sorted by lowest to highest.&#x20;

<HTMLBlock>{`
<div class="callout-banner callout-banner--neutral">
  <span class="callout-icon"><i class="fa-regular fa-square-info"></i></span>
  <p>
    If a location or channel link ID isn't known, the <code class="strong">accountId</code> can be used instead: <code>/loyalty/account/{accountId}/configuration</code>
  </p>
</div>
`}</HTMLBlock>

<br />