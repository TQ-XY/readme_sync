---
title: How to sort Categories & Items
deprecated: false
hidden: false
link:
  new_tab: false
metadata:
  robots: index
---
## Introduction

Customers can configure the sorting order of their categories and products in their menu. For example:

- Display best-selling or new products at the top of the menu.
- A category for starters to display at the top of the menu and a category for desserts at the bottom.

## How does this order show in a published menu?

The intended order of categories shown in the menu push is simply the order in which they appear in the JSON. (For more information, view the guide on [how to configure a Menu Update Webhook URL](https://developers.deliverect.com/docs/how-do-i-receive-a-customer-menu#where-can-i-configure-a-menu-update-webhook-url))

In a published menu, products are sorted in the order they should appear per category.

Products can also appear more than once in different categories. Therefore, you should read the categories array on the payload and refer to the order of the **subProducts** array inside the category.

## Example

Here's an example for a category called **Steak & Burgers**. If you refer to the **subProducts** array, the first item has the ID `63cf9b**********05f6c05d` that relates to a **Delicious Steak and Frites** item. This item is followed by the ID `63cf9***********05f6c05e` , which is a **Burger Combo** item, and so on.

As shown in the screenshot below, the items are sorted on Deliverect the same as in the JSON payload.

Any changes to the order with subsequent menu publishing should also be reflected.

```json Sorted Product in Categories
{
"_id": "63cf9b******05f6c0a0",
"name": "Steak & Burgers",
...
"subProducts": [
   "63cf9b**********05f6c05d",
   "63cf9***********05f6c05e",
   "63cf9***********05f6c057",
   "63cf9***********05f6c05b",
],
},
```


<Image src="https://files.readme.io/c2ba834-guide_sorting_1.jpg" alt="Image shows a Steak & Burgers category with the 4 items that are mentioned as subProducts in the code above" align="center" border={true} />


<HTMLBlock>{`
<div class="callout-banner callout-banner--important">
  <span class="callout-icon"><i class="fa-regular fa-triangle-exclamation"></i></span>
  <p><strong>subProductSortOrder</strong><br>
 This is a legacy component, it shouldn't be referenced when interpreting sorting, see <code>"subProducts"</code> order instead</p>
</div>
`}</HTMLBlock>
