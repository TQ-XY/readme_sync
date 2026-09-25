---
title: How to handle maximum limit per product
deprecated: false
hidden: false
metadata:
  robots: index
---
## Introduction

Sometimes, merchants would like to restrict the number of products that can be sold within one order. For example, pharmaceuticals or medications often have legal limits to how many can be sold per customer order.

## **Format**

A customer can define a 'Max order limit' as in below screenshot. This will show in the menu push in the product information as a multiMax value e.g. `"multiMax": 1,` channels should then ensure the product can only be sold one time in a given order basket.

## Testing

To test this scenario, you can add this function via 'Products', navigating to any product settings page and under "Max order limit" apply a numerical value.

<HTMLBlock>{`
<div class="callout-banner callout-banner--neutral">
  <span class="callout-icon"><i class="fa-regular fa-square-info"></i></span>
  <p>
    <strong>Product Only Attribute</strong><br>
   This applies only to Products (<code>"productType":1</code>) only.
  </p>
</div>
`}</HTMLBlock>

<br />

![](https://files.readme.io/bc1784e-B92FC570-F97E-45BC-8202-C058092EB240_1_201_a.jpeg)

##
