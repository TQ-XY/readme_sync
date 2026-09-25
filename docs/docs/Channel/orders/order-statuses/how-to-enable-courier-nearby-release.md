---
title: How to enable Courier Nearby Release
deprecated: false
hidden: false
metadata:
  robots: index
---
## Introduction

The **Courier Nearby Order Release** setting allows for an order to be released to a POS only after it receives an "En Route to Pickup" status update from the delivery channel or dispatch partner.

## Prerequisites

1. The channel must have a configured [Order Status URL](ref:channel_order_status) to receive updates about the order status changes.

2. Your **Status Webhook URL** can receive a status event "Scheduled" (status value `25`) for every order created.

```json
{
    "orderId": "656f13506bbb6cf17d5c7ce3",
    "status": 25,
    "timeStamp": "2023-12-05T12:10:56.831498Z",
    "receiptId": "",
    "reason": "Waiting for order to be released by Channel",
    "channelOrderId": "TEST1743",
    "location": "61c30761e4******1ee072af",
    "channelLink": "64f999f4*******720009e3"
  }
}
```

3. Be able to use the provided "[Update Courier Status](https://developers.deliverect.com/reference/courier-update)" endpoint to inform Deliverect about the courier's status changes.

<HTMLBlock>{`
<div class="callout-banner callout-banner--neutral">
  <span class="callout-icon"><i class="fa-regular fa-square-info"></i></span>
  <p>

  If a merchant uses Dispatch via Deliverect, then updating the courier status from the channel side is not required. The order is injected into the POS once the dispatch partner updates the courier status to <code>"En Route to Pick Up"</code>
  </p>
</div>
`}</HTMLBlock>

<br />

## Configuration

**Step 1.** Log in to the staging environment&#x20;

**Step 2.** Activate the **Courier Nearby Order Release** toggle. Select the **Save** button at the bottom of the page. Orders created by the channel are set to the "Scheduled" status (value 25).


<Image src="https://files.readme.io/4cc5ef4-Image_06-12-2023_at_14.51.jpeg" alt="Activate &quot;Courier nearby order release&quot; in channel settings" align="center" border={true} />


**Step 3.** To trigger the injection of orders to the POS webhook, the channel must use the [Update Courier / Guest Status](ref:update-courier-guest-status) endpoint. When the courier is en route to pick up, send a request to the **Update Courier Status** endpoint with the appropriate parameters and set the status value to 83.

```json
{
  "channelOrderId": "63171d******d34b5efe",
  "courierUpdate": {
    "status": 83,
    "arrivalTime": "2022-10-25T16:24:40.482000Z",
    "deliveryTime": "2022-10-25T16:54:40.482000Z",
    "courier": {
      "firstName": "Joe",
      "lastName": "Driver",
      "phoneNumber": "+44 20 3936 1162"
    }
  }
}
```

**Step 4.** The order is injected into the POS webhook once our system receives the "En route to pick up" courier status update.
