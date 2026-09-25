---
title: How to test orders for Dispatch
deprecated: false
hidden: false
metadata:
  robots: index
---
## How Orders for Delivery Are Sent

Delivery orders are processed and forwarded as webhook events to the endpoints provided by the Dispatch partner.

<HTMLBlock>{`
<div class="callout-banner callout-banner--neutral">
  <span class="callout-icon"><i class="fa-regular fa-square-info"></i></span>
  <p>

    The courier assignment workflow only applies to channels enabled with Dispatch
  </p>
</div>
`}</HTMLBlock>

### Confirming Orders for Delivery

Deliverect first sends a webhook that requests order validation. Once the order is confirmed as deliverable, Deliverect sends a second webhook to create the delivery job. These two steps **Validate** and **Create** are detailed below along with the process of **Updating Delivery Jobs** and handling **Cancelled Orders**

***

## Configure Webhooks

Configure your dispatch webhooks before you receive delivery orders from Deliverect: <Anchor target="_blank" href="https://developers.deliverect.com/v3.0-ordering-experience/docs/how-to-configure-dispatch-webhooks">follow the dispatch webhooks configuration guide</Anchor>.

***

## Validate Webhook

Place a test order to confirm that Deliverect can validate your webhook (an HTTP callback URL that receives delivery job events).

1. Create a test order from your test account by following [Place a test order](https://help.deliverect.com/en/articles/7978984-place-a-test-order).
2. Select **Add Info** in the basket and provide a valid delivery address before you place the order.


<Image src="https://files.readme.io/6fa2144-guide_orderflow_4.png" alt="Basket screen with the Add Info button" align="center" caption="Select Add Info in the basket before placing the test order." border={true} />


<br />


<Image src="https://files.readme.io/e81818f-guide_orderflow_5.png" alt="Delivery address form for a test order" align="center" caption="Enter a valid delivery address for the test order." border={true} />


Check that the location also has a valid address. Go to **Locations**, then select **Edit** for the location.


<Image src="https://files.readme.io/b90b9e8-guide_orderflow_6.png" alt="Locations page with the Edit button for a location" align="center" caption="Open the location settings from the Locations page." border={true} />


<br />


<Image src="https://files.readme.io/f309d57-guide_orderflow_7.png" alt="Location address settings form" align="center" caption="Confirm that the location has a valid address." border={true} />


After you place the order, Deliverect validates the request to your webhook. Respond [according to the samples in the public documentation](https://developers.deliverect.com/reference/post-validate-delivery-job).

***

## Create Webhook

Once your webhook responds, you can view the order in the <Glossary>Delivery Manager App</Glossary>. Either manually **Assign** the order to your dispatch channel or wait two minutes for Deliverect to assign the order automatically.

Deliverect posts the event to your **Create Webhook URL**, which must respond [according to the public technical documentation](https://developers.deliverect.com/reference/post-create-delivery-job).

***

## Update Endpoint

Call our [**Update** endpoint](https://developers.deliverect.com/reference/update-delivery) to change the delivery job status, courier information, or estimated times of arrival (ETAs) for pick-up and delivery.

The final status is **Delivered**. Values and specifications are provided in the [endpoint documentation](https://developers.deliverect.com/reference/update-delivery).

You can track status updates:

- in the <Glossary>Delivery Manager App</Glossary> ([explained here](https://help.deliverect.com/en/articles/7979013-view-orders))
- in your Deliverect staging account, by navigating to the **Orders** page and selecting the order ([explained here](https://help.deliverect.com/en/articles/7979073-dma-manage-your-orders))

***

## Cancel Webhook

Initiate the cancellation of a delivery job using the <Glossary>Delivery Manager App</Glossary>. Find the order and tap **More order options**.


<Image src="https://files.readme.io/0c6e6c9-guide_orderflow_1.png" alt="Order details screen with the More order options menu" align="center" caption="Open More order options from the order details screen." border={true} />


Tap **Cancel Delivery**. Deliverect calls your **Cancel Webhook URL**.


<Image src="https://files.readme.io/742dae0-guide_orderflow_2.png" alt="More order options menu with Cancel Delivery" align="center" caption="Select Cancel Delivery to trigger the cancel webhook." border={true} />


Your webhook must respond [according to the cancel delivery documentation](https://developers.deliverect.com/reference/cancel-delivery). The app shows a message when the cancellation succeeds.

<Callout icon="📘" theme="info">
  Create the delivery job without errors before you test the **Cancel** webhook.
</Callout>

***

## Delivery Logs

Track any errors that Deliverect receives from a delivery. Find the order on the **Orders** page and select the **Delivery job** tab.


<Image src="https://files.readme.io/25ebbf8-guide_orderflow_3.png" alt="Delivery job tab showing delivery logs for an order" align="center" caption="Use the Delivery job tab to review delivery errors." border={true} />


## Error handling and testing

Handle each integration state explicitly during testing:

If your integration cannot deliver an order, do not return `"canDeliver": true` in the **Validate** webhook response.

If an update or cancellation request fails, compare the request against the linked endpoint reference, correct the required fields, and resend the request.

Test the full order flow with the Delivery Manager App before using the integration in production.
