---
title: How to test Busy Mode
deprecated: false
hidden: false
metadata:
  robots: index
---
## Introduction

Busy mode allows customers to close their store if they are unable to prepare orders.

## How a channel knows when busy mode is activated

Follow these steps to configure a webhook to receive busy mode updates.

**Step 1.** [Go to your customer account on staging](https://developers.deliverect.com/docs/staging-and-production-environment).

***

**Step 2.** Select **Locations** in the sidebar **①** and then the **Edit** button for the channel **②**.


<Image src="https://files.readme.io/537ad71-guide_testbusymode_1.png" alt="on location tabs, edit channel settings" align="center" border={true} />


***

**Step 3.** Enter your webhook into the **Busy mode URL** field.


<Image src="https://files.readme.io/295c1d1-guide_testbusymode_2.png" alt="add busy mode URL to channel" align="center" border={true} />


***

**Step 4.** Select the **Save** button at the bottom of the page.


<Image src="https://files.readme.io/114c9d8-guide_testbusymode_3.png" alt="Save the changes" align="center" border={true} />


***

**Step 5.** You can now test the functionality by [following the steps in this help article](https://help.deliverect.com/en/articles/7978972-use-busy-mode-to-temporarily-delay-orders-or-close-a-location).

You will receive a response in this format:

```json Example
{
"accountId": "5b****71c6489f0029****d4",
"locationId": "5c****ecc6489f0001****b8",
"channelLinkId": "5e****abc11dec0001****9b",
"status": "PAUSED"
}
```

<br />