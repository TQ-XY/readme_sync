---
title: How to Handle Multiple Menus
deprecated: false
hidden: false
metadata:
  robots: index
---
## Overview

Deliverect customers can manage multiple menus in their account, publishing them according to different contexts, for example:

- A different menu per ordering platform (e.g. First Party vs. Third Party).
- A different menu per fulfilment type (Delivery, Pickup, Eat-in or Curbside)

On platforms which support multiple fulfilment types, end-consumers can switch between menus and be shown different content which can cover a wide range of variables, for example;

- Available items (e.g. Soda Fountain available for Pickup but not Delivery).
- Pricing strategies (e.g. applying a markup price on Delivery prices but not on Eat-in prices)

When using the Commerce API to [GET Store Menu(s)](https://developers.deliverect.com/v3.0-ordering-experience/reference/commerce-get-menus), the response will include the types of variations above, the following sections will explain how to identify these.

## Menu Type

The menu endpoint returns an array of menus. If the customer has chosen to publish multiple menus, each menu will be included and uniquely identified by it's `"menuId"`

The `"menuType"` field (integer) indicates which fulfillment type the menu is intended for:

| Name                | Integer Value |
| :------------------ | :------------ |
| Delivery and pickup | 0             |
| Delivery            | 1             |
| Pickup              | 2             |
| Eat-in              | 3             |
| Curbside            | 4             |

## Price Variations

Different menus may define different prices for the same product, depending on the fulfillment type.

In the example below, two menus are returned:

- `menuType`: 2 → **Pickup**
- `menuType`: 3 → **Eat-in**

Note that the product "Garlic Bread" is the same across both menus with the exception of the `"price"` value.

When displaying menus, this means depending on the user’s chosen fulfillment type, the specific menu content should display.

```json Multiple Menu Sample
[
    {
        "menu": "Burger Bar - Kiosk",
        "menuId": "61********************59",
        "menuType": 2,
        "products":
        {
            "65********************29":
            {
                "id": "65********************29",
                "plu": "11302",
                "name": "Garlic Bread",
                "price": 850
            }
        }
    },
    {
        "menu": "Burger Bar - Website",
        "menuId": "65********************32",
        "menuType": 3,
        "products":
        {
            "62********************22":
            {
                "id": "62********************22",
                "plu": "11302",
                "name": "Garlic Bread",
                "price": 950
            }
        }
    }
]
```

## Menu Model

For full details on the menu structure, see. the Menu Model below;

<HTMLBlock>{`
<a href="https://developers.deliverect.com/page/channel-menu-model" target="_blank" class="doc-button">▶ Menu Model</a>
`}</HTMLBlock>
