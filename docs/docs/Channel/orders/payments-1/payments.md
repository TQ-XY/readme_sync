---
title: How to set Basic Payment Info
deprecated: false
hidden: false
metadata:
  robots: index
---
## Payments

Depending on the method of payment, the relevant payment types should be sent with one of two following values (as an integer)

Further details on processing additional payment parameters below;

| Payment Type       | Integer Value |
| :----------------- | :------------ |
| credit card online | 0             |
| cash               | 1             |

```json Payment Type
  "payment": {
    "amount": 1455,
    "type": 0,
    "due": 0,
    "rebate": 0,
    "commissionType": ""
  },
```

<HTMLBlock>{`
<div class="callout-banner callout-banner--neutral">
  <span class="callout-icon"><i class="fa-regular fa-square-info"></i></span>
  <p>
    <strong>Amount</strong><br>
    Payment amounts should be sent as an integer with <strong>2 decimal digits</strong>, for example, 5 dollars would be sent as <code>500</code>  </p>
</div>
`}</HTMLBlock>

### Tax Exclusive Orders

For customers in tax exclusive regions, you should ensure you handle tax accordingly, see details below;

<HTMLBlock>{`
<a href="https://developers.deliverect.com/v3.0-ordering-experience/docs/how-to-process-taxes" target="_blank" class="doc-button">▶ Tax Exclusive Orders</a>
`}</HTMLBlock>

### Paid/Unpaid Orders

In some ordering platforms, users can checkout without processing a payment. A typical scenario would be for pickup orders with a cash payment on collection. If allowing for this option at checkout, it is important to set the flag  `"orderIsAlreadyPaid": false,`

For all other scenarios where payment is taken online, set `"orderIsAlreadyPaid": true,`&#x20;

<HTMLBlock>{`
<div class="callout-banner callout-banner--neutral">
  <span class="callout-icon"><i class="fa-regular fa-square-info"></i></span>
  <p>
    <strong>Payment Amount</strong><br>
    Always pass the payment amount, whether the order is already paid or not.
  </p>
</div>
`}</HTMLBlock>

### Commission Type

This relates to the type of commission charged by the channel for its services.

Each type will correspond to an agreed percentage of the order value taken as commission, but is information provided by some channels only.

```json Comission Type
  "payment": {
    "amount": 7140,
    "type": 3,
    "due": 0,
    "rebate": 0,
    "commissionType": "regular"
  },
```

### Tips

To send a tip through with an order, there are two possible parameters allowing a channel to distinguish between the intended recipient of tips. i.e

If a tip is intended for the restaurant;

`"tip": 500,`.

If intended for the driver;

`"driverTip": 500,`.

Please be aware that not all POS partners will handle this addition to an order, in which case we have a toggle setting to not include these.

### Bag Fee

In certain regions it is mandatory to apply a charge against the packaging used. For this, we have the attribute `"bagFee"`

When included within an order it will be processed accordingly and will appear as a line item on the integrated POS.

A bag fee of $1.20 would then be sent as the below example;

```json
"bagFee": 120,
```