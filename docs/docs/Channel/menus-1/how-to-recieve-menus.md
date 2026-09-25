---
title: How to recieve menus
deprecated: false
hidden: false
metadata:
  robots: index
---
Use a menu update webhook URL to receive published Deliverect menu data for a channel.

## Understand menus and categories

Customers can sync products from their POS (point of sale) and use those products to create a menu. A completed menu represents the items a customer wants to sell and is typically a subset of the products synced from their POS.

Menus are organized into categories in the Deliverect menu management page. To read the sorted order of products and categories in a published menu, see [How can the correct sorting of products and categories be seen in the menu pushed?](https://developers.deliverect.com/docs/how-can-the-correct-sorting-of-products-and-categories-be-seen-in-the-menu-pushed).

## Receive menu data

When a customer updates a menu on their channels, they publish it by choosing the menus and channels. Deliverect sends the published menu to the **Menu update webhook URL** configured for the channel.

The menu contains the `channelLinkId` you stored when the channel was activated. Use this value to map the menu to the correct store on your platform. For more information, see [Activate a Channel](https://developers.deliverect.com/docs/how-do-i-activate-my-channel).

<Callout icon="far fa-circle-info" theme="info">
  ###

  More than one menu can be published to a channel if the channel supports multiple menus.
</Callout>


<Image src="https://files.readme.io/4a08861-guide_receivemenu_4.png" alt="Menu publishing options in Deliverect" align="center" border={true} />


## Configure a menu update webhook URL

1. [Go to your customer account on staging](https://developers.deliverect.com/docs/staging-and-production-environment).

2. Select **Locations** in the sidebar **①**, then select the **Edit** button for the channel **②**.


   <Image src="https://files.readme.io/7cc1361-guide_receivemenu_1.png" alt="Locations page showing the Edit button for a channel" align="center" border={true} />


3. In the **Menu** section, locate the **Menu update webhook URL** field and enter your menu webhook URL.


   <Image src="https://files.readme.io/c82c1e8-guide_receivemenu_2.png" alt="Menu update webhook URL field in the Menu section" align="center" border={true} />


4. Select **Save**.


   <Image src="https://files.readme.io/60c13c9-guide_receivemenu_3.png" alt="Save button for the channel configuration" align="center" border={true} />


<br />