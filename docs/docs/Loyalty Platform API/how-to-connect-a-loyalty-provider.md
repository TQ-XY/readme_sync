---
title: How to Connect a Loyalty Provider
excerpt: This guide explains how to set up loyalty webhooks in your Deliverect account.
deprecated: false
hidden: false
metadata:
  robots: index
---
## How to save your Loyalty Webhook URLs in staging

**Step 1.** [Access your test customer account on our staging environment](https://developers.deliverect.com/docs/staging-and-production-environment#access-your-customer-account).

**Step 2.** Select **More** on account level and then Select **Loyalty Settings**


<Image src="https://files.readme.io/66876cec2599ee8c1e9efe931fe89c2d2a0a4eb65f618f203d85a0d8abe3d995-Loyalty_settings.png" align="center" />


<br />

**Step 3**: Select your own provider name from the list. For example "Test Loyalty" and then click on Install.


<Image src="https://files.readme.io/cfde0013995d74c161e8293f2574874e5cf282dc0a483f397d00daac5f66d54d-Install_loyalty.png" align="center" />


<br />

<br />

**Step 4** Complete the following fields:

**Registration URL**: The Registration URL is the endpoint provided by the loyalty partner where Deliverect can send the registration request. You need to provide this URL so we can initiate the registration call for the loyalty integration.

**API Key**: The unique API Key provided by the Loyalty Partner.

<br />


<Image src="https://files.readme.io/22e040fd1c29ff4c1d3b1c0884085aa1c330f71134a0c92a555abddc1a3f3845-image.png" align="center" width="500px" border={true} />


<br />

This triggers an API call to your [**Register Webhook URL**](https://developers.deliverect.com/v3.0-ordering-experience/reference/loyalty_registration). Deliverect will send you the following information:

<br />

```json Payload
{
    "account": "6401c934c43f86e*****eb9c",
    "apiKey": "123***890"
}
```

The response should contain the necessary URLs for the integration: **Customer URL, Order URL, Available Programs URL, customerWalletURL**

```json Response
{
    "customerURL": "https://yourserver.com/customer",
    "customerWalletURL": "https://yourserver.com/customerWallet",
    "loyaltyProgramsURL": "https://yourserver.com/programs",
    "orderURL": "https://yourserver.com/orders"
}
```

<br />

**Step 5**: After successfully completing the registration, select the **pencil** to edit the Generic Loyalty Settings.

<br />


<Image src="https://files.readme.io/e0d86a50f3e816e873ae85ed88d6cd5edbc23e686ad8f39d841bcead20c4fcc8-image.png" align="center" width="500px" border={true} />


<br />

**Step 6**: The**Customer URL, Order URL, Available Programs URL** will be visible if the response to the regiser on step 4 was correct. Click on "Save".


<Image src="https://files.readme.io/d74c2da485aead3f230713b4c41839dccebd20baebb4d4476ba9d4afe9aa6b60-image.png" align="center" width="500px" border={true} />


<br />


<Image src="https://files.readme.io/6df6fc224852dad96bcf98a770f4b6cdcefbf9112de683c6f50af71d4ee951dd-image.png" align="center" width="5px" />
