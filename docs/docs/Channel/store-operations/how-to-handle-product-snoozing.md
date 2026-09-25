---
title: How to handle Product Snoozing
deprecated: false
hidden: false
metadata:
  robots: index
---
## Introduction

In Deliverect, a product can be snoozed to indicate it should be no longer available on ordering platforms for a defined period of time.

## Snooze Webhooks

When a customer snoozes an item, a webhook event is delivered to a designated endpoint to ensure real-time availability is updated on their online menus.&#x20;

<HTMLBlock>{`
<a href="https://developers.deliverect.com/v3.0-ordering-experience/reference/channel_snooze" target="_blank" class="doc-button">▶ Snooze Webhooks</a>
`}</HTMLBlock>

## Snoozed Status

Each product in the menu payload includes a boolean property `"snoozed"` which specifies if at the point of the menu being published, if the item is snoozed or not.

If you require information about the snooze period, you can reference the product.snoozeId and cross-reference this ID in the menu.snoozeProducts to retrieve additional details such as the start and end dates of the snooze period.

```json
"products": {
    "65*******************73c": {
        "_id": "65*******************3c",
        "name": "Toasted Bagel",
                ..
                "plu": "P-BA-9PxS-2",
                ..
                "snoozed": true,
                "snoozeId": "65*******************de",
                ..
},
```

```json
"snoozedProducts": {
    "65*******************b7": {
    "location": "61*******************af",
    "name": "Toasted Bagel",
    "plu": "P-BA-9PxS-2",
    "snoozeEnd": "yyyy-MM-dd HH:mm:ss.SSSSSSZ",
    "snoozeStart": "yyyy-MM-dd HH:mm:ss.SSSSSSZ"
    },
```

If you use multiple menus in one location (for different channels etc.) It's possible that a product snoozed on one menu is available on another menu in the same location.

<br />