---
title: How to Retrieve Store Details
deprecated: false
hidden: false
metadata:
  robots: index
---
## Retrieve `channelLinkdId`

A **channelLinkId** is the unique identifier for a store-channel (ordering platform) at a specific location. It may also be referenced as **storeId** throughout the documentation. Baskets are always created in association with a specific `channelLinkdId`&#x20;

Use the [Get Stores](ref:commerce-get-stores) endpoint to retrieve the `channelLinkdId` for an account.

## Registration Events

To recieve webhook events for a store registration to a channel registration webhook URL with the <Glossary>channelLinkId</Glossary> and an <Glossary>External Location Id</Glossary> known to the channel platform included, follow the steps below:

**Step 1.** <Anchor target="_blank" href="https://developers.deliverect.com/docs/staging-and-production-environment">Go to your customer account on staging</Anchor>.

***

**Step 2.** Select **Locations** in the sidebar **①** and then the **Edit** button for the channel **②**.


<Image src="https://files.readme.io/5dcbd6d-guide_pricelevels_1.png" alt="Edit a location" align="center" border={true} />


***

**Step 3.** Complete the following fields:

- **External location ID**: The ID you use in your system for the customer location.
- **Channel registration webhook URL**: Your webhook to receive channel status updates.


<Image src="https://files.readme.io/b685d62-guide_activatechannel_2.png" alt="add external ID and channel registration webhook URL" align="center" border={true} />


***

**Step 4.** Click on the **Save** button **①**, then select the three dots next to it and choose **Register** **②**.

![Click on Save button](https://files.readme.io/161d2550fba4a5b25e81fdfa062a28b005dd083e4f1e1701f820284d691c678f-image.png)

<br />

## How to know when a channel is activated, registered, or disabled

You will receive key status changes via the channel status webhook when users set one of the following statuses:

- **Register**
- **Activate**
- **Disable**

We also communicate the IDs of the channel link with each status change, in addition to the **External Location ID** (the unique ID for the customer on your platform).

## Video

View a demonstration of these processes.

<HTMLBlock>{`
<div style="position: relative; padding-bottom: 62.5%; height: 0;"><iframe src="https://www.loom.com/embed/0d7d11678f77497dbb01beddac5d97cb" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe></div>
`}</HTMLBlock>
