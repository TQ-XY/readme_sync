---
title: Loyalty Customers
deprecated: false
hidden: false
icon: fad fa-people-group
metadata:
  robots: index
---
## Introduction

The following webhooks are called by our system to enable loyalty providers to manage customer data.

## Webhooks

| Webhook                                                                | Method                                                                                                                                                                              | Purpose                                                                                                                                                                                                                                        |
| :--------------------------------------------------------------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Create Loyalty Customer](ref:loyalty-channel-create-loyalty-customer) | <span style={{ backgroundColor: "#0272d9", color: "white", borderRadius: "16px", fontFamily: "Helvetica", fontWeight: "light", fontSize: "11px", padding: "5px 10px" }}>POST</span> | This webhook is triggered to create or update a customer profile.                                                                                                                                                                              |
| [Get Loyalty Customer](ref:loyalty-channel-get-customer)               | <span style={{ backgroundColor: "#0e9b71", color: "white", borderRadius: "16px", fontFamily: "Helvetica", fontWeight: "light", fontSize: "11px", padding: "5px 10px" }}>GET</span>  | This webhook is triggered to retrieve a customer's profile details. Your system will receive this request when our system needs to fetch a customer's information, including their unique loyalty customer ID and other relevant profile data. |
