---
title: 'How to test Wallet Balance '
deprecated: false
hidden: false
metadata:
  robots: index
next:
  pages:
    - slug: loyalty_get_wallet
      title: Get Loyalty Customer Wallet
      type: endpoint
---
## Introduction

A loyalty platform should return a customer’s available wallet balance in response to the <Anchor target="_blank" href="https://developers.deliverect.com/v3.0-ordering-experience/reference/loyalty_get_wallet">Get Loyalty Customer Wallet</Anchor> webhook, this will either be in the form o&#x66;**&#x20;Loyalty Points** or **Wallet Cash**;

- **Loyalty points:** consumed when programs are applied
- **Wallet cash:&#x20;**&#x61;pplied at checkout

<HTMLBlock>{`
<div class="callout-banner callout-banner--neutral">
  <span class="callout-icon"><i class="fa-regular fa-square-info"></i></span>
  <p>
    <strong>Required Support</strong><br>
    Supporting at least one type of wallet is required.
  </p>
</div>
`}</HTMLBlock>

### Testing Wallet Balance

Deliverect will provide an Online Ordering store and Kiosk setup to test the complete loyalty workflow. To ensure this is working correctly to display the customer’s current funds, the following should be checked;

### Wallet Points - Deliverect Direct

If the value of `points.balance` is returned correctly, it will be displayed as shown below;

####


<Image src="https://files.readme.io/4be0e02df101edf7730858495cee1e6ead917312179b6c624fa09d643890718e-Screenshot_2026-02-10_at_14.23.43.png" align="center" width="500px" border={true} />


### Wallet Points - Deliverect Kiosk

The returned `points.balance` will display within 'My Loyalty' as below;


<Image src="https://files.readme.io/31a4ed6754b61db2e75c3b3c54ec8b193245cf4569a9a8443e3a419902f41ffd-Screenshot_2026-04-15_at_09.11.54.png" align="center" border={true} />


### Wallet Cash - Deliverect Direct

The amount displayed at "Use Credits"  level will reflect the `cash.balanceAmount` returned on the cash response.


<Image src="https://files.readme.io/252640d43796710f8a0117d41f6147f1547a2175a35c8d546d2aea314a9084b6-image.png" align="center" width="450px" border={true} />


<br />

### Wallet Cash - Deliverect Kiosk

The `cash.balanceAmount`  will show as below in local currency as 'available in your wallet'


<Image src="https://files.readme.io/2455daf8f0d3bbbc3b1c7c8229d3087e2ad84100aa839184d948b8ba5c071ce4-Screenshot_2026-04-15_at_09.13.32.png" align="center" border={true} />