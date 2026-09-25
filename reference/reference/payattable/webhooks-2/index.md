---
title: Webhooks
deprecated: false
hidden: true
metadata:
  robots: index
---
<br />

<HMACAuthentication />

<HTMLBlock>{`
<div style="background: #F00; font-weight: bold; color: #FFF; padding: 10px">Please do not yet share this information to anyone else.<br>The below spec might still be prone to changes.</div>
`}</HTMLBlock>

Please refer to the documentation on the [Dine-In Payment Endpoints](ref:endpoints-4) section for more information. This section contains any webhooks that need to be implemented on POS or Channel side that Deliverect might call.

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        ENDPOINT
      </th>

      <th>
        TYPE
      </th>

      <th>
        FUNCTION
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        - \*BILL PAYMENT\*\*[ 🔗](https://developers.deliverect.com/reference/post-payment-to-bill-1)
      </td>

      <td>
        <span style={{ backgroundColor: "#0272d9", color: "white", borderRadius: "16px", fontFamily: "Helvetica", fontWeight: "light", fontSize: "11px", padding: "5px 10px" }}> POST</span>
      </td>

      <td>
        When we receive a **payment notification** from a channel partner, we will send this notification to the POS who is assumed to accept this payment, apply it to the bill and close the bill.
      </td>
    </tr>

    <tr>
      <td>
        - \*RETRIEVE BILL\*\*[ 🔗](https://developers.deliverect.com/reference/get-bill)
      </td>

      <td>
        <span style={{ backgroundColor: "#0e9b71", color: "white", borderRadius: "16px", fontFamily: "Helvetica", fontWeight: "light", fontSize: "11px", padding: "5px 10px" }}> GET</span>
      </td>

      <td>
        To retrieve the latest state of a bill, especially when processing payments, this webhook will be used and the latest state returned
      </td>
    </tr>
  </tbody>
</Table>