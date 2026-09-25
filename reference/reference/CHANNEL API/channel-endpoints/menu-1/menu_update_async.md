---
api:
  file: channel.json
  operationId: post_channelname-menustatus-id
hidden: false
---
## Purpose

For channels configured to handle menu publish requests asynchronously, this endpoint is used to provide the final menu update status. This gives customers full visibility on menu publish events and their success, particularly where bulk operations across multiple locations are actioned.

## Format

Channel partners should POST to the provided `"callback"` endpoint with the final menu update status of either;

| Value    | Description                                                                                                                                              |
| :------- | :------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `ONLINE` | Signifies that the menu is now successfully published and available to users. No additional information is required in the request body for this status. |
| `FAILED` | Indicates that the operation has failed. Partners should include relevant error details or error codes in the request body to assist in troubleshooting. |

**Path Parameters**

| Parameters    | Description                                                                                                                                   | Type   |
| :------------ | :-------------------------------------------------------------------------------------------------------------------------------------------- | :----- |
| `channelName` | Represents the case-sensitive <Glossary>Scope</Glossary> provided. If a `channelname` used is invalid the request is considered unauthorised. | string |
| `_id`         | This id shown in the callback url is a unique identifier of the menu publish request                                                          | string |

**Body Parameters**  (Fields marked with (<span style={{ color: "red" }}> * </span>)are required.

| Parameters                                         | Description                  | Type   |
| :------------------------------------------------- | :--------------------------- | :----- |
| `status` <span style={{ color: "red" }}> * </span> | status of the menu operation | string |
| `comment`                                          | any comment (optional)       | string |

## Response Time

Please ensure that the menu is published successfully within a maximum of **30 minutes**. If the process exceeds this time limit, Deliverect will automatically set the operation as "Failed"

**Stores (multiple channel IDs)**

Currently we support menu publishing for one store/channelLinkId. In the payload you will find "stores" array where in the future you may receive more `channelLinkIds`.

```json Stores
"stores": [
  "649a**********9ea9"
]
```

## Synchronous vs Asynchronous

Partners switching to an asynchronous flow should note the differences from the synchronous flow. These are shown in the JSON example belows, can be summarized as follows;

- **Asynchronous:** Has `"menus" ` , `"stores"` and `"callback"` as keys within a `"body"`
- **Synchronous:** Shows an array of properties e.g. `"availabilities"`, `"categories"`, `"modifierGroups"` etc.

<HTMLBlock>{`
<div class="callout-banner callout-banner--neutral">
  <span class="callout-icon"><i class="fa-regular fa-square-info"></i></span>
  <p>
    <strong>Menu Model</strong><br>
    All menu content within <code>"menus"</code> follows the same menu model documented <a href="https://developers.deliverect.com/page/menu-glossary" target="_blank" rel="noopener noreferrer">here</a>
  </p>
</div>
`}</HTMLBlock>

```json Async Menu Push
{
    "body": {
        "menus": [
            {
                "availabilities": [],
                "modifierGroups": {},
                "categories": []
                // ... other properties
            }
        ],
        "stores": [
            "64*******************a9"
        ],
        "callback": "https://api.staging.deliverect.com/{channelName}/menuStatus/64*******************2d"
    }
}
```
```json Sync Menu Push
[
    {
        "availabilities": [],
        "modifierGroups": {},
        "categories": [],
        // ... other properties
    }
]
```
```json Full Async Menu Push
"body": {
    "menus": [
        {
            "availabilities": [
                {
                    "dayOfWeek": 1,
                    "endTime": "17:00",
                    "startTime": "10:00"
                },
                {
                    "dayOfWeek": 2,
                    "endTime": "10:00",
                    "startTime": "09:00"
                },
                {
                    "dayOfWeek": 2,
                    "endTime": "12:00",
                    "startTime": "11:00"
                }
            ],
            "bundles": {},
            "categories": [
                {
                    "_id": "6464**********6dd6010",
                    "name": "test",
                    "description": "",
                    "descriptionTranslations": {},
                    "nameTranslations": {},
                    "account": "61c3**********dd0306de1",
                    "posLocationId": "",
                    "posCategoryType": "",
                    "posCategoryId": "",
                    "imageUrl": "",
                    "subCategories": [],
                    "products": [
                        "649ea**********db4a92c"
                    ],
                    "availabilities": [],
                    "level": 1,
                    "menu": "6464**********f80406",
                    "sortedChannelProductIds": [],
                    "subProducts": [
                        "649eab**********6cdb4a92c"
                    ],
                    "subProductSortOrder": []
                }
            ],
            "channelLinkId": "649ad021949cfa36470f9ea9",
            "currency": 1,
            "description": "",
            "descriptionTranslations": {},
            "menu": "test",
            "menuId": "64648bd2a28d59a83ff80406",
            "menuType": 1,
            "modifierGroups": {
                "64776b3879e36bee40db37b0": {
                    "_id": "64776b3879e36bee40db37b0",
                    "name": "Cooking instructions",
                    "description": "Cooking Instructions",
                    "descriptionTranslations": {
                        "ar": "تعليمات الطبخ"
                    },
                    "nameTranslations": {
                        "en": "Cooking Instructions",
                        "ar": "تعليمات الطبخ"
                    },
                    "account": "61c3070ae41eefadd0306de1",
                    "capacityUsages": [],
                    "deliveryTax": 6000,
                    "imageUrl": "",
                    "location": "61c30761e41eefadd03072af",
                    "max": 1,
                    "min": 1,
                    "multiply": 1,
                    "plu": "MOD-01",
                    "posCategoryIds": [
                        "POS-CAT-001"
                    ],
                    "posProductCategoryId": "",
                    "posProductId": "POS-ID-009",
                    "price": 900,
                    "productTags": [],
                    "productType": 3,
                    "subProducts": [
                        "64776b3879e36bee40db37ba",
                        "64776b3879e36bee40db37bc",
                        "64776b3879e36bee40db37be"
                    ],
                    "takeawayTax": 6000,
                    "parentId": "64776b3879e36bee40db37ae",
                    "snoozed": false,
                    "subProductSortOrder": []
                },
                "64776b3879e36bee40db37b2": {
                    "_id": "64776b3879e36bee40db37b2",
                    "name": "Add a side",
                    "description": "Pizza made for cheese fanatics",
                    "descriptionTranslations": {},
                    "nameTranslations": {
                        "en": "Choose a side",
                        "ar": "اختر طبقك الجانبي"
                    },
                    "account": "61c3070ae41eefadd0306de1",
                    "capacityUsages": [],
                    "deliveryTax": 6000,
                    "imageUrl": "https://www.stockvault.net/data/2009/07/20/109569/preview16.jpg",
                    "location": "61c30761e41eefadd03072af",
                    "max": 0,
                    "min": 0,
                    "multiMax": 3,
                    "multiply": 1,
                    "plu": "MOD-02",
                    "posCategoryIds": [
                        "INTERNAL-POS-CAT-2"
                    ],
                    "posProductCategoryId": "",
                    "posProductId": "POS-ID-014",
                    "price": 900,
                    "productTags": [],
                    "productType": 3,
                    "subProducts": [
                        "64776b3879e36bee40db37c0",
                        "64776b3879e36bee40db37c2",
                        "64776b3879e36bee40db37c4"
                    ],
                    "takeawayTax": 6000,
                    "parentId": "64776b3879e36bee40db37ae",
                    "snoozed": false,
                    "subProductSortOrder": []
                }
            },
            "modifiers": {
                "64776b3879e36bee40db37ba": {
                    "_id": "64776b3879e36bee40db37ba",
                    "name": "Rare",
                    "description": "",
                    "descriptionTranslations": {},
                    "nameTranslations": {
                        "en": "Rare",
                        "ar": "غير ناضج جيدا"
                    },
                    "account": "61c3070ae41eefadd0306de1",
                    "capacityUsages": [],
                    "deliveryTax": 9000,
                    "imageUrl": "",
                    "location": "61c30761e41eefadd03072af",
                    "max": 0,
                    "min": 0,
                    "multiply": 1,
                    "plu": "COOK-01",
                    "posCategoryIds": [
                        "POS-CAT-001"
                    ],
                    "posProductCategoryId": "",
                    "posProductId": "POS-ID-003",
                    "price": 0,
                    "productTags": [],
                    "productType": 2,
                    "subProducts": [],
                    "takeawayTax": 9000,
                    "parentId": "64776b3879e36bee40db37b0",
                    "snoozed": false,
                    "subProductSortOrder": []
                },
                "64776b3879e36bee40db37bc": {
                    "_id": "64776b3879e36bee40db37bc",
                    "name": "Medium Rare",
                    "description": "",
                    "descriptionTranslations": {},
                    "nameTranslations": {
                        "en": "Medium Rare",
                        "ar": "مُتَوَسِّط النُضْجِ"
                    },
                    "account": "61c3070ae41eefadd0306de1",
                    "capacityUsages": [],
                    "deliveryTax": 9000,
                    "imageUrl": "",
                    "location": "61c30761e41eefadd03072af",
                    "max": 0,
                    "min": 0,
                    "multiply": 1,
                    "plu": "COOK-02",
                    "posCategoryIds": [
                        "INTERNAL-POS-CAT-2"
                    ],
                    "posProductCategoryId": "",
                    "posProductId": "POS-ID-004",
                    "price": 0,
                    "productTags": [],
                    "productType": 2,
                    "subProducts": [],
                    "takeawayTax": 9000,
                    "parentId": "64776b3879e36bee40db37b0",
                    "snoozed": false,
                    "subProductSortOrder": []
                },
                "64776b3879e36bee40db37be": {
                    "_id": "64776b3879e36bee40db37be",
                    "name": "Well Done",
                    "description": "",
                    "descriptionTranslations": {},
                    "nameTranslations": {
                        "en": "Well done",
                        "ar": "مطبوخ جيدا"
                    },
                    "account": "61c3070ae41eefadd0306de1",
                    "capacityUsages": [],
                    "deliveryTax": 9000,
                    "imageUrl": "",
                    "location": "61c30761e41eefadd03072af",
                    "max": 0,
                    "min": 0,
                    "multiply": 1,
                    "plu": "COOK-03",
                    "posCategoryIds": [
                        "INTERNAL-POS-CAT-2"
                    ],
                    "posProductCategoryId": "",
                    "posProductId": "POS-ID-005",
                    "price": 0,
                    "productTags": [],
                    "productType": 2,
                    "subProducts": [],
                    "takeawayTax": 9000,
                    "parentId": "64776b3879e36bee40db37b0",
                    "snoozed": false,
                    "subProductSortOrder": []
                },
                "64776b3879e36bee40db37c0": {
                    "_id": "64776b3879e36bee40db37c0",
                    "name": "Fries",
                    "description": "Fries",
                    "descriptionTranslations": {
                        "ar": "بطاطس مقلية"
                    },
                    "nameTranslations": {
                        "en": "Fries",
                        "ar": "بطاطس مقلية"
                    },
                    "account": "61c3070ae41eefadd0306de1",
                    "capacityUsages": [],
                    "defaultQuantity": 1,
                    "deliveryTax": 9000,
                    "eatInTax": 9000,
                    "imageUrl": "",
                    "location": "61c30761e41eefadd03072af",
                    "max": 0,
                    "min": 0,
                    "multiply": 1,
                    "plu": "SI-01",
                    "posCategoryIds": [
                        "SD"
                    ],
                    "posProductCategoryId": "",
                    "posProductId": "POS-ID-012",
                    "price": 0,
                    "productTags": [],
                    "productType": 2,
                    "subProducts": [],
                    "takeawayTax": 9000,
                    "parentId": "64776b3879e36bee40db37b2",
                    "snoozed": false,
                    "subProductSortOrder": []
                },
                "64776b3879e36bee40db37c2": {
                    "_id": "64776b3879e36bee40db37c2",
                    "name": "Salad",
                    "description": "Salad",
                    "descriptionTranslations": {
                        "ar": "سلطة"
                    },
                    "nameTranslations": {
                        "en": "Salad",
                        "ar": "سلطة"
                    },
                    "account": "61c3070ae41eefadd0306de1",
                    "capacityUsages": [],
                    "deliveryTax": 9000,
                    "eatInTax": 9000,
                    "imageUrl": "",
                    "location": "61c30761e41eefadd03072af",
                    "max": 0,
                    "min": 0,
                    "multiply": 1,
                    "plu": "SI-02",
                    "posCategoryIds": [
                        "SD"
                    ],
                    "posProductCategoryId": "",
                    "posProductId": "POS-ID-013",
                    "price": 200,
                    "productTags": [],
                    "productType": 2,
                    "subProducts": [],
                    "takeawayTax": 9000,
                    "parentId": "64776b3879e36bee40db37b2",
                    "snoozed": false,
                    "subProductSortOrder": []
                },
                "64776b3879e36bee40db37c4": {
                    "_id": "64776b3879e36bee40db37c4",
                    "name": "Mashed Potato",
                    "description": "Mashed Potato",
                    "descriptionTranslations": {
                        "ar": "البطاطا المهروسة"
                    },
                    "nameTranslations": {
                        "en": "Mashed Potato",
                        "ar": "البطاطا المهروسة"
                    },
                    "account": "61c3070ae41eefadd0306de1",
                    "capacityUsages": [],
                    "deliveryTax": 9000,
                    "eatInTax": 9000,
                    "imageUrl": "",
                    "location": "61c30761e41eefadd03072af",
                    "max": 0,
                    "min": 0,
                    "multiply": 1,
                    "plu": "SI-03",
                    "posCategoryIds": [
                        "SD"
                    ],
                    "posProductCategoryId": "",
                    "posProductId": "POS-ID-014",
                    "price": 100,
                    "productTags": [],
                    "productType": 2,
                    "subProducts": [],
                    "takeawayTax": 9000,
                    "parentId": "64776b3879e36bee40db37b2",
                    "snoozed": false,
                    "subProductSortOrder": []
                }
            },
            "menuTranslations": {},
            "nestedModifiers": false,
            "products": {
                "649eab653d940e56cdb4a92c": {
                    "_id": "649eab653d940e56cdb4a92c",
                    "name": "Delicious Steak Frites",
                    "description": "Delicious Steak Frites",
                    "descriptionTranslations": {
                        "ar": "شريحة لحم فريتس"
                    },
                    "nameTranslations": {
                        "en": "Delicious Steak Frites",
                        "ar": "شريحة لحم فريتس"
                    },
                    "account": "61c3070ae41eefadd0306de1",
                    "capacityUsages": [],
                    "deliveryTax": 9000,
                    "eatInTax": 9000,
                    "imageUrl": "https://resizer.staging.deliverect.com/QWXAKnkpH1Md-kCY-7OeMO4I23T2VL7f05RSP1CNic4/rt:fill/g:ce/el:0/aHR0cHM6Ly9zdG9yYWdlLmdvb2dsZWFwaXMuY29tL2lrb25hLWJ1Y2tldC1zdGFnaW5nL2ltYWdlcy81ZmY2ZWUwODkzMjhjOGFlZmVlYWJlMzMvc3RlYWstNjIyODYyNTg4YzUwNmYwMTViZTYwMThlLmpwZWc=.jpg",
                    "location": "61c30761e41eefadd03072af",
                    "max": 0,
                    "min": 0,
                    "multiMax": 1,
                    "multiply": 1,
                    "plu": "STK-01",
                    "posCategoryIds": [
                        "STK"
                    ],
                    "posProductCategoryId": "",
                    "posProductId": "POS-ID-001",
                    "price": 1500,
                    "productTags": [
                        1
                    ],
                    "productType": 1,
                    "subProducts": [
                        "64776b3879e36bee40db37b0",
                        "64776b3879e36bee40db37b2"
                    ],
                    "takeawayTax": 9000,
                    "supplementalInfo": {
                        "instructionsForUse": "Cool before drink.",
                        "ingredients": [
                            "Water",
                            "Sugar"
                        ],
                        "additives": [
                            "Artificial Food Coluring",
                            "Sodium Nitrite",
                            "Salt",
                            "Aspartame"
                        ],
                        "prepackaged": true,
                        "deposit": 0
                    },
                    "parentId": "64648bd97ab06a6436dd6010",
                    "snoozed": false,
                    "subProductSortOrder": [],
                    "referenceId": "STK-01"
                }
            },
            "productTags": [
                1
            ],
            "snoozedProducts": {},
            "validations": []
        }
    ],
    "stores": [
        "649ad021949cfa36470f9ea9"
    ],
    "callback": "https://api.staging.deliverect.com/{channelName}/menuStatus/649e**********b4a92d"
}
}
```

Existing Partners developing support can reuse 100% of their code as follows:

```python
if isinstance(payload, Object):  
store_payload()  
async process_menu_and_send_callback(payload["menus"], payload["callback"])  
return OK  
else: # payload is a list  
process_menu_old_style(payload)  
return OK
```

This should be implemented in a backwards compatible way as shown above.