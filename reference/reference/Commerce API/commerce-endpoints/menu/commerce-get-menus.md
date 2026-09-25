---
api:
  file: commerce.json
  operationId: commerce-channel-api-stores-get-store-menus
hidden: false
---
## Purpose

This endpoint retrieves the most recently published menu for a specific store, identified by its unique <Glossary>channelLinkId</Glossary>

The response includes the store’s available products, pricing details, images, and more. Specific menu and category availabilities are also included.

## Query Parameters

It is possible to refine results by the menu type, the listed type below

```Text Delivery
?fulfillmentType=delivery
```
```Text Pickup
?fulfillmentType=pickup
```
```Text Curbside
?fulfillmentType=curbside
```
```Text Eat-In
?fulfillmentType=eatIn
```

## Menu types

All menu types below will be shown as `"menuType"` and the corresponding integer. This represents the intended ordering format which the menu is suitable for.

| Name                | Integer Value |
| :------------------ | :------------ |
| Delivery and pickup | 0             |
| Delivery            | 1             |
| Pickup              | 2             |
| Eat-in              | 3             |
| Curbside            | 4             |

## Menu Model

View all menu attributes and their meaning via the link below;

<HTMLBlock>{`
<a href="https://developers.deliverect.com/page/menu-glossary" target="_blank" class="doc-button">▶ Menu Model</a>
`}</HTMLBlock>

## Multiple menus per fulfillment type

Check out the guide below that details handling menu content when more than one menu is retrieved.

<HTMLBlock>{`
<a href="https://developers.deliverect.com/v3.0-ordering-experience/docs/how-to-handle-multiple-menus" target="_blank" class="doc-button">▶ Multiple Menu Format</a>
`}</HTMLBlock>