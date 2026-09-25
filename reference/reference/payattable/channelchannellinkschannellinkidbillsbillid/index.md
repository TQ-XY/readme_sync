---
title: Endpoints
hidden: true
---
<HTMLBlock>{`
<div style="background: #F00; font-weight: bold; color: #FFF; padding: 10px">Please do not yet share this information to anyone else.<br>The below spec might still be prone to changes.</div>
`}</HTMLBlock>

## Pay at Table

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th>
        ENDPOINT
      </th>

      <th>
        TYPE
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        - _GET Bill by Id_\*[ 🔗](https://developers.deliverect.com/reference/bill-by-id)
      </td>

      <td>
        <span style={{ backgroundColor: "#0e9b71", color: "white", borderRadius: "16px", fontFamily: "Helvetica", fontWeight: "light", fontSize: "11px", padding: "5px 10px" }}> GET</span>
      </td>
    </tr>

    <tr>
      <td>
        - _GET Bill by table_\*[ 🔗](https://developers.deliverect.com/reference/bill-by-id-1)
      </td>

      <td>
        <span style={{ backgroundColor: "#0e9b71", color: "white", borderRadius: "16px", fontFamily: "Helvetica", fontWeight: "light", fontSize: "11px", padding: "5px 10px" }}> GET</span>
      </td>
    </tr>

    <tr>
      <td>
        - _POST Payment to Bill_\*[ 🔗](https://developers.deliverect.com/reference/post-payment-to-bill)
      </td>

      <td>
        <span style={{ backgroundColor: "#0272d9", color: "white", borderRadius: "16px", fontFamily: "Helvetica", fontWeight: "light", fontSize: "11px", padding: "5px 10px" }}> POST</span>
      </td>
    </tr>

    <tr>
      <td>
        - _POST Payment to Order_\*[ 🔗](https://developers.deliverect.com/reference/post-payment-to-order)
      </td>

      <td>
        <span style={{ backgroundColor: "#0272d9", color: "white", borderRadius: "16px", fontFamily: "Helvetica", fontWeight: "light", fontSize: "11px", padding: "5px 10px" }}> POST</span>
      </td>
    </tr>

    <tr>
      <td>
        **WEBHOOK**
      </td>

      <td>

      </td>
    </tr>

    <tr>
      <td>
        - _Payment Feeback_\*[ 🔗](https://developers.deliverect.com/reference/channel-payment-feedback)
      </td>

      <td>
        <span style={{ backgroundColor: "#0272d9", color: "white", borderRadius: "16px", fontFamily: "Helvetica", fontWeight: "light", fontSize: "11px", padding: "5px 10px" }}> POST</span>
      </td>
    </tr>

    <tr>
      <td>
        - _Bill Update_\*[ 🔗](https://developers.deliverect.com/reference/channel-bill-update)
      </td>

      <td>
        <span style={{ backgroundColor: "#0272d9", color: "white", borderRadius: "16px", fontFamily: "Helvetica", fontWeight: "light", fontSize: "11px", padding: "5px 10px" }}> POST</span>
      </td>
    </tr>
  </tbody>
</Table>

This documentation describes the API endpoints that are being prepared to support **Deliverect Pay at Table functionalities**. They are by no means a full documentation on the [entire Deliverect API](https://developers.deliverect.com/reference/get-started). The purpose of the Pay at Table API is to allow partners to fulfil the payment of a bill. Whether it is created via Deliverect or directly in the POS should preferably not matter (but will depend on the capabilities of each underlying POS).

Setting up a (Payment) Channel Link can be done as described on our [Activating Channels](https://developers.deliverect.com/docs/how-do-i-activate-my-channel) page. Endpoint [POST Channel Status](https://developers.deliverect.com/reference/post-channel-status) will be used to communicate channelLink ID and location ID back to you. In case payments are supported, we expect "billPaymentFeedbackURL" to be part of the return.

Authorization and authentication are not specifically described in this document, but are subject to the same rules as described on [Public API Documentation](https://developers.deliverect.com/reference/machine-2-machine-access-token). Your API Token should have the scope "Order & Pay" enabled.

The mentioned endpoints in this document are not related to the getReceipt endpoint which were deprecated early 2022. **This API is work in progress and breaking changes might still take place. Not all POSes integrated with Deliverect will already be implemented for these endpoints.** For an insight on the POSes supported, please contact our API team.

![](https://files.readme.io/519b20b-Dine-In_Payment_Flow.png "Dine-In Payment Flow.png")

<br />
