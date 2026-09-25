---
api:
  file: commerce.json
  operationId: commerce-channel-api-baskets-update-basket-items
hidden: false
---
### Purpose

Update existing items with changes to e.g.  "quantity" or "note' or add new items to the basket.

<HTMLBlock>{`
<div class="callout-banner callout-banner--neutral">
  <span class="callout-icon"><i class="fa-regular fa-square-info"></i></span>
  <p>
    <strong>Patch Behaviour</strong><br>
  Each patch will fully replace the curent basket content, to update or add new products, retain the existing basket items.
  </p>
</div>
`}</HTMLBlock>

<br />

<br />