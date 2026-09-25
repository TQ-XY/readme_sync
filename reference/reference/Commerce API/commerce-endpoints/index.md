---
title: Endpoints
deprecated: false
hidden: false
icon: fad fa-plug
metadata:
  title: Commerce API Endpoints
  description: ''
  keywords:
    - commerce api
    - 1PO
    - first party ordering
  robots: index
---
<TokenRequest />

<BaseURLsTable />

## Glossary

Below is a list of all endpoints relating to the Commerce flow, other endpoints are available via our Channel API to enhance the ordering flow e.g. to pre-validate courier availabiity;

<HTMLBlock>{`
<div class="callout-banner callout-banner--note">
  <span class="callout-icon"><i class="fa-regular fa-lightbulb"></i></span>
  <p>
    <strong>Channel Endpoints</strong><br>
  See additional endpoints available to all ordering integrators via
    <a href="https://developers.deliverect.com/v3.0-ordering-experience/reference/channel-endpoints" style="color: #1b5e20; font-weight: 600; text-decoration: underline;">this link </a>.
  </p>
</div>
`}</HTMLBlock>

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
        [Get Stores](ref:commerce-get-stores)
      </td>

      <td>
        <GET_LABEL />
      </td>

      <td>
        Returns the list of stores. A store represents a unique ordering experience from a specific location.
      </td>
    </tr>

    <tr>
      <td>
        [Get Store](ref:get-store)
      </td>

      <td>
        <GET_LABEL />
      </td>

      <td>
        Returns details of a specific store
      </td>
    </tr>

    <tr>
      <td>
        [Get Root Menu(s)](ref:get-root-menu)
      </td>

      <td>
        <GET_LABEL />
      </td>

      <td>
        Retrieves the brand-level Root Menu linked to the primary location, representing all items across the brand.
      </td>
    </tr>

    <tr>
      <td>
        [Get Store Menu(s)](ref:commerce-get-menus)
      </td>

      <td>
        <GET_LABEL />
      </td>

      <td>
        Retrieves a store's menu, including its product range and pricing details.
      </td>
    </tr>

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
        [Checkout Basket](ref:commerce-checkout)
      </td>

      <td>
        <POST_LABEL />
      </td>

      <td>
        Creates a checkout session using a unique basket ID.
      </td>
    </tr>

    <tr>
      <td>
        [Get Checkout](ref:commerce-get-checkout)
      </td>

      <td>
        <GET_LABEL />
      </td>

      <td>
        Returns a checkout session by ID. This can be used to poll the status of a checkout session, providing order placement details.
      </td>
    </tr>
  </tbody>
</Table>
