---
title: Endpoints
deprecated: false
hidden: false
icon: fad fa-plug
metadata:
  robots: index
next:
  pages:
    - slug: create_customer
      title: Create Customer
      type: endpoint
---
<BaseURLsTable />

## CRM Endpoints

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
        [Customer Order History](ref:customer_order_history)
      </td>

      <td>
        <POST_LABEL />
      </td>

      <td>
        Get customer order history.
      </td>
    </tr>

    <tr>
      <td>
        [Lookup Customer by Email](ref:customer_by_email)
      </td>

      <td>
        <POST_LABEL />
      </td>

      <td>
        Identify customer at checkout when they provide email
      </td>
    </tr>

    <tr>
      <td>
        [Customer Profile](ref:customer_by_id)
      </td>

      <td>
        <GET_LABEL />
      </td>

      <td>
        Get customer by profile ID.
      </td>
    </tr>

    <tr>
      <td>
        [Update Customer Profile](ref:update_customer)
      </td>

      <td>
        <PATCH_LABEL />
      </td>

      <td>
        Partially update a customer profile.
      </td>
    </tr>

    <tr>
      <td>
        [Update Customer Delivery Addresses](ref:update_deliveryaddresses)
      </td>

      <td>
        <PATCH_LABEL />
      </td>

      <td>
        Fully update a customer's delivery addresses
      </td>
    </tr>

    <tr>
      <td>
        [Update Customer Vehicles](ref:update_vehicles)
      </td>

      <td>
        <PATCH_LABEL />
      </td>

      <td>
        Fully update a customer's vehicles
      </td>
    </tr>

    <tr>
      <td>
        [Customer Favorite Orders](ref:favorite_orders)
      </td>

      <td>
        <PATCH_LABEL />
      </td>

      <td>
        Fully update a customer's favorites
      </td>
    </tr>

    <tr>
      <td>
        [Customer Order History](ref:customer_order_history)
      </td>

      <td>
        <GET_LABEL />
      </td>

      <td>
        Retrieve full order history
      </td>
    </tr>

    <tr>
      <td>
        [CRM Order](ref:order_by_id)
      </td>

      <td>
        <GET_LABEL />
      </td>

      <td>
        Retrieve specific order by it's CRM Id
      </td>
    </tr>

    <tr>
      <td>
        [Customer Favorite Orders](ref:favorite_orders)
      </td>

      <td>
        <GET_LABEL />
      </td>

      <td>
        Retrieve a customer's favorite orders
      </td>
    </tr>
  </tbody>
</Table>
