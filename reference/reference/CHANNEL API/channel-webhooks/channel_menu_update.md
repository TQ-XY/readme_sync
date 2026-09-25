---
api:
  file: channel_webhooks.json
  operationId: channel_menu_update
hidden: false
link:
  new_tab: false
---
## Purpose

Menus will be routinely published to a provided Menu Update URL. The JSON payload contains all the necessary attributes to display a customer menu(s) as intended

##

## Menu types

All menu types below will be shown as `"menuType"` and the corresponding integer. This represents the intended ordering format which the menu is suitable for.

| Name                | Integer Value |
| :------------------ | :------------ |
| Delivery and pickup | `0`           |
| Delivery            | `1`           |
| Pickup              | `2`           |
| Eat-in              | `3`           |
| Curbside            | `4`           |

## Product Configurations

<HTMLBlock>{`
<div class="callout-banner callout-banner--neutral">
  <span class="callout-icon"><i class="fa-regular fa-square-info"></i></span>
  <p>
    <strong> Item Identifier</strong><br>
   The unique identifier for each item is its <code>plu</code> which should be referenced when creating orders
  </p>
</div>
`}</HTMLBlock>

Each item in a menu has a specific type as shown in the table below

For more detail on products types and different product configurations follow the link below;

<HTMLBlock>{`
<a href="https://developers.deliverect.com/v3.0-ordering-experience/docs/how-to-handle-modifer-groups" target="_blank" class="doc-button">▶ Product Model</a>
`}</HTMLBlock>

| Product Type   | Description                                                                        | Integer Value |
| :------------- | :--------------------------------------------------------------------------------- | :------------ |
| Product        | A 'top level' item on a menu (can also be grouped within a **modifier group**)     | 1             |
| Modifier       | Options selectable when ordering a product, typically modifications of the product | 2             |
| Modifier Group | A grouping of modifiers (can also group products)                                  | 3             |

## Images

See more information on how various image types are sent within a menu;

<HTMLBlock>{`
<a href="https://developers.deliverect.com/v3.0-ordering-experience/docs/how-to-handle-images" target="_blank" class="doc-button">▶ Images</a>
`}</HTMLBlock>

## Currency

See a list of the currency types we will send within a published menu;

<HTMLBlock>{`
<a href="https://developers.deliverect.com/page/list-of-currencies" target="_blank" class="doc-button">▶ Currency Types</a>
`}</HTMLBlock>

## Translations

Find in the link below all the translatable elements of the menu and the list of translations codes.

<HTMLBlock>{`
<a href="https://developers.deliverect.com/v3.0-ordering-experience/docs/how-to-handle-translations" target="_blank" class="doc-button">▶ Translatable Elementsn</a>
`}</HTMLBlock>

## Store Opening Times

A Location's opening times are communicated within the menu payload as `"availabilities"` and covered in more detail within the guide below;

<HTMLBlock>{`
<a href="https://developers.deliverect.com/v3.0-ordering-experience/docs/how-to-handle-store-opening-hours" target="_blank" class="doc-button">▶ Opening Hours</a>
`}</HTMLBlock>

## Product Availability

There are two indicators of a product availability which are it's "snoozed" state and "visible" status. These are detailed in the page below;

<HTMLBlock>{`
<a href="https://developers.deliverect.com/v3.0-ordering-experience/docs/how-to-handle-product-snoozing" target="_blank" class="doc-button">▶ Product Availability</a>
`}</HTMLBlock>

## Multiple menus per fulfillment type

Check out the guide below that details handling menu content when more than one menu is received;

<HTMLBlock>{`
<a href="https://developers.deliverect.com/v3.0-ordering-experience/docs/how-to-process-multiple-menu-groups" target="_blank" class="doc-button">▶ Multiple Menu Format</a>
`}</HTMLBlock>

### Sample Menu JSON

Follow the guide [How to recieve menus](doc:how-to-recieve-menus) to create and publish a test menu to your channel from your Deliverect test account. See full JSON sample below;

<HTMLBlock>{`
<a href="https://storage.googleapis.com/retail-api-docs/menusample.json" target="_blank" class="doc-button">▶ Menu Sample</a>
`}</HTMLBlock>
