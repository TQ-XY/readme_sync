---
title: How to test Order Status Updates
deprecated: false
hidden: false
metadata:
  robots: index
---
## Introduction

To test handling order status updates, you can either set a single **default order status** or use the **Delivery Manager App (DMA)** to test order status updates.

## Receive order status updates

Firstly, you need to set an **Order Status Webhook URL** in the channel link settings for each channel being tested. Once in place, Deliverect sends every status to this URL as a webhook event.

<HTMLBlock>{`
<div class="callout-banner callout-banner--neutral">
  <span class="callout-icon"><i class="fa-regular fa-square-info"></i></span>
  <p>
    If the setting is not visible, turn on the **Show more** toggle at the top right of the page.
  </p>
</div>
`}</HTMLBlock>


<Image src="https://files.readme.io/06b21bf-guide_receiveorderstatuses_annotated.png" alt="Order Status Webhook URL setting in the channel link settings" align="center" border={true} />


### 1.Set default order status

To simulate immediate order status updates e.g. an order failed upon POS injection, you can preset the order status in the channel settings. Edit your channel settings and scroll to **Order > Order Status** where the default value will be **Pos received**. If you update this to e.g. 'Failed', each time an order is created for this channel, the system will automatically assign a failed status.&#x20;


<Image src="https://files.readme.io/8023341-A3EC4818-CACB-482C-9FB2-C33B1CD37FA7.jpeg" alt="default value shown as POS received in the channel settings" align="center" border={true} />



<Image src="https://files.readme.io/69632b3-2011FF16-F4BC-42C2-A833-7015D8514D4C.jpeg" alt="order status can be changed to Failed for Deliverect to respond with Failed status" align="center" border={true} />


<br />

### Update statuses on the DMA app

Use the Delivery Manager App (DMA) on an iPad or Android to apply the same status updates you can expect from an integrated POS e.g. 'Accepted' > 'Preparing' > 'Ready for Pickup'

<HTMLBlock>{`
<div class="callout-banner callout-banner--note">
  <span class="callout-icon"><i class="fa-duotone fa-solid fa-lightbulb"></i></span>
  <p>
    <strong>Set up a user on DMA</strong><br>
    See guide <a href="https://developers.deliverect.com/docs/installing-the-deliverect-app" target="_blank" rel="noopener noreferrer">here</a> on registering a user and installing the DMA app.
  </p>
</div>
`}</HTMLBlock>

When logged in to the app with a new user, you can begin accepting orders and applying incremental status updates

<HTMLBlock>{`
<div class="callout-banner callout-banner--note">
  <span class="callout-icon"><i class="fa-duotone fa-solid fa-lightbulb"></i></span>
  <p>
    <strong>Updating Statuses</strong><br>
    See guide <a href="https://help.deliverect.com/en/articles/7979073-dma-manage-your-orders" target="_blank" rel="noopener noreferrer">here</a> on updating order statuses on the DMA app
  </p>
</div>
`}</HTMLBlock>


<Image src="https://files.readme.io/16ec43a-360010482937_2_en.png" alt="Delivery Manager App order management screen" align="center" border={true} />


<br />

<br />