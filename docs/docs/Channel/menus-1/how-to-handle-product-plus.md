---
title: How to handle product PLUs
deprecated: false
hidden: false
metadata:
  robots: index
---
## Introduction

A product can exist on its own, but also under another product. When that happens, the product may not have the same price as the original product. Because of this, you may see products with the same <Glossary>PLU</Glossary> but with number signs (**#**) added.

Similarly, a structure of a PLU similar to **-#..#-** can be received after publishing a menu. This means that one of the sub-products contains an attribute different from what is on the menu (such as a different price, modifiers inactive in one place, etc.)

## Example

A product called "Fanta" with a price of €1.50 has the following data:

```json Example
60b8a345a2c6d5c0f9a8306e": {
"name": "Fanta",
"description": "330ml",
...
"_id": "60b8a345xxx0f9a8306e",
"account": "60ae589bxxxxe232a2d99",
"location": "60ae5xxxb637e232a2db1",
"productType": 1,
"plu": "DRN-03",
"price": 150,
...
```

The same product as part of a bundle is shown below. Notice how the PLU for this product is `DRN-03###`.

```json Example
"_id": "60e3110c2bd73d0eec98cd21",
"account": "60ae589xxxx232a2d99",
"location": "60ae5xxxxb637e232a2db1",
"productType": 1,
"plu": "DRN-03###",
"price": 0
```

<Callout icon="📘" theme="info">
  ### referenceId

  We include the original PLU in the menu push payload via the attribute "referenceId" for you to be able to always map the original PLU. For example, if you want to track sales of that specific item for loyalty purposes.
</Callout>

<Glossary>Snoozing</Glossary> the product with the PLU `DRN-03` from the **Snooze** tab of your Deliverect test account would also snooze all other instances of the product.

By publishing the menu, you would see that under the object `snoozed_items`.

<Callout icon="🚧" theme="warn">
  ### Creating an order

  When creating an order always include the PLU in the item information and not the `referenceId`, which refers to the original PLU.
</Callout>

<br />