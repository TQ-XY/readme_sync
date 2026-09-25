---
title: Loyalty Wallet
deprecated: false
hidden: false
icon: fad fa-wallet
metadata:
  robots: index
---
## Introduction

The lifecycle of applying a loyalty wallet as a discount to an order follows a clear tree-step process, with your system receiving webhooks at each stage.

## Webhooks

| Webhook                                                        | Method                                                                                                                                                                              | Purpose                                                                                                                                                                                                                                                                                                                           |
| :------------------------------------------------------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Get Loyalty Customer Wallet](ref:get-loyalty-customer-wallet) | <span style={{ backgroundColor: "#0e9b71", color: "white", borderRadius: "16px", fontFamily: "Helvetica", fontWeight: "light", fontSize: "11px", padding: "5px 10px" }}>GET</span>  | This webhook is triggered to retrieve a customer's wallet balance. Your system should respond with the customer's available funds in the form of cash and/or loyalty points. This data is essential for our system to display the customer's current balance, allowing them to make informed decisions about using their rewards. |
| [Loyalty Order Notification](ref:loyalty-partner-order)        | <span style={{ backgroundColor: "#0272d9", color: "white", borderRadius: "16px", fontFamily: "Helvetica", fontWeight: "light", fontSize: "11px", padding: "5px 10px" }}>POST</span> | This webhook is called when an end customer places an order. Here the loyalty provider can redeem the applied discounts created from the wallet.                                                                                                                                                                                  |
| [Cancel Loyalty Order](ref:loyalty-partner-cancel-order)       | <span style={{ backgroundColor: "#0272d9", color: "white", borderRadius: "16px", fontFamily: "Helvetica", fontWeight: "light", fontSize: "11px", padding: "5px 10px" }}>POST</span> | This webhook is called an order is cancelled. Here the loyalty provider can revert any redemptions or transactions done when the order was created                                                                                                                                                                                |
