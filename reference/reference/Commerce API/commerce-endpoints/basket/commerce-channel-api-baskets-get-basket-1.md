---
api:
  file: commerce.json
  operationId: commerce-channel-api-baskets-get-basket
hidden: false
link:
  new_tab: false
---
### Basket ID

Upon successful basket validation, an `"id"` is returned that can be retrieved via this endpoint.

<HTMLBlock>{`
<div class="callout-banner callout-banner--important">
  <span class="callout-icon"><i class="fa-duotone fa-solid fa-triangle-exclamation"></i></span>
  <p>
    <strong>Basket Validity</strong><br>
    Only baskets which haven't been completed via the checkout process can be retrieved via this endpoint
  </p>
</div>
`}</HTMLBlock>