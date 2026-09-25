---
title: How to handle Product Allergens/Metadata
deprecated: false
hidden: false
metadata:
  robots: index
---
## Introduction

A product can be set with additional metadata including; **allergens**/**tags**, **calories**, **nutritional** and **supplemental information**. This can be for general customer reference, but certain regional legislation may require this information to be included as part of the product data displayed on digital ordering platforms.<br />Product Model

## Product tags

A product can have one or more product tag and these are stored with key `productTags`. Product tags are used to indicate consumable types and or allergens, which your channel should show in menus to customers.

To retrieve a list of up to date tags see the endpoint [GET Allergens & Tags](https://developers.deliverect.com/reference/get-allergens-and-tags)

<Cards>
  <Card title="GET Allergens & Tags" href="https://developers.deliverect.com/v1.1-restaurants/reference/allergens-and-tags" icon="fad fa-gear-api" target="_blank">
    Retrieve all available allergens and tags supported in Deliverect.
  </Card>

  <Card title="Product Allergens & Tags" href="https://developers.deliverect.com/page/custom-tags-and-allergens" icon="fad fa-peanuts" target="_blank">
    A complete list of current allergens and tags
  </Card>
</Cards>

See example snippet below which shows a "Chicken Sate" product as containing Nuts  and Eggs via the array of `productTags`

```json Tags Example
{
  "68908441bf2d317437e96ab4": {
    "name": "Chicken Sate",
    "description": "Product contains nuts",
    "productTags": [
      104,
      109
    ]
  },
```

## Calories

If the calories are sent from the POS or added in Deliverect, it will be sent to channel in Menu Push as per the sample below

| Parameter           | Meaning                                                                                                       | type             |
| :------------------ | :------------------------------------------------------------------------------------------------------------ | :--------------- |
| `calories`          | This is the base calorie amount, where a maximum calories is set, this should be interpreted as the 'minimum' | integer or float |
| `caloriesRangeHigh` | The maximum calorie amount of an item                                                                         | integer or float |

```json
"62334e600cf177afb8bad2b1": {
  "name": "Cheeseburger",
  "description": "Burger with Cheese",
  "calories": 500,
  "caloriesRangeHigh": 750              ...
}
```

## Nutritional Information

If nutritional information is sent by the POS, you will also receive it for each product via the menu push. The unit of the values is gram.

Notice, that ingredients and additives are lists of strings. You may or may not receive food business information (fbo) depends on local regulation.

### Product Example

See example of a single item with all additional info included, for a complete reference to each attribute, see the full menu model via the link below;

<HTMLBlock>{`
<a href="https://developers.deliverect.com/page/channel-menu-model" target="_blank" class="doc-button">▶ Menu Model</a>
`}</HTMLBlock>

```json Product Example
{
  "61********************c3": {
    "_id": "61********************c3",
    "name": "Ginger Beer",
    "description": "Made with locally grown ginger and sugarcane",
    "beverageInfo": {
      "caffeine": 13,
      "alcohol": 1
    },
    "calories": 500,
    "caloriesRangeHigh": 750,
    "kJ": 2092,
    "kJRangeHigh": 3138,
    "capacityUsages": [],
    "deliveryTax": 1200,
    "eatInTax": 1200,
    "imageUrl": "https://resizer.staging.deliverect.com/iFUJT73YtMe1pChj29lAFUt_NBknsyTu5Hlr6NvA5NI/rt:fill/g:ce/el:0/aHR0cHM6Ly9zdG9yYWdlLmdvb2dsZWFwaXMuY29tL2lrb25hLWJ1Y2tldC1zdGFnaW5nL2ltYWdlcy81ZmY2ZWUwODkzMjhjOGFlZmVlYWJlMzMvZ2luZ2VyYmVlci02MjI4NTU0OGRiNTk4NjAwMWViZjU4ZDEuanBn.jpg",
    "max": 0,
    "min": 0,
    "multiply": 1,
    "nutritionalInfo": {
      "fat": 2,
      "sugar": 2,
      "saturatedFat": 1.5,
      "carbohydrates": 1.5,
      "protein": 2,
      "salt": 2,
      "servingSize": {
        "amount": 3,
        "unitType": 3,
        "countUnitDescription": "g"
      },
      "netQuantity": {
        "amount": 12,
        "unitType": 1,
        "countUnitDescription": "g"
      }
    },
    "packaging": {
      "count": 1,
      "reusable": true,
      "storageInstructions": "Keep cool"
    },
    "plu": "DRNK-03",
    "price": 500,
    "productTags": [
      10,
      14,
      18,
      23,
      128
    ],
    "productType": 1,
    "subProducts": [],
    "takeawayTax": 1200,
    "supplementalInfo": {
      "legalName": "Carbonated Soft Drink",
      "instructionsForUse": "Best served chilled",
      "ingredients": [
        "Carbonated Water",
        "Sugar",
        "Colour (Caramel E150d)",
        "Phosphoric Acid",
        "Natural Flavourings"
      ],
      "additives": [
        "Artificial Food Coloring",
        "Sodium Nitrite"
      ],
      "prepackaged": true,
      "deposit": 100,
      "fbo": {
        "name": "The Coca-Cola Company",
        "address": "Atlanta, GA, USA"
      }
    },
    "gtin": [
      "8712345000103",
      "74993001078"
    ]
  }
}
```

##