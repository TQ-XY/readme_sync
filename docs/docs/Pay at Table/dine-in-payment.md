---
title: Dine-In Payment
deprecated: false
hidden: true
icon: fad fa-book-open-lines
metadata:
  robots: index
---
Use these endpoints to apply a Deliverect Dine-In Payment to an order.

This page covers only the endpoints prepared for Deliverect Dine-In Payment. For the complete Deliverect API, see the [Deliverect API reference](https://developers.deliverect.com/reference/get-started).

Deliverect Dine-In Payment allows API partners to fulfill payment for an order, whether the order was created through Deliverect or directly in the POS. Support depends on the capabilities of each underlying POS.

Set up a Payment Channel Link by following [Activate your channel](https://developers.deliverect.com/docs/how-do-i-activate-my-channel). Deliverect uses [POST Channel Status](https://developers.deliverect.com/reference/post-channel-status) to send the channelLink ID and location ID back to you.

Use the same authorization and authentication rules described in [Public API Documentation](https://developers.deliverect.com/reference/machine-2-machine-access-token).

<Callout icon="far fa-triangle-exclamation" theme="warning">
  ###

  This API is work in progress, and breaking changes might still occur. Not all POS integrations support these endpoints. For details about supported POS integrations, contact the Deliverect API team.
</Callout>

These endpoints are not related to the [getReceipt endpoint](https://developers.deliverect.com/reference/get-receipt-from-pos), which was marked for deprecation in early 2022.

## Contact information

Contact email: [frederik.cornil@deliverect.com](mailto:frederik.cornil@deliverect.com)

## License information

Terms of service: [http://developers.deliverect.com/](http://developers.deliverect.com/)

## URI scheme

- Host: `developers.deliverect.com`
- Base path: `/`
- Schemes: `HTTPS`

## Tags

- `orders`: Operations related to orders
- `receipts`: Operations related to receipts
- `tables`: Operations related to tables

## Send a payment for a Deliverect order

`POST /channellinks/{clId}/orders/{channelOrderId}/payments`

<Table align={["left","left","left","left"]}>
  <thead>
    <tr>
      <th>
        Type
      </th>

      <th>
        Name
      </th>

      <th>
        Description
      </th>

      <th>
        Schema
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        Path
      </td>

      <td>
        **channelOrderId**<br />
        required
      </td>

      <td>
        ID of the channel order. This is the ID defined by the channel partner that originally sent Deliverect the order.
      </td>

      <td>
        string
      </td>
    </tr>

    <tr>
      <td>
        Path
      </td>

      <td>
        **clId**<br />
        required
      </td>

      <td>
        The channelLink for the payment. If the order exists and the payment succeeds, Deliverect adds the payment to the order. The original channelLink remains unchanged. The channelLink used for payment is available in the order payment information.
      </td>

      <td>
        string (uuid)
      </td>
    </tr>

    <tr>
      <td>
        Body
      </td>

      <td>
        **body**<br />
        required
      </td>

      <td>
        The payment to apply to the order.
      </td>

      <td>
        Payment
      </td>
    </tr>
  </tbody>
</Table>

<br />