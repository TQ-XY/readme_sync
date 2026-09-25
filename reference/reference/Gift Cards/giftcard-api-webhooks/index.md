---
title: Webhooks
deprecated: false
hidden: false
icon: fad fa-webhook
link:
  new_tab: false
metadata:
  robots: index
---
<br />

<HMACAuthentication />

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        WEBHOOK
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
        [Register Gift Card Provider](ref:giftcards_registerprofile)
      </td>

      <td>
        <POST_LABEL />
      </td>

      <td>
        Request to connect a client by exchanging credentials for details.
      </td>
    </tr>

    <tr>
      <td>
        [Redeem Gift Cards](ref:post_giftcards-redeem)
      </td>

      <td>
        <POST_LABEL />
      </td>

      <td>
        Request to redeem value from gift card.
      </td>
    </tr>

    <tr>
      <td>
        [Reverse Redemption](ref:post_giftcards-reverse)
      </td>

      <td>
        <POST_LABEL />
      </td>

      <td>
        Request to reverse gift card redemption.
      </td>
    </tr>
  </tbody>
</Table>
