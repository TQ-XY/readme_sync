---
title: Loyalty Tiers
deprecated: false
hidden: false
icon: fad fa-crown
metadata:
  robots: index
---
# Introduction

The tier system allows loyalty providers to define and manage customer loyalty tiers. Your system will receive a webhook to provide a list of these tiers.

| Webhook                                | Method                                                                                                                                                                             | Purpose                                                                                                                                                                                                                                                                                                                                                                                       |
| :------------------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Get Loyalty Tiers](ref:loyalty_tiers) | <span style={{ backgroundColor: "#0e9b71", color: "white", borderRadius: "16px", fontFamily: "Helvetica", fontWeight: "light", fontSize: "11px", padding: "5px 10px" }}>GET</span> | This webhook is triggered when our system needs to retrieve a list of all available loyalty tiers. Your system should respond with details about each tier, such as its name, a description, and the point requirements to achieve it. This information is used by our channel partners to build a user interface that shows a customer's progress and the benefits of reaching higher tiers. |
