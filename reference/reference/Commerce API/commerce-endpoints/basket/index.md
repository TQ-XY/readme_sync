---
title: Basket
deprecated: false
hidden: false
icon: fad fa-basket-shopping
metadata:
  robots: index
---
## Glossary

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
        [Create Basket](ref:commerce-create-basket)
      </td>

      <td>
        <POST_LABEL />
      </td>

      <td>
        Generates a unique basket ID, validates the order and its contents, and calculates the total payable amount including applicable taxes and store charges.
      </td>
    </tr>

    <tr>
      <td>
        [Validate Basket](ref:validate-basket)
      </td>

      <td>
        <POST_LABEL />
      </td>

      <td>
        Validates a basket using a unique basket ID.
      </td>
    </tr>

    <tr>
      <td>
        [Get Basket](ref:commerce-channel-api-baskets-get-basket-1)
      </td>

      <td>
        <GET_LABEL />
      </td>

      <td>
        Retrieves a basket by unique ID, including its details and contents.
      </td>
    </tr>

    <tr>
      <td>
        [Recreate Basket](ref:recreate-basket)
      </td>

      <td>
        <POST_LABEL />
      </td>

      <td>
        Recreate a previous basket in a specified store
      </td>
    </tr>

    <tr>
      <td>
        [Update Basket - Fulfillment Details](ref:update-basket-fulfillment)
      </td>

      <td>
        <PATCH_LABEL />
      </td>

      <td>
        Updates the basket's fulfillment details, such as the fulfillment type, scheduled time, or delivery information.
      </td>
    </tr>

    <tr>
      <td>
        [Update Basket - Store](ref:update-basket-store)
      </td>

      <td>
        <PATCH_LABEL />
      </td>

      <td>
        Updates the store associated with the basket.
      </td>
    </tr>

    <tr>
      <td>
        [Update Basket - Item(s)](ref:update-basket-items)
      </td>

      <td>
        <PATCH_LABEL />
      </td>

      <td>
        Adds, removes, or updates items in the basket.
      </td>
    </tr>

    <tr>
      <td>
        [Update Basket - Customer](ref:update-basket-customer)
      </td>

      <td>
        <PATCH_LABEL />
      </td>

      <td>
        Updates the customer's information associated with the basket.
      </td>
    </tr>

    <tr>
      <td>
        [Update Basket - Group Customers](ref:update-basket-group-customers)
      </td>

      <td>
        <PATCH_LABEL />
      </td>

      <td>
        Updates the list of customers participating in a group order.
      </td>
    </tr>

    <tr>
      <td>
        [Update Basket - Policies](ref:update-basket-group-policies)
      </td>

      <td>
        <PATCH_LABEL />
      </td>

      <td>
        Updates policy acknowledgements or policy-related information associated with the basket.
      </td>
    </tr>

    <tr>
      <td>
        [Update Basket - Tip](ref:update-basket-payments)
      </td>

      <td>
        <PATCH_LABEL />
      </td>

      <td>
        Updates the gratuity or tip amount applied to the basket.
      </td>
    </tr>

    <tr>
      <td>
        [Update Basket - Donations](ref:update-donations)
      </td>

      <td>
        <PATCH_LABEL />
      </td>

      <td>
        Updates donation amounts associated with the basket.
      </td>
    </tr>

    <tr>
      <td>
        [Update Basket - Discount(s)](ref:commerce-update-basket-discounts)
      </td>

      <td>
        <PATCH_LABEL />
      </td>

      <td>
        Applies, updates, or removes discounts from the basket.
      </td>
    </tr>

    <tr>
      <td>
        [Update Basket - Charges](ref:update-basket-charges)
      </td>

      <td>
        <PATCH_LABEL />
      </td>

      <td>
        Updates additional charges applied to the basket, such as service or delivery fees.
      </td>
    </tr>
  </tbody>
</Table>
