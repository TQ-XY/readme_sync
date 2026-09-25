---
title: User Authentication
deprecated: false
hidden: false
icon: fad fa-user-unlock
metadata:
  robots: index
---
## Authentication via SSO

A customer has the possibility to start the experience from a dedicated app and then use an external ordering channel to place an order. To simplify the process and remove friction we offer a Single Sign On (SSO) feature, that allows the customer to login in his loyalty app remaining connected when he moves to the ordering platform.

| Webhook                                                 | Method                                                                                                                                                                              | Purpose                                                                                                                                                                                                                                              |
| :------------------------------------------------------ | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Loyalty SSO - OAuth token exchange](ref:loyalty_token) | <span style={{ backgroundColor: "#0272d9", color: "white", borderRadius: "16px", fontFamily: "Helvetica", fontWeight: "light", fontSize: "11px", padding: "5px 10px" }}>POST</span> | This endpoint performs the last step of a classic OAuth2.0 authentication, exchanging an authorization code for an access token. For more information, see [SSO documentation](https://developers.deliverect.com/v3.0/reference/loyalty-partner-sso) |

## Channel requirements for SSO

Generic channels needs to support the following webhook in order to support SSO flows for loyalty providers

| Webhook                                                                        | Method                                                                                                                                                                              | Purpose                                                                                                                                                                                                                                                             |
| :----------------------------------------------------------------------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| [Loyalty SSO - redirect to ordering channel](ref:loyalty-partner-sso-redirect) | <span style={{ backgroundColor: "#0e9b71", color: "white", borderRadius: "16px", fontFamily: "Helvetica", fontWeight: "light", fontSize: "11px", padding: "5px 10px" }}>POST</span> | This webhook will be called when when a customer attempts to authenticate to their service when being redirected from a 3rd party application.  For more information, see [SSO documentation](https://developers.deliverect.com/v3.0/reference/loyalty-partner-sso) |
