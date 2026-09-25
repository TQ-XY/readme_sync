---
title: Endpoints
deprecated: false
hidden: false
icon: fad fa-plug
metadata:
  robots: index
---
<BaseURLsTable />

## Channel API Endpoints

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        Endpoint
      </th>

      <th>
        Type
      </th>

      <th>
        Function
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        [Update Store Status](ref:channel-update-store-status)
      </td>

      <td>
        <POST_LABEL />
      </td>

      <td>
        Update Deliverect on any change made to a store status when either `open` or `closed` on the channel platform
      </td>
    </tr>

    <tr>
      <td>
        [Tables and Floors](ref:get-tables-floors)
      </td>

      <td>
        <GET_LABEL />
      </td>

      <td>
        Retrieve table and floor information for a specific POS location.
      </td>
    </tr>

    <tr>
      <td>
        [Menu Update (Async)](ref:menu_update_async)
      </td>

      <td>
        <POST_LABEL />
      </td>

      <td>
        Respond asynchronously to confirm successful update of a published menus
      </td>
    </tr>

    <tr>
      <td>
        [Create / Cancel Order](ref:create-channel-order)
      </td>

      <td>
        <POST_LABEL />
      </td>

      <td>
        Place a new order or process the cancellation of an existing order.
      </td>
    </tr>

    <tr>
      <td>
        [Update Courier / Guest Status](ref:update-courier-guest-status)
      </td>

      <td>
        <POST_LABEL />
      </td>

      <td>
        Update the status of a courier or guest associated with an order.
      </td>
    </tr>

    <tr>
      <td>
        [Dispatch Availability](ref:post_fulfillment-validate)
      </td>

      <td>
        <POST_LABEL />
      </td>

      <td>
        Pre-validate dispatch availability for order fulfillment
      </td>
    </tr>

    <tr>
      <td>
        [Order Delivery Update](ref:order-delivery-update)
      </td>

      <td>
        <GET_LABEL />
      </td>

      <td>
        Retrieve delivery status and tracking information for an order.
      </td>
    </tr>

    <tr>
      <td>
        [Order Rating Update](ref:post_channelname-updaterating)
      </td>

      <td>


        <POST_LABEL />
      </td>

      <td>
        Submit customer ratings / review for completed orders.
      </td>
    </tr>
  </tbody>
</Table>

## Flow Diagram

See the full ordering lifecycle of a channel integration below;

<HTMLBlock>{`
<a href="https://developers.deliverect.com/page/channel-flow" target="_blank" class="doc-button">▶ Channel Diagram</a>
`}</HTMLBlock>
