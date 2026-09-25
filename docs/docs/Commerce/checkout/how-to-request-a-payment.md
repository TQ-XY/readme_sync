---
title: How to Request a Payment
deprecated: false
hidden: false
metadata:
  robots: index
next:
  pages:
    - slug: pay-api-get-payment-gateways
      title: Get Payment Gateways
      type: endpoint
---
## Introduction

Before checking out a basket using Deliverect Pay <Glossary>Dpay</Glossary> a commerce platform must first initiate a payment request to the payment provider.

### 1. Get Payment Gateway

Retrieve the available payment methods for a given store (`channelLinkId`) under a customer account.

#### Payment Gateways Configuration

<HTMLBlock>{`
<div class="callout-banner callout-banner--note">
  <span class="callout-icon"><i class="fa-duotone fa-solid fa-lightbulb"></i></span>
  <p>
    <strong>Payment Gateway</strong><br>
   A payment platform must be integrated and linked to stores by the merchant before they can be used to process payments. For more information about how payment gateways are managed in Deliverect <a href="https://help.deliverect.com/en/articles/7979307-deliverect-pay-configure-a-payment-gateway" target="_blank" rel="noopener noreferrer">see guide here</a>
  </p>
</div>
`}</HTMLBlock>

### Types of payment gateways

Merchants can create online and offline payment gateways in Deliverect. **Online payment gateways** allow end users to complete checkout through an online payment service, such as Adyen or Stripe. **Offline payment gateways** allow checkout to continue when the payment happens outside the scope of a commerce integration.

<HTMLBlock>{`
<div class="callout-banner callout-banner--neutral">
  <span class="callout-icon"><i class="fa-regular fa-square-info"></i></span>
  <p>
    <strong>Heading</strong><br>
    For a DPay integration, only gateways with <code>"paymentType": "online"</code> are compatible, as they'll support the required re-direct or tokenization flow. You can safely ignore non-online gateways
  </p>
</div>
`}</HTMLBlock>

```json Get Payment Gateway Response
  [
    {
        "id": "68e79ac****01c94d3044",
        "integration": 1,
        "paymentType": "online"
    }
]
```

2. ### Request a payment

Initiate a payment request with the selected provider and re-direct the user to the URL returned in the payment request response to complete the transaction. The payment remains pending until the transaction is finalized.&#x20;

```json Payment Request Response
{
  "paymentId": "68ed22c5***",
  "gateway": 1,
  "paymentStatus": "pending",
  "action": {
    "type": "redirect",
    "url": "https://checkout.providerredirect.com/c/pay/******g1a5cPaz2fbIdRRRmHXVKMi6rG7AljRysCBFY77U1BS64H#fidnandhYHdWc***********ndqcGthRmppancnPycmY2NjY2NjJyknaWR8anBxUXx1YCc%2FJ3Zsa2JpYFpscWBoJyknYGtkZ2lgVWlkZmBtamlhYHd2Jz9xd3BgeCUl"
  }
}
```

### 3. Configure the payment update webhook URL

Set the 'Payment Update Webhook URL' in the channel settings as below to receive updates to confirm a payments authorisation status;

<br />


<Image src="https://files.readme.io/9663b84e6dec9a605faf17a31c83c983eaef5ab2438ff006526e3296cdb31ce0-image.png" alt="Payment update webhook URL channel setting" align="center" width="400px" border={true} />


```json Payment Update -  Authorized
{
    "paymentId": "6***2c****c***dda6636",
    "status": "authorized",
    "metadata": {
        "gatewayProfileLinkId": "68ed22c5***",
        "methodRaw": "visa"
    }
}
```

<br />

<HTMLBlock>{`
<div class="callout-banner callout-banner--neutral">
  <span class="callout-icon"><i class="fa-regular fa-square-info"></i></span>
  <p>
    <strong>Authorized Payments</strong><br>
   After the payment update webhook confirms the payment with <code>"status": "authorized"</code>, the basket checkout can proceed.
  </p>
</div>
`}</HTMLBlock>
