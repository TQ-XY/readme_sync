---
title: How to handle Deposits
deprecated: false
hidden: false
metadata:
  robots: index
---
## Introduction

In some countries it is mandatory to charge a deposit for e.g. glass bottles and to record this in a POS.

Deliverect can support this by allowing a single deposit product with a unique PLU to be set in an account.

With this PLU mapped within POS settings, any order for a product with a deposit will also add the specifiied deposit PLU to the order payload sent to the POS.

## How are deposits sent to channels?

A deposit will show as e.g. `"supplementalInfo.deposit":10` within the menu payload as below example. A channel receiving a product with a deposit set does **not** need to make any additional calculations, as the product price will already be inclusive of any deposit cost.&#x20;

```json Deposit Example
"6**f578fa205bc3eca854***": {
  "_id": "6**f578fa205bc3eca854***",
  "plu": "DRNK-03",
  "name": "Ginger Beer",
  "price": 260,
  "supplementalInfo": {
    "deposit": 10
  },
```

## How should this be displayed?

Wherever this is a mandatory charge to apply, although already included in the price, it is the responsibility of the ordering platform to clearly state when there is a deposit included as in below example;


<Image src="https://files.readme.io/159848b338cda7c9b09ba41fe24b33e55f4ff8e299372ca47d12d36f7e513c90-image.png" align="center" width="390px" />


###
