---
title: How to add a BOGOF promotion
deprecated: false
hidden: false
metadata:
  robots: index
---
## Introduction

A channel or restaurant may seek to enhance sales by introducing an enticing **"Buy One, Get One"** offer for a specific product.

Use **Buy One Get One Free** consistently for the promotion name. In API payloads, Deliverect identifies the promotion with the `BOGOF` prefix.

## Configuration

**Step 1.** [Access your test customer account on our staging environment](https://developers.deliverect.com/docs/staging-and-production-environment#access-your-customer-account).

**Step 2.** Go to the **Menu** page. Open the actions menu for the menu that contains the product, then select the edit option.


<Image src="https://files.readme.io/8a992e5-image.png" alt="Menu page showing the actions menu for editing a menu" align="center" border={true} />


***

**Step 3.** Scroll down to the product where you want to apply **Buy One Get One** promotion. Then select **Edit product** by clicking the 3 dots.


<Image src="https://files.readme.io/9f89ca2-image.png" alt="Product row showing the actions menu and Edit product option" align="center" width="-2px" border={true} />


***

**Step 4.** In the **Edit Product** section, turn on the **Buy one get one free** toggle. Select **Save edits**.


<Image src="https://files.readme.io/330bb41-image.png" alt="Edit Product section showing the Buy one get one free toggle" align="center" width="-2px" border={true} />


***

**Step 5.** Push the menu to the channel. The promoted product PLU (price lookup code) includes the `[BOGOF]` prefix.

```json JSON
"products": {
            "exampleProductId": {
                "_id": "63a0770ec28e0*****0b6193",
                "name": "Chicken Burger",
                "description": "Crispy coated chicken thigh, iceberg lettuce, pickles, slice of cheese and mayo, all in a toasted brioche bun.",
                "descriptionTranslations": {},
                "nameTranslations": {},
                "account": "614318d8ca0b*****c3e2c6d",
                "capacityUsages": [],
                "deliveryTax": 9000,
                "eatInTax": 9000,
                "imageUrl": "https://resizer.staging.deliverect.com/By5AsW4yrHpO2XEkTpT59gT0ojYuFArr5krZnUIyeAI/rt:fill/g:ce/el:0/aHR0cHM6Ly9zdG9yYWdlLmdvb2dsZWFwaXMuY29tL2lrb25hLWJ1Y2tldC1zdGFnaW5nL2ltYWdlcy81ZmY2ZWUwODkzMjhjOGFlZmVlYWJlMzMvY2hrYnVyZ2VyLTYyMjhjMWRjZGI1OTg2MDAxZWJmNThkZi5qcGVn.jpg",
                "location": "61431bb1dfb22e7*****2e2b",
                "max": 0,
                "min": 0,
                "multiply": 1,
                "plu": "[BOGOF]P-BURG-CHK-#D2#-",
                "posCategoryIds": [
                    "BURG"
                ],
                "posProductCategoryId": "",
                "posProductId": "POS-ID-026",
                "price": 800,
                "productTags": [],
                "productType": 1,
                "subProducts": [],
                "takeawayTax": 9000,
                "parentId": "63a0770fc2*****23f0b61e4",
                "snoozed": false,
                "subProductSortOrder": [],
                "referenceId": "P-BURG-CHK"
            } 
         }
      }
```

***

After the menu is published, place a test order from your channel with the product that has the **Buy One Get One Free** promotion.

Deliverect sends two products to the POS. Deliverect divides the price across the promoted products so one product is free.


<Image src="https://files.readme.io/bd40be8-image.png" alt="Order details showing two promoted products sent to the POS" align="center" border={true} />


***

<br />