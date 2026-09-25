---
title: How to process multiple menu groups
deprecated: false
hidden: false
metadata:
  robots: index
---
## Introduction

A typical menu comprises multiple categories containing products.

Some customers prefer categories to be further divided into subcategories, which helps to manage larger product offerings (e.g., grocery stores). Deliverect has support for this.

## How

**Step 1.** Each category is created as a new menu in Deliverect. Within each menu, categories are added to represent the subcategories.

**Step 2.** The menus are [added to a menu group](https://help.deliverect.com/en/articles/7978992-publish-a-menu-to-your-delivery-channels).

**Step 3.** The menu group is selected in the [**Publish menus** page](https://help.deliverect.com/en/articles/7978992-publish-a-menu-to-your-delivery-channels). All menus are then published simultaneously as a single JSON file to a channel.

## Example

Below is the desired category structure of a customer:

| Category      | Subcategories                                             |
| :------------ | :-------------------------------------------------------- |
| Snacks        | • Nuts<br />• Sandwiches                                  |
| Beverages     | • Soft drinks<br />• Fruit smoothies<br />• Energy drinks |
| Confectionary | • Chocolate<br />• Sweets                                 |
| Hot Drinks    | • Coffee<br />• Tea                                       |
| Bakery        | • Pastries<br />• Bread<br />• Cakes                      |

To create this structure for **Snacks**, the customer does the following:

1. Create a menu called Snacks.
2. Create the categories:
   1. Nuts
   2. Sandwiches
3. Add the products to the categories.

They then repeat this process for all other categories.

## Menu Payload

When a menu is grouped, the menu JSON would show in the format below.

```json Menu Grouping
[
    {
        "availabilities": [],
        "bundles": {},
        "categories": [],
        "channelLinkId": "65ddbe003110fd505a9e7be4",
        "currency": 2,
        "description": "",
        "descriptionTranslations": {},
        "menu": "FOOD",
        "menuId": "65ddbd64e338f3cb0a8c8150",
        "menuImageURL": "",
        "menuType": 0,
        "modifierGroups": {},
        "modifiers": {},
        "menuTranslations": {},
        "nestedModifiers": true,
        "products": {},
        "productTags": [],
        "snoozedProducts": {},
        "validations": []
    },
    {
        "availabilities": [],
        "bundles": {},
        "categories": [],
        "channelLinkId": "65ddbe003110fd505a9e7be4",
        "currency": 2,
        "description": "",
        "descriptionTranslations": {},
        "menu": "DRINK",
        "menuId": "65ddbd823002c1715c6230a7",
        "menuImageURL": "",
        "menuType": 0,
        "modifierGroups": {},
        "modifiers": {},
        "menuTranslations": {},
        "nestedModifiers": true,
        "products": {},
        "productTags": [],
        "snoozedProducts": {},
        "validations": []
    }
]
```