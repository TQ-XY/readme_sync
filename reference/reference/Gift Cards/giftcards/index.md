---
title: Endpoints
hidden: false
icon: fad fa-plug
---
<BaseURLsTable />

## Gift Card Endpoints

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
        [Get Profile Links](ref:get_giftcards-channel-channellinkid-providerprofilelinks)
      </td>

      <td>
        <GET_LABEL />
      </td>

      <td>
        Returns information about the current profile links.
      </td>
    </tr>

    <tr>
      <td>
        [Get Balance](ref:giftcards_get_balance)
      </td>

      <td>
        <POST_LABEL />
      </td>

      <td>
        Returns the current balance of a gift card.
      </td>
    </tr>

    <tr>
      <td>
        [Apply Gift Card](ref:giftcards_apply_gift_card)
      </td>

      <td>
        <POST_LABEL />
      </td>

      <td>
        Validates if a gift card can be applied and returns the data necessary for the order injection.
      </td>
    </tr>
  </tbody>
</Table>
