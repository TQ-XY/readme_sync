---
title: How to handle Variant Products
deprecated: false
hidden: false
link:
  new_tab: false
metadata:
  robots: index
---
## Introduction

A variant structure applies to products with configurable options, typically of size or quantity which affect its price.&#x20;

## Format

The menu will send a main 'Variant Product' marked as `"isVariant": true` which will have the lowest possible `"price"` across all available options (menu example below)

The available options are listed within a modifier group marked as `"isVariantGroup": true` -

## Display Variant Pricing

The pricing calculation remains as **base price + selected modifier price** but the above variant flags can inform how the menu displays variant items and their prices e.g. UI elements can be modified to show as;

- _"Prices from $8.00"_  - would use the base `"price"` of the variant product to indicate the lowest price
- _"+$3.00"_ - can show on each variant options to indicate the additional cost.

## Ordering Variant Products

A variant product should be included in the order payload much like any other product with modifier options with any additional modifiers chosen.&#x20;

### Example

To further illustrate see example below;

- _"Chicken Tenders"_ has `"isVariant": true` and a base price of `800` (i.e. $8.00).
- _"How many pieces?"_ has `"isVariantGroup": true,` with options like:
  - "3 pieces"- with no added cost → **+$0.00**
  - "6 pieces"  → costs $11.00 adding $3.00 to base price → **+$3.00**

**Note:** Not all POS systems structure variants this way, so these flags may not appear in every menu where size options apply.


<Image src="https://files.readme.io/6625343-Screenshot_2024-07-04_at_11.06.07.png" align="center" width="-32px" border={true} />


<br />

### Menu - Example Payload

Below is how a variant will be sent within the menu payload;

```json Menu Push - Variants
[
    {
        "products":
        {
            "68906df43080e2fd55bcb642":
            {
                "_id": "68906df43080e2fd55bcb642",
                "name": "Chicken Tenders",
                "isVariant": true,
                "plu": "VAR-PROD-1",
                "price": 800,
                "productType": 1,
                "subProducts":
                [
                    "68906df43080e2fd55bcb641"
                ]
            },
            "68906df43080e2fd55bcb63e":
            {
                "_id": "68906df43080e2fd55bcb63e",
                "name": "3 Pieces",
                "plu": "VAR-1-#V0#-",
                "price": 0,
                "productType": 1
            },
            "68906df43080e2fd55bcb63f":
            {
                "_id": "68906df43080e2fd55bcb63f",
                "name": "6 Pieces",
                "plu": "VAR-2-#V300#-",
                "price": 300,
                "productType": 1
            },
            "68906df43080e2fd55bcb640":
            {
                "_id": "68906df43080e2fd55bcb640",
                "name": "9 Pieces",
                "plu": "VAR-3-#V550#-",
                "price": 550,
                "productType": 1
            }
        },
        "modifierGroups":
        {
            "68906df43080e2fd55bcb641":
            {
                "_id": "68906df43080e2fd55bcb641",
                "name": "How many pieces?",
                "isVariantGroup": true,
                "max": 1,
                "min": 1,
                "plu": "MG-VAR-1",
                "productType": 3,
                "subProducts":
                [
                    "68906df43080e2fd55bcb63e",
                    "68906df43080e2fd55bcb63f",
                    "68906df43080e2fd55bcb640"
                ]
            }
        }
    }
]
```

##
