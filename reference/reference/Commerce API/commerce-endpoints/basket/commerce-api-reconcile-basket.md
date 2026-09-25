---
api:
  file: commerce.json
  operationId: post_commerce-accountid-baskets-basketid-reconcile
hidden: false
link:
  new_tab: false
metadata:
  robots: index
---
## Purpose

Performs a full recalculation of the basket, including all data points from downstream services such as loyalty and coupons. As it updates the basket with the results, including any adjusted totals, it's intended purpose is to be used prior to checkout, so that where issuing final payment, the total amounts charged are fully correct.

Format

When sending a request to reconcile a basket, there are two possible outcomes;

**Basket Updates** - If any necessary corrections are needed based on downstream calculations from third parties these will be updated and persisted in the basket<br /><br />**Validation errors** - If for any reason the basket content causes issues in resolving with downstream services, an error will be returned to indicate the issue

<HTMLBlock>{`
<div class="callout-banner callout-banner--neutral">
  <span class="callout-icon"><i class="fa-regular fa-square-info"></i></span>
  <p>
    <strong>Validating without updates</strong><br>
    For the purpose of checking for any basket errors, without persisting any updates, use the <a href="https://developers.deliverect.com/v3.0-ordering-experience/reference/validate-basket">Validate Basket</a> endpoint.
  </p>
</div>
`}</HTMLBlock>