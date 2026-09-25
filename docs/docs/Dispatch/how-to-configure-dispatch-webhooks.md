---
title: How to configure Dispatch Webhooks
deprecated: false
hidden: false
metadata:
  robots: index
next:
  pages:
    - slug: overview
      title: Dispatch Overview
      type: basic
---
## Introduction

Configure dispatch webhooks on Deliverect so your integration can validate, create, and cancel dispatch orders.

## Prerequisites

Before you start, complete these steps:

1. [Log in to your customer account](https://developers.deliverect.com/docs/staging-and-production-environment#access-your-customer-account).
2. Confirm that you can access **Dispatch** → **Configuration**.
3. Prepare standardized webhook URLs for **Validate URL**, **Create URL**, and **Cancel URL**. Use the same URLs for every customer install.

## Instructions

**Step 1.** [Log in to your customer account](https://developers.deliverect.com/docs/staging-and-production-environment#access-your-customer-account). In the sidebar, select **Dispatch** **①**, followed by **Configuration** **②**.


<Image src="https://files.readme.io/f8f66f3d6c8c03fefb3ecebc0467cc7a2136b03ae9acdf2d5214963e7fc3b53d-Screenshot_2025-05-09_at_10.59.21.png" alt="Dispatch Configuration page in the Deliverect sidebar&quot; caption=&quot;Open Dispatch, then Configuration from the sidebar." align="center" border={true} />


***

**Step 2.** Select **Add partner** for your location.


<Image src="https://files.readme.io/b760dc3-guide_receiveorders_3.png" alt="Add partner button for a location in Dispatch configuration&quot; caption=&quot;Select Add partner for the location you want to configure." align="center" border={true} />


***

**Step 3.** Choose **Generic** and enter your webhooks for **Validate URL**, **Create URL** and **Cancel URL**.  Select the **Save** button.


<Image src="https://files.readme.io/f941427-guide_receiveorders_4.png" alt="Generic partner form with Validate URL, Create URL, and Cancel URL fields&quot; caption=&quot;Choose Generic, enter the three webhook URLs, then save the configuration." align="center" border={true} />


***

## Live tutorial

<HTMLBlock>{`
<iframe
    title="Dispatch webhooks configuration live tutorial" src="https://www.iorad.com/player/2131637/Dispatch-Webhooks-configuration?iframeHash=watchsteps-1&src=iframe&oembed=1"
    width="1000px" height="600px" style="max-width: 100%; height: 600px; border-bottom: 1px solid #ccc;"
    referrerpolicy="strict-origin-when-cross-origin" frameborder="0" webkitallowfullscreen="webkitallowfullscreen"
    mozallowfullscreen="mozallowfullscreen" allowfullscreen="allowfullscreen"
    allow="camera; microphone; clipboard-write"></iframe>
`}</HTMLBlock>

***

## Troubleshooting

### I don't receive orders at my webhook

Check that the location has a valid address and that the channel is set to **Use dispatch**. You can find this option when you select the **Edit** button for the channel on the **Locations** page.


<Image src="https://files.readme.io/2e9e810-guide_receiveorders_5.png" alt="Use dispatch setting in the channel editor on the Locations page&quot; caption=&quot;Enable Use dispatch for the channel on the Locations page." align="center" border={true} />