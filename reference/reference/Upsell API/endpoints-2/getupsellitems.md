---
api:
  file: upsells.json
  operationId: getUpsellItems
hidden: false
---
## Purpose

Provides upsell recommendations based on the items in an order

## Format

Recommendations are generated using two signals;

- **Analysis of the brand's historical order data** - which products are genuinely bought together, beyond simple popularity (individual customer history isn't factored)
- **An AI-based analysis of the brand menu** - which products are comparable to or complementary to one another

A recommendation must be supported by both signals to be returned, which keeps suggestions specific to each brand's menu and the behaviour of their customer base.

The response will also filter on 'live menu' content, meaning that only products currently online and not snoozed at the specific location are recommended.

<HTMLBlock>{`
<div class="callout-banner callout-banner--neutral">
  <span class="callout-icon"><i class="fa-regular fa-square-info"></i></span>
  <p>
   Recommendations are product-level only, modifiers are not returned
  </p>
</div>
`}</HTMLBlock>

## Upsell Overrides

Brands can control the recommendations via Upsell Overrides, which allow specific products to be "pinned" so they are always suggested at a given location. This aids in selling new promotions or seasonal items which wouldn't factor in order history rankings.

Overrides work at the individual product level (not category), are merged ahead of the automatic suggestions rather than replacing them, and duplicates are removed automatically.
