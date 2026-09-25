---
title: How to test Order Preparation Time Updates
deprecated: false
hidden: false
metadata:
  robots: index
---
## Introduction

You can update an order's preparation time before or after accepting it

## Before acceptance

Update the preparation time before accepting the order.

**Step 1.** Place the order from your application.

**Step 2.** Open the order in the Delivery Manager App.

**Step 3**. Increase the preparation time by up to 30 minutes before accepting the order.


<Image src="https://files.readme.io/c73cfb7-7979076_1_en.png" alt="Order preparation time controls before accepting an order in the Delivery Manager App" align="center" border={true} />


You will receive the payload on your [**Preparation time update** webhook](https://developers.deliverect.com/reference/post-preparation-time-update).

```json Update Preparation Time Example
{
"channelOrderId": "TEST1",
"orderId": "64b61edcdb7bfd9994cb9366",
"location": "62f4ce50310a88a92ff6a364",
"status": "6",
"pickupTime": "2023-07-18T05:27:04.131438Z"
}
```

## After acceptance

Update the preparation time after accepting the order.

**Step 1.** Place the order from your application.

**Step 2.** Open the accepted order in the Delivery Manager App.

**Step 3. &#x20;**&#x54;ap **Change Pickup Time**.


<Image src="https://files.readme.io/8b4f4cf-image.png" alt="Change Pickup Time button for an accepted order in the Delivery Manager App" align="center" border={true} />


***

**Step 4.** Choose how many minutes to add to the pickup time.


<Image src="https://files.readme.io/2663037-image.png" alt="Pickup time delay options in the Delivery Manager App" align="center" border={true} />


Deliverect sends the updated preparation time to your [**Preparation time update** webhook](https://developers.deliverect.com/reference/post-preparation-time-update). In this example, `pickupTime` is the updated pickup time

```Text json
{
"channelOrderId": "TEST1",
"orderId": "64b61edcdb7bfd9994cb9366",
"location": "62f4ce50310a88a92ff6a364",
"status": "20",
"pickupTime": "2023-07-18T05:55:30.015034Z"
}
```
