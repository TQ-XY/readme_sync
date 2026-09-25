---
title: Webhooks
deprecated: false
hidden: false
icon: fad fa-webhook
metadata:
  robots: index
---
<br />

<HMACAuthentication />

# Registration

During certification, you will be required to provide a registration webhook. When a merchant selects a generic integration as their loyalty provider, we will call this webhook in order to retrieve all the remaining configuration.

| Webhook                                              | Method         | Purpose                                                                                                   |
| :--------------------------------------------------- | :------------- | :-------------------------------------------------------------------------------------------------------- |
| [Register Loyalty Partner](ref:loyalty_registration) | <POST_LABEL /> | This webhook is called when the merchant registers a your integration as a loyalty provider in Deliverect |

# Customer Management Webhooks

The following webhooks are called by our system to enable loyalty providers to manage customer data.

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        Webhook
      </th>

      <th>
        Method
      </th>

      <th>
        Purpose
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        [Create Loyalty Customer](ref:loyalty-channel-create-loyalty-customer)
      </td>

      <td>
        <POST_LABEL />
      </td>

      <td>
        This webhook is triggered to create or update a customer profile.
      </td>
    </tr>

    <tr>
      <td>
        [Get Loyalty Customer](ref:loyalty_get_customer)
      </td>

      <td>
        <GET_LABEL />
      </td>

      <td>
        This webhook is triggered to retrieve a customer's profile details. Your system will receive this request when our system needs to fetch a customer's information, including their unique loyalty customer ID and other relevant profile data.
      </td>
    </tr>
  </tbody>
</Table>

# Tier System Webhook

The tier system allows loyalty providers to define and manage customer loyalty tiers. Your system will receive a webhook to provide a list of these tiers.

| Webhook                            | Method        | Purpose                                                                                                                                                                                                                                                                                                                                                                                       |
| :--------------------------------- | :------------ | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Loyalty Tiers](ref:loyalty-tiers) | <GET_LABEL /> | This webhook is triggered when our system needs to retrieve a list of all available loyalty tiers. Your system should respond with details about each tier, such as its name, a description, and the point requirements to achieve it. This information is used by our channel partners to build a user interface that shows a customer's progress and the benefits of reaching higher tiers. |

# Wallet Application Lifecycle

The lifecycle of applying a loyalty wallet as a discount to an order follows a clear tree-step process, with your system receiving webhooks at each stage.

| Webhook                                                        | Method         | Purpose                                                                                                                                                                                                                                                                                                                           |
| :------------------------------------------------------------- | :------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Get Loyalty Customer Wallet](ref:get-loyalty-customer-wallet) | <GET_LABEL />  | This webhook is triggered to retrieve a customer's wallet balance. Your system should respond with the customer's available funds in the form of cash and/or loyalty points. This data is essential for our system to display the customer's current balance, allowing them to make informed decisions about using their rewards. |
| [Loyalty Wallet](ref:loyalty-wallet)                           | <POST_LABEL /> | This webhook is initiated by our system to validate a customer's request to use cash or points from their loyalty wallet as a discount on a current order. Your system, as the loyalty provider, is responsible for performing the necessary business rule checks and returning the discount amount and type.                     |
| [Loyalty Orders](ref:orders)                                   | <POST_LABEL /> | This webhook is called when an end customer places an order. Here the loyalty provider can redeem the applied discounts created from the wallet.                                                                                                                                                                                  |
| [Cancel Loyalty Order](ref:loyalty-partner-cancel-order)       | <POST_LABEL /> | This webhook is called an order is cancelled. Here the loyalty provider can revert any redemptions or transactions done when the order was created                                                                                                                                                                                |

# Program Application Lifecycle

The lifecycle of applying a loyalty program to an order follows a clear three-step process, with your system receiving webhooks at each stage.

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        Webhook
      </th>

      <th>
        Method
      </th>

      <th>
        Purpose
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        [Loyalty Programs](ref:loyalty-programs)
      </td>

      <td>
        <POST_LABEL />
      </td>

      <td>
        This webhook is called to get a list of all loyalty programs a customer is eligible for. Your system should respond with a list of programs, which our channel partners will use to populate a list of available rewards in their user interfaces.
      </td>
    </tr>

    <tr>
      <td>
        [Validate Programs](ref:loyalty-platform-validate-program)
      </td>

      <td>
        <POST_LABEL />
      </td>

      <td>
        This webhook is called to validate that selected programs are applicable to the current basket. Your system should respond with the specific discounts that should be applied to the order.
      </td>
    </tr>

    <tr>
      <td>
        [Loyalty Orders](ref:orders)
      </td>

      <td>
        <POST_LABEL />
      </td>

      <td>
        This webhook is triggered when an order is finalized and placed or when an order is cancelled.

        When an order is created, your system should handle the automatic redemption of all applied loyalty programs in the basket. This includes deducting loyalty points, marking coupons as used, or processing any other redemption logic.
      </td>
    </tr>

    <tr>
      <td>
        [Cancel Loyalty Order](ref:loyalty-partner-cancel-order)
      </td>

      <td>
        <POST_LABEL />
      </td>

      <td>
        This webhook is triggered when an order is is cancelled.

        For order cancelation, your system should revert any transactions or redemptions that were performed for that order, ensuring that loyalty points are returned and any program usage is undone.
      </td>
    </tr>
  </tbody>
</Table>

# Authentication via SSO

A customer has the possibility to start the experience from a dedicated app and then use an external ordering channel to place an order. To simplify the process and remove friction we offer a Single Sign On (SSO) feature, that allows the customer to login in his loyalty app remaining connected when he moves to the ordering platform.

| Webhook                                                 | Method         | Purpose                                                                                                                                                                                                                                         |
| :------------------------------------------------------ | :------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Loyalty SSO - OAuth token exchange](ref:loyalty_token) | <POST_LABEL /> | This endpoint performs the last step of a classic OAuth2.0 authentication, exchanging an authorization code for an access token. For more information, see [SSO documentation](https://developers.deliverect.com/reference/loyalty-partner-sso) |

## Channel requirements for SSO

Generic channels needs to support the following webhook in order to support SSO flows for loyalty providers

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        Webhook
      </th>

      <th>
        Method
      </th>

      <th>
        Purpose
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        [Loyalty SSO - redirect to ordering channel](ref:loyalty-partner-sso-redirect)
      </td>

      <td>
        <POST_LABEL />
      </td>

      <td>
        This webhook will be called when when a customer attempts to authenticate to their service when bering redirected from a 3rd party application.  For more information, see [SSO documentation](https://developers.deliverect.com/v3.0-ordering-experience/reference/loyalty-partner-sso)
      </td>
    </tr>
  </tbody>
</Table>

<br />

<br />
