---
title: How to Create / Update a Basket
excerpt: >-
  This API lets you create and manage baskets by defining the order type and
  adding menu items. Baskets can be updated with customer details, items,
  discounts, or fulfillment before checkout.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Adding items to a basket

`menuId` needs to be provided in order to add items to the basket; see [this guide here ](https://developers.deliverect.com/docs/setting-up-a-store) for more information. unique identifier for each item is the `plu` ; the PLUs are retrieved via [`GET Menus endpoint.`](https://developers.deliverect.com/reference/commerce-channel-api-stores-get-store-menus)

On the example below, the item ordered would be a Burger with Tomatoes as a modifier. At subItem level, the  `"customizationPlu"` refers to the PLU of the modifier group.

```json Item with modifers
  "items": [
    {
      "menuId": "668f7ff64dc853e9c96a4877",
      "plu": "BURGER",
      "quantity": 1,
      "note": "extra salt please"
      ,
      "subItems": [
        {
          "plu": "TOMAT",
          "customizationPlu": "INGRD",
          "quantity": 1
        }
      ]
    }
  ]
```

### Update basket

Certain basket information can be updated after the basket has been created, see the PATCH options documented below;

<HTMLBlock>{`
<a href="https://developers.deliverect.com/v3.0-ordering-experience/reference/basket" target="_blank" class="doc-button">▶ Basket Updates</a>
`}</HTMLBlock>